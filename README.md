# FERC

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

The Federal Energy Regulatory Commission (FERC) is the independent United States federal agency that regulates the interstate transmission of electricity, natural gas, and oil, licenses hydropower projects, and oversees the wholesale power markets run by the seven ISOs and RTOs. FERC sits on the wholesale side of the US energy value chain — it does not regulate retail utility service, retail rates, or the customer relationship, which remain with the fifty state public utility commissions. That jurisdictional line defines FERC's API posture exactly. FERC operates a real, self-serve open data API at api.data.ferc.gov, documented at data.ferc.gov with a published OpenAPI 3.0 description, a free 40-character API key issued from a sign-up form, a 1,000-request-per-hour rate limit, and X-Api-Key header or api_key query authentication on the api.data.gov API Umbrella stack — genuinely open market and regulatory data covering the Market-Based Rate Database, FERC Form No. 552 natural gas transactions, FERC Form 556 qualifying facility certifications, Company Registration, Annual Charges, Information Collections Management, and the NEPA infrastructure schedule. FERC also runs a credentialed OAuth2 XBRL submission API at ecollection.ferc.gov for the mandated eForms filings (Form Nos. 1, 2, 3-Q, 6, 60, 552, 714). What FERC does NOT do is any part of consumer energy data — there is no Green Button, no ESPI, no consumer data right, and no individual customer usage or billing API anywhere in FERC's surface, because retail customer data is outside its statutory reach. FERC is therefore an open-market-data, zero-consumer-data regulator, and it publishes a better documented API than most of the utilities it indirectly touches.

**Areas:** Energy · United States · Energy Markets · Electricity · Natural Gas · Grid · Regulator · Government · Open Data · Wholesale Power Markets · Hydropower · Oil Pipelines

## FERC on APIs.io

Everything profiled for FERC is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/ferc/](https://apis.io/providers/ferc/)** — or go straight to one of the APIs or properties below.

### APIs (8)

- [FERC Data API](https://apis.io/apis/ferc/ferc-data-api/) — The Data API from FERC — 1 operation(s) for data.
- [FERC Data Assets API](https://apis.io/apis/ferc/ferc-data-assets-api/) — The Data-Assets API from FERC — 1 operation(s) for data-assets.
- [FERC Details API](https://apis.io/apis/ferc/ferc-details-api/) — The Details API from FERC — 1 operation(s) for details.
- [FERC Dictionary API](https://apis.io/apis/ferc/ferc-dictionary-api/) — The Dictionary API from FERC — 1 operation(s) for dictionary.
- [FERC Filing API](https://apis.io/apis/ferc/ferc-filing-api/) — Credentialed machine-to-machine submission of XBRL filings.
- [FERC Public Filings API](https://apis.io/apis/ferc/ferc-public-filings-api/) — Anonymous read access to the public FERC eForms submission record.
- [FERC Reference API](https://apis.io/apis/ferc/ferc-reference-api/) — Form lists and submission constraints.
- [FERC Taxonomy API](https://apis.io/apis/ferc/ferc-taxonomy-api/) — XBRL taxonomy versions, packages and sample forms for the FERC eForms.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### Arazzo workflows (1)

Multi-step workflows that chain operations into a business task.

- [FERC open data — discover a dataset and retrieve it](https://apis.io/arazzos/ferc/ferc-dataset-discovery-and-retrieval/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Ferc Agentic Access](https://apis.io/agentic-access/ferc/ferc-agentic-access/)

#### JSON Schema (5)

The data models the API reads and writes.

- [FormList](https://apis.io/schemas/ferc/ferc-form-list/)
- [PublicSubmission](https://apis.io/schemas/ferc/ferc-public-submission/)
- [SubmissionDetail](https://apis.io/schemas/ferc/ferc-submission-detail/)
- [TaxonomyVersion](https://apis.io/schemas/ferc/ferc-taxonomy-version/)
- [TestStatus](https://apis.io/schemas/ferc/ferc-test-status/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Ferc Context](https://apis.io/jsonld/ferc/ferc-context/)

#### Collections (2)

Postman and Open Collection request collections.

- [API Endpoints](https://apis.io/collections/ferc/open-ferc-data-api/)
- [FERC eForms (eCollection) API](https://apis.io/collections/ferc/open-ferc-eforms-api-openapi-derived/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Ferc Data Api Overlay](https://apis.io/overlays/ferc/ferc-data-api-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [FERC API Rules](https://apis.io/rules/ferc/ferc-rules/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Ferc Authentication](https://apis.io/security/ferc/ferc-authentication/)
- [Ferc Domain Security](https://apis.io/security/ferc/ferc-domain-security/)
- [Ferc Vulnerability Disclosure](https://apis.io/security/ferc/ferc-vulnerability-disclosure/)

#### Rate limits (1)

Published request limits.

- [Ferc Rate Limits](https://apis.io/rate-limits/ferc/ferc-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.ferc.gov)
- [Documentation](https://data.ferc.gov/developer/gettingstarted/)
- [Getting started](https://data.ferc.gov/developer/gettingstarted/understanding-our-apis/)
- [API reference](https://data.ferc.gov/developer/apiendpoints/)
- [Sign up](https://data.ferc.gov/developer/gettingstarted/sign-up-form/)
- [Support](https://data.ferc.gov/developer/helpandsupport/)
- [Security](https://www.ferc.gov/media/ferc-vulnerability-disclosure-policy)
- [Terms of service](https://data.ferc.gov/disclaimer/)
- [Privacy policy](https://www.ferc.gov/privacy)

## API Evangelist rating

**Kin Score 50.4** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 67.9 |
| Contract quality | 45.0 |
| Contract governance | 22.0 |
| Operational transparency | 55.3 |
| Developer ergonomics | 64.9 |
| Access clarity | 34.2 |

**Agent readiness 31.8** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 36.1** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/ferc/](https://apis.io/providers/ferc/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for FERC: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/ferc/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
