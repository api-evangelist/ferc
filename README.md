# FERC (ferc)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

The Federal Energy Regulatory Commission (FERC) is the independent United States federal agency that regulates the interstate transmission of electricity, natural gas, and oil, licenses hydropower projects, and oversees the wholesale power markets run by the seven ISOs and RTOs. FERC sits on the wholesale side of the US energy value chain — it does not regulate retail utility service, retail rates, or the customer relationship, which remain with the fifty state public utility commissions. That jurisdictional line defines FERC's API posture exactly. FERC operates a real, self-serve open data API at api.data.ferc.gov, documented at data.ferc.gov with a published OpenAPI 3.0 description, a free 40-character API key issued from a sign-up form, a 1,000-request-per-hour rate limit, and X-Api-Key header or api_key query authentication on the api.data.gov API Umbrella stack. FERC also runs a credentialed OAuth2 XBRL submission API at ecollection.ferc.gov for the mandated eForms filings. What FERC does NOT do is any part of consumer energy data — there is no Green Button, no ESPI, no consumer data right, and no individual customer usage or billing API anywhere in FERC's surface.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/ferc/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/ferc/refs/heads/main/apis.yml)

## Tags

- Energy
- United States
- Energy Markets
- Electricity
- Natural Gas
- Grid
- Regulator
- Government
- Open Data
- Wholesale Power Markets
- Hydropower
- Oil Pipelines

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### FERC Open Data API

FERC's public open data API, serving the same data assets and datasets published in the data.ferc.gov Data Catalog. A Data-Assets endpoint returns the catalog and the dataset IDs; Details, Data, and Dictionary endpoints return per-dataset metadata, full row data, and column definitions. Free self-serve API key, 1,000 requests per hour, X-Api-Key header or api_key query parameter. Runs on the api.data.gov API Umbrella stack hosted on cloud.gov. Verified live 2026-07-27 — an unauthenticated GET returns HTTP 403 with `API_KEY_MISSING` and a bogus key returns HTTP 403 with `API_KEY_INVALID`.

- **Human URL:** [https://data.ferc.gov/developer/gettingstarted/](https://data.ferc.gov/developer/gettingstarted/)
- **Base URL:** `https://api.data.ferc.gov/v1`

#### Tags

- Open Data
- Energy Markets
- Electricity
- Natural Gas
- Regulatory Data

#### Properties

- [OpenAPI](openapi/ferc-data-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://data.ferc.gov/developer/gettingstarted/)
- [API Reference](https://data.ferc.gov/developer/apiendpoints/)
- [Getting Started](https://data.ferc.gov/developer/gettingstarted/understanding-our-apis/)
- [Signup](https://data.ferc.gov/developer/gettingstarted/sign-up-form/)
- [Authentication](https://data.ferc.gov/developer/gettingstarted/api-key-usage/)
- [Rate Limits](https://data.ferc.gov/developer/gettingstarted/api-key-usage/)
- [Support](https://data.ferc.gov/developer/helpandsupport/)
- [Terms of Service](https://data.ferc.gov/disclaimer/)
- [Data Catalog](https://data.ferc.gov/datacatalog/)
- [FAQ](https://data.ferc.gov/faq/)

### FERC eForms XBRL Submission API

The machine-to-machine filing API for FERC's mandated eForms. Credentialed filers exchange their FERC eRegistration and Company Registration username and password for a bearer token at `POST /api/token` (OAuth2 password grant, `role=filer`), then POST a zipped XBRL submission to `/api/SubmissionHistory/ExternalFiling` with the company CID, report year, report period, and form identifier. This is a write API for regulated filers, not a read API for developers — there is no public data retrieval surface here. Verified live 2026-07-27 — `POST /api/token` without valid credentials returns HTTP 400 with "Failed validating user in company registration".

- **Human URL:** [https://www.ferc.gov/vendor-files-library](https://www.ferc.gov/vendor-files-library)
- **Base URL:** `https://ecollection.ferc.gov/api`

#### Tags

- XBRL
- Regulatory Filing
- eForms
- Compliance

#### Properties

- [Postman Collection](collections/ferc-xbrl-submission-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Documentation](https://www.ferc.gov/media/ferc-submission-api-step-step-guide)
- [Getting Started](https://www.ferc.gov/sites/default/files/2020-12/FERC_SubmissionAPI_PROD-Step-by-step-guide_v3.1.pdf)
- [Portal](https://ecollection.ferc.gov/)
- [Registration](https://www.ferc.gov/company-registration)
- [Documentation](https://www.ferc.gov/filing-forms/eforms-refresh)

## Common Properties

- [Website](https://www.ferc.gov)
- [Portal](https://data.ferc.gov/)
- [Documentation](https://data.ferc.gov/developer/gettingstarted/)
- [Signup](https://data.ferc.gov/developer/gettingstarted/sign-up-form/)
- [Authentication](https://data.ferc.gov/developer/gettingstarted/api-key-usage/)
- [Rate Limits](https://data.ferc.gov/developer/gettingstarted/api-key-usage/)
- [Support](https://data.ferc.gov/developer/helpandsupport/)
- [Terms of Service](https://data.ferc.gov/disclaimer/)
- [Privacy Policy](https://www.ferc.gov/privacy)
- [Vulnerability Disclosure](https://www.ferc.gov/vulnerability-disclosure-policy)
- [Strategy](https://www.ferc.gov/about/what-ferc/digital-strategy)
- [LinkedIn](https://www.linkedin.com/company/federal-energy-regulatory-commission)
- [eLibrary document repository (web only, no public API)](https://www.ferc.gov/ferc-online/elibrary)
- [Electric Quarterly Reports (EQR) — bulk download, no public API](https://www.ferc.gov/power-sales-and-markets/electric-quarterly-reports-eqr)

## Mandate Posture

- **Mandate regime:** `other` — FERC issues its own wholesale reporting mandates (EQR; eForms Form Nos. 1, 2, 3-Q, 6, 60, 552, 714 in XBRL) and incorporates NAESB WGQ/WEQ wholesale business practice standards by reference. It is **not** a consumer data right. Green Button / ESPI is NAESB Retail Electric Quadrant Book 21, which is retail and outside FERC's jurisdiction.
- **Mandate status:** `live-implemented` — verified against live endpoints, not press releases. The eForms XBRL portal, the OAuth2 token endpoint, the EQR report viewer, and the published Form 552 / Market-Based Rate Database data assets were all probed directly.
- **Consumer data API:** none. **Market data:** open.
- **Data standard:** XBRL (FERC eForms taxonomies) for filings; no energy data standard on the Open Data API.
- **Access gate:** self-serve — complete a form, receive a 40-character key by email.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
