# Adapter: Arcads external API — Seedance 2.0 (WORKED EXAMPLE)

> This is a reference example showing what a filled-in adapter looks like. It is NOT the
> active backend — to use it, copy it to `adapters/active.md` and confirm the values.
> Pricing and gotchas were accurate as of the dates noted; re-validate before trusting them.

## Identity

- **Backend:** Arcads external API
- **Base URL / SDK:** `https://external-api.arcads.ai` (override via `ARCADS_BASE_URL`)
- **Docs:** https://external-api.arcads.ai/docs
- **Models:**

| Model | `model` value | Speaks? | Notes |
|-------|---------------|:------:|-------|
| Seedance 2.0 | `seedance-2.0` | yes (in prompt) | UGC sweet spot; i2v + v2v; audio toggle |

## Auth

- **Scheme:** HTTP Basic — API key as username, empty password.
- **Secret env var:** `ARCADS_API_KEY`
- **Probe:**
  ```bash
  curl -sS -u "$ARCADS_API_KEY:" "https://external-api.arcads.ai/v1/products"
  ```
- **On 401/403:** key missing/wrong/no permission — re-paste into `.env`.

## upload(file) → handle

- **How:** request a presigned URL, then PUT the bytes.
  ```bash
  PRESIGN=$(curl -sS -X POST -u "$ARCADS_API_KEY:" -H "Content-Type: application/json" \
    -d '{"fileType":"image/jpeg"}' "$BASE/v1/file-upload/get-presigned-url")
  URL=$(echo "$PRESIGN" | jq -r .presignedUrl)
  HANDLE=$(echo "$PRESIGN" | jq -r .filePath)   # ← this is the handle
  curl -sS -X PUT -H "Content-Type: image/jpeg" --data-binary @file.jpg "$URL"
  ```
- **Returns:** `filePath` string → pass into `referenceImages` / `referenceVideos` / `referenceAudios`.
- **Accepted types:** image/jpeg|png|webp|heic, video/mp4|mov|webm, audio/mp3|wav|m4a|aac…
- **Handle reuse:** ⚠️ **ONE-TIME-USE** (confirmed 2026-05-19). A `filePath` works once;
  reusing it → `400 REFERENCE_FILE_NOT_FOUND`. Re-upload before each call.

## submit(prompt, params, refs) → jobId

- **Endpoint:** `POST /v2/videos/generate` (`CreateVideoDto`)
- **Request shape:**
  ```json
  {
    "model": "seedance-2.0",
    "productId": "<uuid>",
    "prompt": "<100–260 words>",
    "aspectRatio": "9:16",
    "duration": 15,
    "resolution": "720p",
    "audioEnabled": true,
    "referenceImages": ["<filePath>"],
    "projectId": "<uuid>"
  }
  ```
- **Required:** `model`, `productId`, `prompt`.
- **Input modes & mutual exclusions:** ⚠️ `referenceImages` (i2v) and `referenceVideos`
  (v2v) **cannot be combined** → `HTTP 500`. Pick one. `referenceAudios` works with either.
- **Response:** asset object; `id` is the jobId.

## poll(jobId) → {status, outputUrl}

- **Endpoint:** `GET /v1/assets/{id}` — ⚠️ **NOT** `/v1/videos/{id}`.
- **Status field:** `status` — done=`generated`, failed=`failed`.
- **Output URL location:** top-level `url` (presigned S3 `.mp4`).
- **Cadence:** every few seconds; back off on rate limit.
- **⚠️ Poll-path differs from submit-path:** YES — created at `/v2/videos/generate` but
  reported at `/v1/assets/{id}` because `type: "seedance_20"` is in the assets family
  (confirmed 2026-05-19). Polling `/v1/videos/{id}` → 404.

## capabilities

| Model | duration | aspectRatio | resolution | input modes | ref caps | audio | price | gen speed |
|-------|----------|-------------|------------|-------------|----------|:-----:|-------|-----------|
| `seedance-2.0` | 4–15s (continuous), max 15 | 9:16, 16:9 only | 480p, 720p | t2v, i2v (referenceImages≤3), v2v (referenceVideos=1 only) | imgs 3 / vids **1** / auds 3 | yes (`audioEnabled`) | ~48 cr/sec i2v @720p | 2–6 min |

## pricing (for estimates)

- Seedance i2v @720p: **~48 credits/sec** (15s ≈ 720). Audio ref does not change price.
  Source: measured across 8 runs on 2026-05-19.
- v2v @720p: likely ~80 credits/sec — re-validate.
- Always an estimate — confirm in the Arcads platform.

## gotchas (date every entry)

- `2026-05-19` — presigned upload handles are one-time-use → re-upload per call.
- `2026-05-19` — Seedance polls at `/v1/assets/{id}`, not `/v1/videos/{id}` (404 otherwise).
- `2026-04-09` — `referenceImages` + `referenceVideos` together → 500.
- `2026-04-09` — `referenceVideos` count > 1 → 500 (docs say max 3; only 1 works).
- `2026-04-09` — credits charged at create time, BEFORE content check; flagged prompts are
  billed and not refunded. Don't blindly resubmit a failed payload.

## error codes

| Code | Meaning | Recovery |
|------|---------|----------|
| 401/403 | auth/permission | re-check `ARCADS_API_KEY` in `.env` |
| 404 | wrong UUID / wrong poll path | re-fetch ids; poll `/v1/assets/{id}` for Seedance |
| 422 | validation/moderation | tighten prompt, check aspect/duration enums |
| 500 | server or bad field combo | check i2v/v2v exclusivity; retry once otherwise |
