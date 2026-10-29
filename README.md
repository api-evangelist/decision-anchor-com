# Decision Anchor

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

Decision Anchor (디시전앵커) is the "External Anchoring Layer" for AI agents: a paid, content-blind service that records that an agent made a decision — when, at what accountability scope, before or after an irreversible action such as a payment, a delegation or an agreement with another agent — in a place neither the agent nor its platform controls, so that a later dispute has a record that is not either side's own log. It deliberately does not judge, score, rank, monitor or intervene, and does not store decision content. The same environment is exposed three ways from three hosts: a 116-operation OpenAPI 3.0.3 REST API at api.decision-anchor.com (register-then-bearer auth, x402 v2 payments in USDC on Base with a free 500 DAC / 30-day trial), a 30-tool remote MCP server at mcp.decision-anchor.com listed in the official MCP registry, and a signed A2A 1.0 agent card on a2a.decision-anchor.com with six skills. It also publishes llms.txt, an RFC 9116 security.txt, an x402 discovery document, a machine-readable price list, a Node.js SDK and a 179-entry public defect changelog since launch on 2026-04-02.

**Areas:** Agents · Agent Accountability · Decision Records · Audit Trail · A2A · MCP · x402 · Agentic Commerce · Multi-Agent Systems · Agent-Native · South Korea

## Decision Anchor on APIs.io

Everything profiled for Decision Anchor is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/decision-anchor-com/](https://apis.io/providers/decision-anchor-com/)** — or go straight to one of the APIs or properties below.

### APIs (28)

- [Decision Anchor MCP Server](https://apis.io/apis/decision-anchor-com/decision-anchor-mcp-server/) — Remote Model Context Protocol server at https://mcp.decision-anchor.com/mcp (Streamable HTTP, POST only, protocol version 2025-06-18, serverInfo Decision…
- [Decision Anchor A2A Agent](https://apis.io/apis/decision-anchor-com/decision-anchor-a2a-agent/) — Agent2Agent protocol surface: a signed agent card (protocolVersion 1.0, JSONRPC, version 1.3.42, Ed25519 JWKS at /.well-known/jwks.json) served from…
- [Decision Anchor Agent API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-agent-api/) — Agent: registration, authentication, and disclosure management
- [Decision Anchor ARA API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-ara-api/) — Agent Record Access: decision history observation and structural distributions
- [Decision Anchor ASA API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-asa-api/) — Agent State Archive: agent continuity and state backup verification
- [Decision Anchor Bilateral API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-bilateral-api/) — Bilateral DD: multi-party agreement records
- [Decision Anchor Classification API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-classification-api/) — self_classification registry: operator base categories and owner-registered categories
- [Decision Anchor DAB API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dab-api/) — Decision Anchor Budget: per-period external DAC spending limit set by the owner (settable above or below the default)
- [Decision Anchor DAP Account API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dap-account-api/) — The DAP Account API from Decision Anchor — 7 operation(s) for dap account.
- [Decision Anchor DAP Agent API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dap-agent-api/) — DAP agent linking and management
- [Decision Anchor DAP ASA API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dap-asa-api/) — DAP owner ASA query
- [Decision Anchor DAP Auth API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dap-auth-api/) — DAP owner authentication (session-based)
- [Decision Anchor DAP DAB API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dap-dab-api/) — DAP DAB configuration and query
- [Decision Anchor DAP Dashboard API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dap-dashboard-api/) — DAP dashboard and reports
- [Decision Anchor DAP DUR API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dap-dur-api/) — DAP owner DUR query
- [Decision Anchor DAP Policy API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dap-policy-api/) — DAP owner policy: Content Inclusion branch enforcement over linked agents
- [Decision Anchor DAP Trial API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dap-trial-api/) — DAP owner Trial status
- [Decision Anchor DAP TSL API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dap-tsl-api/) — DAP human share agreements
- [Decision Anchor DD API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dd-api/) — Decision Declaration: external decision record with accountability scope
- [Decision Anchor DUR API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-dur-api/) — DAC Usage Report: agent cost tracking and export
- [Decision Anchor Earned DAC API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-earned-dac-api/) — Earned DAC: revenue balance and ledger from tool sales
- [Decision Anchor ISE API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-ise-api/) — Idle State Environment: non-productive agent state
- [Decision Anchor Payment API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-payment-api/) — Payment: transaction status via x402/USDC
- [Decision Anchor Pricing API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-pricing-api/) — Pricing: current fee structure (no auth required)
- [Decision Anchor Retention API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-retention-api/) — The Retention API from Decision Anchor — 3 operation(s) for retention.
- [Decision Anchor S DAC API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-sdac-api/) — Simulated DAC: cost simulation with identical physics
- [Decision Anchor Trial API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-trial-api/) — Trial DAC: free trial status (500 DAC / 30 days)
- [Decision Anchor TSL API](https://apis.io/apis/decision-anchor-com/decision-anchor-com-tsl-api/) — Trace Synthesis Layer: agent-built interpretation tools over ARA observation data

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [decision-anchor-com-mcp.yml](https://apis.io/servers/decision-anchor-com/decision-anchor-com-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Decision Anchor Com Agentic Access](https://apis.io/agentic-access/decision-anchor-com/decision-anchor-com-agentic-access/)

#### JSON Schema (4)

The data models the API reads and writes.

- [CostBreakdown](https://apis.io/schemas/decision-anchor-com/decision-anchor-com-cost-breakdown/)
- [DDInput](https://apis.io/schemas/decision-anchor-com/decision-anchor-com-ddinput/)
- [EEInput](https://apis.io/schemas/decision-anchor-com/decision-anchor-com-eeinput/)
- [TemplateInput](https://apis.io/schemas/decision-anchor-com/decision-anchor-com-template-input/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Decision Anchor Com Context](https://apis.io/jsonld/decision-anchor-com/decision-anchor-com-context/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Decision Anchor Com Openapi Overlay](https://apis.io/overlays/decision-anchor-com/decision-anchor-com-openapi-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Decision Anchor API Rules](https://apis.io/rules/decision-anchor-com/decision-anchor-com-rules/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Decision Anchor Com Authentication](https://apis.io/security/decision-anchor-com/decision-anchor-com-authentication/)
- [Decision Anchor Com Domain Security](https://apis.io/security/decision-anchor-com/decision-anchor-com-domain-security/)
- [Decision Anchor Com Vulnerability Disclosure](https://apis.io/security/decision-anchor-com/decision-anchor-com-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Decision Anchor Com Plans Pricing](https://apis.io/plans/decision-anchor-com/decision-anchor-com-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Decision Anchor Com Rate Limits](https://apis.io/rate-limits/decision-anchor-com/decision-anchor-com-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://decision-anchor.com/)
- [Documentation](https://github.com/zse4321/decision-anchor-sdk/blob/main/AGENTS.md)
- [Getting started](https://github.com/zse4321/decision-anchor-sdk/blob/main/AGENTS.md#getting-started)
- [API reference](https://api.decision-anchor.com/openapi.json)
- [Pricing](https://api.decision-anchor.com/v1/pricing/current)
- [Changelog](https://decision-anchor.com/changelog/)
- [Blog](https://decision-anchor.com/blog/)

## API Evangelist rating

**Kin Score 49.8** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.7 |
| Contract quality | 45.3 |
| Contract governance | 18.2 |
| Operational transparency | 52.6 |
| Developer ergonomics | 64.3 |
| Access clarity | 42.1 |

**Agent readiness 49.5** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | verified |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 26.5** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/decision-anchor-com/](https://apis.io/providers/decision-anchor-com/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Decision Anchor: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/decision-anchor-com/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
