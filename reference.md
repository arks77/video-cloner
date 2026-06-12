# reference — the adapter contract + generic video mechanics

This file defines **what every backend adapter must provide** and the **backend-independent
mechanics** the skill relies on. The concrete values for your chosen API live in
`adapters/active.md`; this file is the interface that file implements.

---

## Part A — The adapter contract

A backend is "supported" when `adapters/active.md` answers all of the following. The
fill-in template is [`adapters/_ADAPTER.template.md`](adapters/_ADAPTER.template.md).

### A1. Identity
- **Backend name** and base URL / SDK.
- **Models** available and their `model` identifiers.

### A2. `auth` — authentication
- Scheme (Bearer token, HTTP Basic, API key header, SDK init…).
- Which env var holds the secret (e.g. `VIDEO_API_KEY`).
- A minimal "is auth working?" probe call.
- **Never** print, log, or commit secrets.

### A3. `upload(file) → handle`
- Endpoint / SDK call to upload a reference image, video, or audio.
- What it returns (a URL, a file id, a path) — the **handle** passed into `submit`.
- Accepted file types and size/duration limits.
- **Reuse rule:** is a handle reusable, or one-time-use? (Some backends burn a handle
  after one generation — if so, re-upload before each call.)

### A4. `submit(prompt, params, refs) → jobId`
- The generation endpoint / SDK call and request shape.
- Required vs optional params: `model`, `prompt`, `aspectRatio`, `duration`,
  `resolution`, reference handles, audio flag, project id.
- **Input modes** the backend supports and any **mutual exclusions** (e.g.
  image-to-video vs video-to-video can't be combined).
- What the response returns: the `jobId` (and which field carries the eventual output).

### A5. `poll(jobId) → {status, outputUrl}`
- The status endpoint / SDK call.
- The status field name and its terminal values (map them to `done` / `failed`).
- Where the final video/image URL appears on a completed job.
- Polling cadence + backoff guidance.
- **Gotcha to record:** if the poll path differs from the submit path (some backends
  create on one route but report status on another), document it here.

### A6. `capabilities` — the matrix
For each model, record:

| Field | What to capture |
|-------|-----------------|
| `duration` | fixed enum or continuous range; max clip length |
| `aspectRatio` | supported values (`9:16`, `16:9`, `1:1`, …) |
| `resolution` | supported values |
| input modes | text-to-video, image-to-video (`startFrame` / `referenceImages`), video-to-video |
| reference caps | max images / videos / audios per call |
| audio/speech | does the model speak? is there an audio toggle? |
| pricing | rate per second or per clip (for estimates) |
| gen speed | rough wall-clock to generate |

### A7. `gotchas` — the scar tissue
The single most valuable section over time. Record every confirmed quirk **with a date**:
broken field combos, billed-before-validation behavior, regressions, undocumented caps.
This is what keeps the skill from repeating expensive mistakes.

---

## Part B — Generic video mechanics (backend-independent)

### B1. Input modes
- **text-to-video (t2v):** prompt only. Backend invents everything.
- **image-to-video (i2v):** a product/person still anchors identity. Best for brand
  fidelity. Field is usually `startFrame` or `referenceImages`.
- **video-to-video (v2v):** a source clip drives style/motion. Best for visual continuity.
- Many backends forbid mixing i2v and v2v in one call — check `capabilities`.

### B2. Script length → duration
Speaking pace ≈ **2.5 words/second** (~150 WPM). Round **up** to the nearest allowed
duration to leave breathing room.

| Script length | ~Duration |
|---------------|-----------|
| 1–8 words | 4–5s |
| 9–15 words | 6–8s |
| 16–25 words | 9–12s |
| 26–38 words | 13–16s |
| 39+ words | split into clips or use a longer-duration model |

Clamp to what the model actually offers (enum vs continuous) per `capabilities`.

### B3. Splitting long scripts
1. Tell the user the math (words ÷ 2.5 vs the model max).
2. Offer: **split** at sentence boundaries into ≤max clips, or **switch model**.
3. For continuity across clips, prefer chaining: clip 1 uses i2v (product still); clips
   2+ use v2v with the *previous clip* as reference (if the backend supports it).
4. Stitch with ffmpeg using **absolute paths**:
   ```bash
   printf "file '%s'\n" "$(pwd)/clip1.mp4" "$(pwd)/clip2.mp4" > /tmp/stitch.txt
   ffmpeg -y -f concat -safe 0 -i /tmp/stitch.txt -c copy stitched.mp4
   ```

### B4. Reference image hygiene
Before uploading any reference image:
1. If the longest side < **1024px**, upscale (Lanczos) so the longest side = **1080px**,
   preserving aspect ratio.
2. Convert to **RGB JPEG** (quality 90–95) to drop alpha channels.
Many backends reject small/RGBA images with a validation error — do this silently.

### B5. Polling pattern (pseudo)
```
job = submit(payload)
log_append({jobId: job.id, status: "pending", ...request})
loop:
    s = poll(job.id)
    if s.status in ("done","failed"): break
    sleep(few seconds, back off on rate limit)
log_update(job.id, {status: s.status, cost, genTime, outputUrl: s.outputUrl})
```

### B6. Logging
Append one line per generation to `logs/video-clone.jsonl`. Schema in
[logs/README.md](logs/README.md). Log request config + outcome; **never** log secrets or
full prompt text.

### B7. Cost discipline
Always present totals as **estimates**, cite the source (log entry date or adapter pricing
table), and wait for confirmation before firing. Warn if a known balance would be exceeded.
