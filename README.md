# Boom Ai

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

Boom AI (useboom.ai) is a Y Combinator-backed (Fall 2025) San Francisco company building "an AI workforce for your customers" — autonomous agents that hold real, multi-turn conversations over SMS, email, WhatsApp, and phone in 50+ languages to run collections and payment recovery, churn recovery, retention monitoring, customer onboarding, sales qualification, and market research for e-commerce and B2B brands. Boom exposes one uniform public REST API — and a hosted MCP server over the same capabilities — covering a customer data platform (people, custom objects, behavioral events, relationships, sources), segments, initiatives and participants, and journey authoring. Authentication is a Bearer organization API key (boom_org_...); the API uses cursor pagination, 1,000 requests/minute rate limits with X-RateLimit-*/Retry-After signaling, and idempotent upsert plus up-to-1000-record batch endpoints.

**Areas:** Company · Artificial Intelligence · Conversational AI · Customer Engagement · Customer Data Platform · Messaging · WhatsApp · SMS · Marketing Automation · E-Commerce · Agents · MCP

## Boom Ai on APIs.io

Everything profiled for Boom Ai is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/boom-ai/](https://apis.io/providers/boom-ai/)** — or go straight to one of the APIs or properties below.

### APIs (11)

- [Boom Ai CDP Custom Objects API](https://apis.io/apis/boom-ai/boom-ai-cdp-custom-objects-api/) — The CDP Custom Objects API from Boom Ai — 5 operation(s) for cdp custom objects.
- [Boom Ai CDP Events API](https://apis.io/apis/boom-ai/boom-ai-cdp-events-api/) — The CDP Events API from Boom Ai — 3 operation(s) for cdp events.
- [Boom Ai CDP People API](https://apis.io/apis/boom-ai/boom-ai-cdp-people-api/) — The CDP People API from Boom Ai — 4 operation(s) for cdp people.
- [Boom Ai CDP Relationships API](https://apis.io/apis/boom-ai/boom-ai-cdp-relationships-api/) — The CDP Relationships API from Boom Ai — 4 operation(s) for cdp relationships.
- [Boom Ai CDP Sources API](https://apis.io/apis/boom-ai/boom-ai-cdp-sources-api/) — The CDP Sources API from Boom Ai — 1 operation(s) for cdp sources.
- [Boom Ai HTTP credentials API](https://apis.io/apis/boom-ai/boom-ai-http-credentials-api/) — The HTTP credentials API from Boom Ai — 1 operation(s) for http credentials.
- [Boom Ai Initiatives API](https://apis.io/apis/boom-ai/boom-ai-initiatives-api/) — The Initiatives API from Boom Ai — 14 operation(s) for initiatives.
- [Boom Ai Journeys API](https://apis.io/apis/boom-ai/boom-ai-journeys-api/) — The Journeys API from Boom Ai — 16 operation(s) for journeys.
- [Boom Ai Segments API](https://apis.io/apis/boom-ai/boom-ai-segments-api/) — The Segments API from Boom Ai — 7 operation(s) for segments.
- [Boom Ai WhatsApp templates API](https://apis.io/apis/boom-ai/boom-ai-whatsapp-templates-api/) — The WhatsApp templates API from Boom Ai — 3 operation(s) for whatsapp templates.
- [Boom Ai Environments API](https://apis.io/apis/boom-ai/boom-ai-environments-api/) — The Environments API from Boom Ai — 1 operation(s) for environments.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Boom Ai Webhooks](https://apis.io/asyncapis/boom-ai/boom-ai-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [boom](https://apis.io/servers/boom-ai/boom/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Boom Ai Agentic Access](https://apis.io/agentic-access/boom-ai/boom-ai-agentic-access/)

#### Collections (10)

Postman and Open Collection request collections.

- [Boom CDP Custom Objects API](https://apis.io/collections/boom-ai/open-boom-ai-cdp-custom-objects-api/)
- [Boom CDP Custom Objects CDP Events API](https://apis.io/collections/boom-ai/open-boom-ai-cdp-events-api/)
- [Boom CDP Custom Objects CDP People API](https://apis.io/collections/boom-ai/open-boom-ai-cdp-people-api/)
- [Boom CDP Custom Objects CDP Relationships API](https://apis.io/collections/boom-ai/open-boom-ai-cdp-relationships-api/)
- [Boom CDP Custom Objects CDP Sources API](https://apis.io/collections/boom-ai/open-boom-ai-cdp-sources-api/)
- [Boom CDP Custom Objects HTTP credentials API](https://apis.io/collections/boom-ai/open-boom-ai-http-credentials-api/)
- [Boom CDP Custom Objects Initiatives API](https://apis.io/collections/boom-ai/open-boom-ai-initiatives-api/)
- [Boom CDP Custom Objects Journeys API](https://apis.io/collections/boom-ai/open-boom-ai-journeys-api/)
- [Boom CDP Custom Objects Segments API](https://apis.io/collections/boom-ai/open-boom-ai-segments-api/)
- [Boom CDP Custom Objects WhatsApp templates API](https://apis.io/collections/boom-ai/open-boom-ai-whatsapp-templates-api/)

#### Overlays (12)

OpenAPI overlays, including conversational phrasing for each operation.

- [Boom Ai Cdp Custom Objects Api Phrasing Overlay](https://apis.io/overlays/boom-ai/boom-ai-cdp-custom-objects-api-phrasing-overlay/)
- [Boom Ai Cdp Events Api Phrasing Overlay](https://apis.io/overlays/boom-ai/boom-ai-cdp-events-api-phrasing-overlay/)
- [Boom Ai Cdp People Api Phrasing Overlay](https://apis.io/overlays/boom-ai/boom-ai-cdp-people-api-phrasing-overlay/)
- [Boom Ai Cdp Relationships Api Phrasing Overlay](https://apis.io/overlays/boom-ai/boom-ai-cdp-relationships-api-phrasing-overlay/)
- [Boom Ai Cdp Sources Api Phrasing Overlay](https://apis.io/overlays/boom-ai/boom-ai-cdp-sources-api-phrasing-overlay/)
- [Boom Ai Environments Api Phrasing Overlay](https://apis.io/overlays/boom-ai/boom-ai-environments-api-phrasing-overlay/)
- [Boom Ai Http Credentials Api Phrasing Overlay](https://apis.io/overlays/boom-ai/boom-ai-http-credentials-api-phrasing-overlay/)
- [Boom Ai Initiatives Api Phrasing Overlay](https://apis.io/overlays/boom-ai/boom-ai-initiatives-api-phrasing-overlay/)
- [Boom Ai Journeys Api Phrasing Overlay](https://apis.io/overlays/boom-ai/boom-ai-journeys-api-phrasing-overlay/)
- [Boom Ai Openapi Overlay](https://apis.io/overlays/boom-ai/boom-ai-openapi-overlay/)
- [Boom Ai Segments Api Phrasing Overlay](https://apis.io/overlays/boom-ai/boom-ai-segments-api-phrasing-overlay/)
- [Boom Ai Whatsapp Templates Api Phrasing Overlay](https://apis.io/overlays/boom-ai/boom-ai-whatsapp-templates-api-phrasing-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Boom Ai Authentication](https://apis.io/security/boom-ai/boom-ai-authentication/)
- [Boom Ai Domain Security](https://apis.io/security/boom-ai/boom-ai-domain-security/)
- [Boom Ai Trust Center](https://apis.io/security/boom-ai/boom-ai-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Boom Ai Scopes](https://apis.io/scopes/boom-ai/boom-ai-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Boom Ai Plans Pricing](https://apis.io/plans/boom-ai/boom-ai-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Boom Ai Rate Limits](https://apis.io/rate-limits/boom-ai/boom-ai-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.useboom.ai/)
- [Documentation](https://docs.useboom.ai)
- [Getting started](https://docs.useboom.ai/quickstart)
- [API reference](https://docs.useboom.ai/api-reference/overview)
- [Pricing](https://useboom.ai/pricing)
- [Sign up](https://useboom.ai/demo)
- [Blog](https://useboom.ai/blog)
- [Compliance](https://trust.useboom.ai/)
- [Terms of service](https://drive.google.com/file/d/1SlTp1_QWhVASpbxncSj1NpmFqiiGBcF1/view)
- [Privacy policy](https://drive.google.com/file/d/1ITWbsA8ZmyhinJYYr4ezRdhNe-MWQBC_/view)
- [GitHub](https://github.com/BOOM-TML)
- [Status](https://status.useboom.ai/)

## API Evangelist rating

**Kin Score 75.6** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 57.1 |
| Contract governance | 18.2 |
| Operational transparency | 55.3 |
| Developer ergonomics | 71.4 |
| Access clarity | 92.1 |

**Agent readiness 63.9** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | yes |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 36.7** — Telecommunications

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/boom-ai/](https://apis.io/providers/boom-ai/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Boom Ai: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/boom-ai/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
