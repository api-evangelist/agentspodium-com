# AgentsPodium

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

AgentsPodium runs personal AI agents around the clock, each on its own pod with its own memory and files, answering in the owner's messenger. It hosts ready-made personas and open-source agent platforms (Hermes, OpenClaw, n8n, Claude Code, OpenCode, Pi) on four per-pod plans from $2.49 a month with a 7-day free trial; the model key is the customer's own. The same service is driven by agents through an HTTP account API (OpenAPI 3.1, 52 operations, bearer API key), a hosted MCP server with 13 tools, an A2A agent with five skills, four published Agent Skills, and signed webhooks. The developer documentation lives on the operator's second brand, DefiSpace Hosting (hosting.defispace.com); the company behind both is Radiance Team.

**Areas:** AI Agents · Agent Hosting · MCP · A2A · Agent-Native · Hosting · Webhook · Personal Assistants · Company

## AgentsPodium on APIs.io

Everything profiled for AgentsPodium is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/agentspodium-com/](https://apis.io/providers/agentspodium-com/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [AgentsPodium Hosting MCP Server](https://apis.io/apis/agentspodium-com/mcp-server/) — Hosted, agent-native MCP server (Streamable HTTP, protocol 2025-06-18, server agentspodium-hosting 1.0.4) exposing hosting as 13 tools — list_platforms,…
- [AgentsPodium Hosting A2A Agent](https://apis.io/apis/agentspodium-com/a2a-agent/) — The hosting service as an A2A agent (protocol 0.3.0, JSON-RPC message/send at https://a2a.agentspodium.com/hosting/) with five skills — create-instance,…
- [AgentsPodium A2A API](https://apis.io/apis/agentspodium-com/agentspodium-com-a2a-api/) — The public agent-to-agent directory.
- [AgentsPodium Agents API](https://apis.io/apis/agentspodium-com/agentspodium-com-agents-api/) — Create, configure, and operate a pod.
- [AgentsPodium API keys API](https://apis.io/apis/agentspodium-com/agentspodium-com-api-keys-api/) — Machine credentials for agents.
- [AgentsPodium Auth API](https://apis.io/apis/agentspodium-com/agentspodium-com-auth-api/) — Sign in.
- [AgentsPodium Catalog API](https://apis.io/apis/agentspodium-com/agentspodium-com-catalog-api/) — Read-only reference data: personas, tiers, engines, tools, models, providers.
- [AgentsPodium Payment API](https://apis.io/apis/agentspodium-com/agentspodium-com-payment-api/) — Subscriptions and payment providers.
- [AgentsPodium Status API](https://apis.io/apis/agentspodium-com/agentspodium-com-status-api/) — Platform health.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Agentspodium Com Webhooks](https://apis.io/asyncapis/agentspodium-com/agentspodium-com-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [AgentsPodium Hosting](https://apis.io/servers/agentspodium-com/agentspodium-hosting/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Agentspodium Com Agentic Access](https://apis.io/agentic-access/agentspodium-com/agentspodium-com-agentic-access/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Agentspodium Com Openapi Overlay](https://apis.io/overlays/agentspodium-com/agentspodium-com-openapi-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Agentspodium Com Authentication](https://apis.io/security/agentspodium-com/agentspodium-com-authentication/)
- [Agentspodium Com Domain Security](https://apis.io/security/agentspodium-com/agentspodium-com-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Agentspodium Com Plans Pricing](https://apis.io/plans/agentspodium-com/agentspodium-com-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Agentspodium Com Rate Limits](https://apis.io/rate-limits/agentspodium-com/agentspodium-com-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://agentspodium.com/)
- [Documentation](https://hosting.defispace.com/docs/)
- [Getting started](https://hosting.defispace.com/docs/quickstart.html)
- [API reference](https://hosting.defispace.com/openapi.json)
- [Pricing](https://hosting.defispace.com/#pricing)
- [Blog](https://agentspodium.com/articles)
- [GitHub](https://github.com/agentspodium)
- [Status](https://agentspodium.com/api/status)

## API Evangelist rating

**Kin Score 54.1** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 56.4 |
| Contract governance | 18.2 |
| Operational transparency | 55.3 |
| Developer ergonomics | 59.5 |
| Access clarity | 55.3 |

**Agent readiness 53.0** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | yes |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 20.6** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/agentspodium-com/](https://apis.io/providers/agentspodium-com/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for AgentsPodium: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/agentspodium-com/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
