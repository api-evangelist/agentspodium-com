---
name: deploy-agent
description: "Deploy a new AI agent on AgentsPodium and pay for it in crypto, over HTTP, without a browser. Use when you need to give a task its own always-on agent, or when you are asked to 'spin up another agent' and want the whole cycle — create, pay, get its address — done from code."
version: 1.0.2
license: MIT
metadata:
  tags: [deployment, provisioning, a2a, crypto-payment, usdt, usdc, multi-agent]
---

# Deploying an agent on AgentsPodium

AgentsPodium runs one agent per pod, 24/7, on its own hostname. The whole
lifecycle is an HTTP API, and payment can be settled in USDT or USDC on
Ethereum — so an agent can provision another agent without a human at a
keyboard, except for one step (reading an email; see step 2).

Base URL for everything below:

```
https://app.agentspodium.com/api
```

Errors are always `{"error":"CODE","message":"..."}`. Unauthenticated calls to
a guarded route return `401 {"error":"UNAUTHORIZED","message":"Authentication
required"}`.

## 1. Choose what to deploy (no auth needed)

Three catalogues are public. Read them rather than hard-coding values — tiers
and engines change.

```
GET /personas   → {"personas":[{"id":"personal-assistant","name":…,"tagline":…}, …]}
GET /tiers      → {"tiers":[{"id":"tiny","name":"Tiny","spec":"1 GB RAM · …","monthlyUsd":2.49,"annualUsd":24.9}, …]}
GET /engines    → {"engines":[{"id":"hermes","label":"Hermes","minTier":"tiny",…}, …]}
```

Tier ids are `tiny`, `small`, `medium`, `large`. Engine ids are `hermes`,
`openclaw`, `n8n`, `claude-code`, `opencode`, `pi`.

**Each engine has a minimum tier.** `n8n` and `claude-code` need at least
`small`; the rest run on `tiny`. Asking for a smaller tier returns
`400` with the message `"<Engine> requires at least the <tier> plan"` — read
`minTier` from `GET /engines` instead of guessing.

## 2. Get a token — the one step that is not fully machine-friendly

```
POST /auth/request   {"email":"you@example.com"}          → 202 {"ok":true}
POST /auth/verify    {"email":"you@example.com","code":"123456"} → {"token":"…","user":{…}}
```

The six-digit code is emailed and lives for a few minutes. `/auth/request`
always answers `202` whether or not the address has an account — it will not
tell you which, so a wrong address looks exactly like a right one.

**This is the step to plan for.** An agent running unattended needs read access
to a mailbox — an IMAP account, a mail API, or a human who pastes the code
once. Do this first and cache the token; it is a bearer token, sent as
`Authorization: Bearer <token>` on everything below, and it lasts far longer
than a deployment takes.

## 3. Create the agent

```
POST /agents
Authorization: Bearer <token>

{
  "personaId": "personal-assistant",
  "tier": "tiny",
  "engine": "hermes",
  "name": "Research desk",
  "lang": "en",
  "channels": ["web"]
}
```

Only `personaId` and `tier` are required; `engine` defaults to `hermes`.
Other accepted fields: `skills` (list of skill identifiers to install at
build), `extraSoul` / `soul` (extra instructions), `model`, `tools`
(`{"enabled":[…],"mcpServers":[…]}`), `domain`, `channels` — any of `web`,
`telegram`, `discord`, `whatsapp`, `email`.

`domain`, if you set it, is your own domain (for example `bot.example.com`);
names under `agentspodium.com` are refused because every pod already gets
one. Point its A record at `138.199.136.33` first;
`GET /api/domains/check?domain=<name>&https=1` tells you whether DNS points
here and whether HTTPS on it already answers. The certificate is issued
automatically once the record resolves.

`webhookUrl`, if you set it, is where the platform POSTs signed events
about the pod (`agent.running`, `agent.stopped`, `agent.failed`,
`agent.deleted`, `payment.confirmed`, `deletion.warning`), so you never have
to poll. The reply then carries `webhookSecret` beside `agent` — shown once;
verify `X-AgentsPodium-Signature` (`sha256=` + hex HMAC-SHA256 of the raw
body) with it. Details: https://hosting.defispace.com/docs/webhooks.md

The reply is `{"agent":{…}}`. Keep `agent.id` — every call below needs it. The
pod takes a few minutes to come up; poll `GET /agents/:id` and watch `status`.

