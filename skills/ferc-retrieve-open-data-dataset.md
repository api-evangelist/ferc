---
name: ferc-retrieve-open-data-dataset
description: >-
  Find the right FERC open dataset and retrieve it correctly — resolve the dataset ID from the
  catalog, read the column dictionary, size the response, then pull the rows. Use for FERC
  market-based rates, Form 552 gas transactions, Form 556 qualifying facilities, company
  registration, annual charges, information collections, and the NEPA project schedule.
api: openapi/ferc-data-api-openapi.json
base_url: https://api.data.ferc.gov/v1
operations:
  - data-asset-id
  - detail-id
  - dictionary-id
  - data-id
generated: '2026-07-27'
method: generated
---

# Retrieve a FERC open dataset

## Before you start

You need a free FERC API key. It is a 40-character string, requested from
<https://data.ferc.gov/developer/gettingstarted/sign-up-form/> and emailed to you — usually instantly,
sometimes up to 24 hours. There is no test key and no sandbox key; the free production key is the
only credential.

Send it as a header on every request:

```
X-Api-Key: <your key>
```

The `?api_key=` query parameter also works, but FERC documents it as less secure because the key
lands in URLs and logs. Prefer the header.

## Rules that will bite you if you ignore them

1. **Dataset IDs are not stable.** FERC says so twice in its own documentation. Never hard-code an
   ID. Resolve it from the catalog at the start of every run.
2. **There is no filtering and no pagination.** `data-id` returns the entire dataset in one response.
   Always read the record count from `detail-id` first and decide whether you can hold it.
3. **The interactive console lies about size.** Executing an endpoint on the API Endpoints page
   returns only the first 100 rows. The same call from your client returns everything. If your
   record counts disagree with what you saw in the browser, this is why.
4. **A missing or bad key returns 403, not 401.** The spec documents 401; the live api.data.gov
   gateway returns 403 with `API_KEY_MISSING` or `API_KEY_INVALID`. Handle 403 as an auth failure.
5. **Budget your calls.** 1,000 requests per hour per key, rolling. Read `X-RateLimit-Limit` and
   `X-RateLimit-Remaining` off every response. Exceeding it returns 429 and temporarily blocks the
   key. Higher limits require contacting support.

## Steps

### 1. List the catalog — `data-asset-id`

```
GET /data-assets/
```

Returns an array of data assets. Each asset carries `id`, `title`, `description`, `program_office`,
`url`, `source` and point-of-contact fields, and nests a `data-sets` array. **The dataset IDs you
need are inside that nested array, not on the asset itself.**

As of 2026-07-27 the catalog holds seven assets: Annual Charges; Company Registration; FERC Form 556
(Certification of Qualifying Facility Status); FERC Information Collections Management; Form No. 552
Download Data; Market-Based Rate Database; NEPA Schedule for Pending Infrastructure Projects. FERC
adds to this over time with no announcement, so read the list rather than assuming it.

Match on the asset and dataset `title`/`description` to pick your dataset ID.

### 2. Size it and check freshness — `detail-id`

```
GET /dataset/{id}/details/
```

Returns the dataset's description, associated industry, record count, most recent update timestamp,
source URL and point of contact. Use the record count to decide whether to pull the data at all, and
the update timestamp to decide whether you need to.

A 404 here means the ID does not exist — go back to step 1 and re-resolve it.

### 3. Learn the columns — `dictionary-id`

```
GET /dataset/{id}/dictionary/
```

Returns `column_id`, `column_name`, `data_type`, `description` and `description_url` per column. Do
this before you interpret any rows: the rows come back as untyped JSON objects and FERC's OpenAPI
does not describe per-dataset schemas anywhere else.

**A 404 here is normal.** FERC states that data dictionaries do not exist for every dataset. Treat it
as "no dictionary published" and continue — do not retry and do not treat it as a bad ID.

### 4. Pull the rows — `data-id`

```
GET /dataset/{id}/data/
```

Returns every row. Stream or write to disk rather than holding the whole body in memory if the
record count from step 2 was large.

## Error handling

| Status | Meaning | What to do |
|---|---|---|
| 403 `API_KEY_MISSING` | No key sent | Add the `X-Api-Key` header |
| 403 `API_KEY_INVALID` | Bad or deactivated key | Re-copy the 40 characters, or request a new key |
| 404 | Dataset ID does not exist, or (on dictionary) none published | Re-resolve the ID from step 1; for dictionary, continue without one |
| 405 | Wrong method | Every operation is GET-only |
| 429 | Rate limit exceeded | Back off; the key is temporarily blocked. Watch the remaining header |
| 500 | Database or server failure | Retry with backoff; quote `x-api-umbrella-request-id` to support |

Errors are `{"error": {"code": "...", "message": "..."}}` — not RFC 9457 problem+json. Every response
carries `x-api-umbrella-request-id`; capture it, it is what FERC support will ask for.

## Scope reminder

FERC is a wholesale regulator. There is no consumer, retail, customer-usage or billing data in this
API and there will not be — that jurisdiction belongs to the fifty state public utility commissions.
If a task asks for individual customer energy data, FERC is the wrong source.
