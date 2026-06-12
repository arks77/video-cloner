# Adapter: <BACKEND NAME>

> Copy this file to `adapters/active.md` and fill in every section for your video API.
> The skill reads `active.md` as the single source of truth for all API specifics.
> See `example-arcads-seedance.md` for a fully worked version.
>
> Leave a section as `TODO` only if you truly don't use it — the agent will ask before
> relying on anything marked `TODO`.

## Identity

- **Backend:** <name, e.g. fal.ai / Replicate / Runway / Arcads / direct vendor>
- **Base URL / SDK:** <https://... or `npm i <sdk>`>
- **Docs:** <link>
- **Models:**

| Model | `model` value | Speaks? | Notes |
|-------|---------------|:------:|-------|
| <name> | `<id>` | yes/no | <one-liner> |

## Auth

- **Scheme:** <Bearer / HTTP Basic / x-api-key header / SDK init>
- **Secret env var:** `<VIDEO_API_KEY>` (load from `.env`; never commit; never print)
- **Probe (is auth working?):**
  ```bash
  <minimal authenticated request that 200s, e.g. list models/products>
  ```
- **On 401/403:** <how to fix — usually re-check the key in `.env`>

## upload(file) → handle

- **How:** <endpoint or SDK call>
  ```bash
  <example: request a presigned URL, PUT the bytes, capture the handle>
  ```
- **Returns:** <the handle shape — URL / id / path — that goes into submit>
- **Accepted types:** <image/jpeg, image/png, video/mp4, audio/mp3, …>
- **Limits:** <max size / max duration>
- **Handle reuse:** <reusable? OR one-time-use → re-upload before each call?>

## submit(prompt, params, refs) → jobId

- **Endpoint / call:** `<POST /...>` or `<sdk.generate(...)>`
- **Request shape:**
  ```json
  {
    "model": "<id>",
    "prompt": "<text>",
    "aspectRatio": "<9:16>",
    "duration": <n>,
    "resolution": "<720p>",
    "<refImagesField>": ["<handle>"],
    "<refVideosField>": ["<handle>"],
    "<audioField>": <true|false>,
    "projectId": "<optional>"
  }
  ```
- **Required:** <list>  **Optional:** <list>
- **Input modes & mutual exclusions:** <e.g. i2v field and v2v field can't coexist>
- **Response:** jobId is in `<field>`; final output URL will appear in `<field>` after polling.

## poll(jobId) → {status, outputUrl}

- **Endpoint / call:** `<GET /...>`
- **Status field:** `<status>` — terminal values: done=`<...>`, failed=`<...>`
- **Output URL location:** `<field on the completed job>`
- **Cadence:** poll every <N>s, back off on rate limit.
- **⚠️ Poll-path differs from submit-path?** <yes/no — if yes, document it>

## capabilities

| Model | duration | aspectRatio | resolution | input modes | ref caps | audio | price | gen speed |
|-------|----------|-------------|------------|-------------|----------|:-----:|-------|-----------|
| `<id>` | <enum/range, max> | <9:16,16:9,1:1> | <720p,1080p> | <t2v/i2v/v2v> | <imgs/vids/auds> | <y/n> | <rate> | <~Ns> |

## pricing (for estimates)

- <model>: <rate per second OR per clip>. Source: <doc / measured on YYYY-MM-DD>.
- Cost is always an **estimate** — confirm exact billing in the provider dashboard.

## gotchas (date every entry)

- `YYYY-MM-DD` — <confirmed quirk: broken field combo, billed-before-validation,
  undocumented cap, regression, …>

## error codes

| Code | Meaning | Recovery |
|------|---------|----------|
| <401/403> | auth | <fix key> |
| <422/400> | validation/moderation | <tighten prompt, check enums> |
| <5xx> | server | <retry once, then stop> |
