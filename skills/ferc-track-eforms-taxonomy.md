---
name: ferc-track-eforms-taxonomy
description: >-
  Determine which FERC XBRL taxonomy version governs a given eForms filing period, fetch that
  taxonomy package and its sample forms, and resolve a specific filing to its accession number and
  attachments in eLibrary. Use when preparing or validating a FERC Form 1/1F/2/2A/3-Q/6/6Q/60/714
  filing, or when auditing what was filed.
api: openapi/ferc-eforms-api-openapi-derived.yml
base_url: https://ecollection.ferc.gov/api
operations:
  - listForms
  - listTaxonomyHistory
  - getTaxonomyFile
  - getTaxonomySampleForm
  - getTaxonomyReleaseFiles
  - getSubmissionDetail
generated: '2026-07-27'
method: generated
---

# Track the FERC eForms XBRL taxonomy

## What this covers

FERC mandates XBRL filing of its eForms. A filing is only valid against the taxonomy version in force
for its reporting period, and FERC publishes those versions — with their reporting windows and schema
URLs — through an endpoint that needs **no authentication at all**. This skill uses only the
anonymous read surface. Nothing here submits a filing.

> The operations below are described in `openapi/ferc-eforms-api-openapi-derived.yml`, an OpenAPI
> **derived** by API Evangelist from FERC's own production client bundle plus live probes. FERC
> publishes no OpenAPI for this API. Every path was verified live on 2026-07-27, but treat it as a
> best-effort description, not a contract FERC has committed to.

## Steps

### 1. Resolve the form — `listForms`

```
GET /SubmissionHistory/forms
```

Returns three parallel lists: `formList` (names), `formIDList` (numeric identifiers) and
`annualForms` (which identifiers are annual rather than quarterly).

The published mapping, which the filing endpoint also uses, is: Form 1 → 1, Form 1F → 2,
Form 3Q Electric → 3, Form 2 → 4, Form 2A → 5, Form 3Q Gas → 6, Form 6 → 7, Form 6Q → 8,
Form 60 → 9, Form 714 → 10. Note the ordering is not alphabetical and Form 2 is **4**, not 2 — this
is the single most common mistake against this API.

### 2. Find the governing taxonomy — `listTaxonomyHistory`

```
GET /TaxonomyHistory
```

Returns every published taxonomy release. For each: `versionID`, `formName`, `version` (the release
date, e.g. `2026-04-01`), the reporting window it governs (`startYear`/`startPeriod` through
`endYear`/`endPeriod`), a `revisionNumber`, and `publishString` — a JSON-encoded string of the
published `.xsd` schema URLs keyed `url0`, `url1`, …

To pick the right version: filter to your `formName`, then select the release whose window contains
your reporting year and period. An `endYear` of `null` means the release is current and open-ended.

Parse `publishString` — it is a **string containing JSON**, not a nested object. Decode it before
reading the URLs.

### 3. Get the taxonomy package — `getTaxonomyFile`

```
GET /TaxonomyHistory/TaxonomyFile/{versionID}
```

Returns a zip (`application/octet-stream`) of the taxonomy files for that version.

Do **not** use `/TaxonomyHistory/TaxonomyPackage/{versionID}` — on 2026-07-27 it returned an HTML
WAF interstitial ("The requested URL was rejected") with an HTTP **200** status. Always check the
content type before trusting a 200 from this host.

### 4. Get blank forms and sample instances — `getTaxonomySampleForm`

```
GET /TaxonomyHistory/SampleForm/{versionID}
```

Returns a zip of blank rendered forms and sample XBRL instance files for that version — the real
fixture set for building a filing.

### 5. Read the release notes — `getTaxonomyReleaseFiles`

```
GET /TaxonomyHistory/getReleaseFiles
```

Returns a **base64-encoded PDF** in the JSON body. Decode it before writing to disk.

### 6. Resolve a filing — `getSubmissionDetail`

```
GET /SubmissionDetail/{filingID}
```

Returns `accessionNumber` (format `YYYYMMDD-NNNN`), any `privilegedAccessionNumber`, CPA
certification flags, and the attachment manifest — one `XBRL_INSTANCE_FILE` and one
`HTML_RENDERING` per filing, named `{filingID}-{cid}-{Form_Name}-{year}-{period}`.

Use the accession number to open the filing in eLibrary:
`https://elibrary.ferc.gov/eLibrary/docinfo?accession_num=<accessionNumber>`

## Validate before you file

FERC publishes the pieces you need to check a filing locally, in the vendor files library
(<https://www.ferc.gov/vendor-files-library>):

- **XULE validation rulesets**, one per form category (Form 1, 2, 6, 60, 714), each covering its
  related forms — the Form 1 ruleset covers Forms 1, 1-F and 3-Q electric, and so on.
- **The FERC rendering tool**, an Arelle plugin that produces the Inline XBRL HTML exactly as FERC
  will render it.

Submission constraints are published live at `GET /getTestStatus`: maximum XBRL name length 50,
maximum file name length 60, maximum file size 52,428,800 bytes (50 MiB), allowed additional-file
tags `FileNameOfSystemMap,OrganizationChart`. Check these before zipping.

## What this skill deliberately does not do

- **It does not submit filings.** `POST /SubmissionHistory/ExternalFiling` writes a mandated
  regulatory filing to production, requires real FERC eRegistration credentials, has no idempotency
  key and no undo. Filing is a human decision.
- **It does not enumerate `PublicSubmissionHistory`.** That endpoint returns ~37,600 records
  including each filer's personal work email address, anonymously. Use `getSubmissionDetail` with a
  known `filingID` instead of bulk-pulling the index.
