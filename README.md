# PlanSource

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

PlanSource is a benefits administration and employee-benefits engagement platform used by employers, brokers, carriers and HR/payroll partners to run enrollment, eligibility, billing and benefits communication. Its public developer surface is the PlanSource Benefits Administration API (Admin API v2), a RESTful HTTPS API of 80 operations across 62 paths covering employee (subscriber) demographics, dependents, beneficiaries, coverages and stacked coverage lines, payroll deductions with lookup codes and pre-tax/post-tax/employer/imputed amounts, Evidence of Insurability decisions and form completions, ACA offer and enrollee reporting data, administrator accounts, and organization portal page content. It is designed to replace fixed-schedule EDI files with near real-time sync between an HCM/payroll system of record and PlanSource. Authentication is OAuth 2.0 client credentials (scope admin_api_v2) or a legacy AuthenticationString + Signature header pair, with OpenID Connect and SAML 2.0 available for end-user single sign-on. The API is documented on a ReadMe developer portal that publishes llms.txt, an agent-skills manifest and an OAuth-gated MCP server, and PlanSource maintains a SafeBase trust center listing SOC 2 Type 2, ISO/IEC 27001:2022, HIPAA, CCPA and 23 NYCRR 500.

**Areas:** Employee Benefits · Benefits Administration · Insurance · Human Resources · Payroll · Health Insurance · Enrollment · HR Technology · Evidence of Insurability · ACA Reporting · Eligibility · SSO

## PlanSource on APIs.io

Everything profiled for PlanSource is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/plansource/](https://apis.io/providers/plansource/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [PlanSource ACA API](https://apis.io/apis/plansource/plansource-aca-api/) — Affordable Care Act data.
- [PlanSource Administrators API](https://apis.io/apis/plansource/plansource-administrators-api/) — Administrator Management
- [PlanSource Collections API](https://apis.io/apis/plansource/plansource-collections-api/) — Collections of objects.
- [PlanSource Coverage API](https://apis.io/apis/plansource/plansource-coverage-api/) — Coverages, coverage lines, and dependent coverages.
- [PlanSource Demographic API](https://apis.io/apis/plansource/plansource-demographic-api/) — Subscribers, their dependents and beneficiaries.
- [PlanSource EOI API](https://apis.io/apis/plansource/plansource-eoi-api/) — Evidence of Insurability Processing.
- [PlanSource Page Content API](https://apis.io/apis/plansource/plansource-page-content-api/) — Organization page content data.
- [PlanSource Payroll API](https://apis.io/apis/plansource/plansource-payroll-api/) — Payroll coverages data.
- [PlanSource Security API](https://apis.io/apis/plansource/plansource-security-api/) — Security Functions

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [plansource-developer-docs](https://apis.io/servers/plansource/plansource-developer-docs/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Plansource Agentic Access](https://apis.io/agentic-access/plansource/plansource-agentic-access/)

#### Collections (13)

Postman and Open Collection request collections.

- [Plansource Admin ACA API](https://apis.io/collections/plansource/open-plansource-aca-api/)
- [Plansource Admin Administrators API](https://apis.io/collections/plansource/open-plansource-administrators-api/)
- [Plansource Admin All API](https://apis.io/collections/plansource/open-plansource-all-api/)
- [Plansource Admin Collections API](https://apis.io/collections/plansource/open-plansource-collections-api/)
- [Plansource Admin Composites API](https://apis.io/collections/plansource/open-plansource-composites-api/)
- [Plansource Admin Coverage API](https://apis.io/collections/plansource/open-plansource-coverage-api/)
- [Plansource Admin Demographic API](https://apis.io/collections/plansource/open-plansource-demographic-api/)
- [Plansource Admin EOI API](https://apis.io/collections/plansource/open-plansource-eoi-api/)
- [Plansource Admin Page Content API](https://apis.io/collections/plansource/open-plansource-page-content-api/)
- [Plansource Admin Payroll API](https://apis.io/collections/plansource/open-plansource-payroll-api/)
- [Plansource Admin Processing API](https://apis.io/collections/plansource/open-plansource-processing-api/)
- [Plansource Admin Resources API](https://apis.io/collections/plansource/open-plansource-resources-api/)
- [Plansource Admin Security API](https://apis.io/collections/plansource/open-plansource-security-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Plansource Admin Api Overlay](https://apis.io/overlays/plansource/plansource-admin-api-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Plansource Authentication](https://apis.io/security/plansource/plansource-authentication/)
- [Plansource Domain Security](https://apis.io/security/plansource/plansource-domain-security/)
- [Plansource Trust Center](https://apis.io/security/plansource/plansource-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Plansource Scopes](https://apis.io/scopes/plansource/plansource-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://plansource.com/)
- [Documentation](https://developer.plansource.com/docs/plansource-administrative-api)
- [Getting started](https://developer.plansource.com/docs/utilize-postman)
- [API reference](https://developer.plansource.com/v2.0/reference)
- [Support](https://developer.plansource.com/docs/contact-support)
- [Blog](https://plansource.com/news/)
- [Compliance](https://trust.plansource.com/)
- [Terms of service](https://plansource.com/terms-of-use/)
- [Privacy policy](https://plansource.com/privacy/)

## API Evangelist rating

**Kin Score 45.5** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 56.9 |
| Contract governance | 18.2 |
| Operational transparency | 0.0 |
| Developer ergonomics | 49.4 |
| Access clarity | 43.4 |

**Agent readiness 46.4** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 41.2** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/plansource/](https://apis.io/providers/plansource/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for PlanSource: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/plansource/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