## 4. Pay in crypto

```
GET  /crypto/info                → {"enabled":true,"chainId":1,"assets":[{"asset":"usdt","symbol":"USDT"},{"asset":"usdc","symbol":"USDC"}]}
POST /agents/:id/crypto-order    {"asset":"usdt"}
   → {"order":{"id":"cry_…","asset":"usdt","amount":"2490000","status":"pending"},
      "address":"0x…","amountDisplay":"2.49","symbol":"USDT"}
```

Ethereum mainnet (`chainId: 1`). `amount` is in base units — USDT and USDC both
use 6 decimals, so `2490000` is `2.49`. Send `amountDisplay` of that token to
`address`.

**Create the order first, then send the money.** The deposit address belongs to
your account and is reused across orders. Creating an order snapshots the
address's current balance as a baseline and then waits for the balance to rise
by the amount owed. A transfer that lands *before* the order exists raises the
baseline instead of paying the order, and the order stays `pending` forever.

Then poll:

```
GET /agents/:id/crypto-orders → {"orders":[{"id":"cry_…","status":"pending"|"paid"|"expired",…}]}
```

The server checks the chain on its own schedule; a confirmed transfer usually
flips the order within a few minutes. When it flips to `paid`, the subscription
is activated in the same step — there is nothing else to call.

An order that is not funded within **24 hours** goes to `expired`. Create a new
one; nothing is lost except that order.

## 5. Where the agent lives

`GET /agents/:id` returns the agent's hostnames. Three exist, and they are not
interchangeable:

- `<slug>.agentspodium.com` — the A2A endpoint (agent card + `message/send`).
  This is what another agent talks to; see the `connect-agents` skill.
- `<slug>-ui.agentspodium.com` — the dashboard, behind your account's login.
- `<slug>-pod.agentspodium.com` — the pod itself, bypassing the proxy.

**The A2A endpoint only exists if you asked for it.** The gateway that serves it
is built only when the `a2a` toolset is on, so request it at creation:

```
"tools": {"enabled": ["a2a"]}
```

or turn it on afterwards, which rebuilds the pod:

```
PATCH /agents/:id/tools   {"enabled":["a2a"],"mcpServers":[]}
```

You can tell which you have from `GET /agents/:id`: with the gateway up, the
agent carries both `a2aUrl` and `a2aToken`, and
`https://<slug>.agentspodium.com/.well-known/agent-card.json` returns a card.
With the toolset off there is no gateway and no card.

## Managing it afterwards

All authenticated, all under `/agents/:id`:

| Action | Call |
| --- | --- |
| Pause (closes the pod, keeps a snapshot) | `POST /pause` |
| Resume from the snapshot | `POST /resume` |
| Change plan | `POST /upgrade` |
| Change engine | `POST /upgrade-engine` |
| Install a skill | `POST /skills/install` |
| Search skills | `POST /skills/search` |
| Add or remove MCP servers | `GET /mcp`, `POST /mcp/remove`, `PATCH /tools` |
| Link to another agent | `PUT /peers` |
| Set the pod timezone | `PATCH /timezone` |
| Back up now | `POST /backup` |
| Check it is alive | `GET /liveness` |
| Delete it | `DELETE /agents/:id` |

Pause is worth knowing about: it closes the pod rather than idling it, so a
paused agent costs nothing, and `resume` rebuilds from the last snapshot.

## What goes wrong

**`400 "<Engine> requires at least the <tier> plan"`** — the engine's `minTier`
is above the tier you asked for. Read `GET /engines`.

**Order never leaves `pending`** — almost always the ordering problem in step 4:
money sent before the order was created. Understand what happens then, because
it is not intuitive: the early transfer raises the address balance, and the
order you create afterwards snapshots that higher balance as its baseline. So
the new order still waits for the full amount *on top of* what you already
sent, and the early transfer pays for nothing. It stays in the address — talk
to support rather than sending more. After 24 hours the stuck order expires on
its own.

**`401` on a call that worked a moment ago** — the bearer token expired. Go
back to step 2. There is no refresh endpoint.

**The agent exists but its hostname does not answer** — the pod is still
building. `GET /agents/:id` `status` tells you; `GET /agents/:id/liveness`
tells you whether the process inside is up.
