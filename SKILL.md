---
name: video-clone
description: >
  Clone, reverse-engineer, or generate video ads through ANY video-generation backend.
  Backend-agnostic: all API specifics live behind an adapter contract (adapters/active.md).
  Use when the user wants to "clone this video ad", "make this ad for my product",
  "turn this video into a template", "analyze this video style", or generate a video ad
  from a brief. Routes to clone-ad (generate a new video), analyze-video (build a reusable
  template), or direct generation via the prompt library.
---

# video-clone — router

A portable hub for cloning and generating video ads. This file routes the request and
enforces the safety/quality gates. The concrete API lives in **`adapters/active.md`**;
the contract that file must satisfy lives in **[reference.md](reference.md)**.

## Backend resolution (do this first)

1. Look for **`adapters/active.md`**. That is the live backend definition.
2. If it does not exist, tell the user: *"No backend is configured yet. Copy
   `adapters/_ADAPTER.template.md` to `adapters/active.md` and fill it in (see the worked
   example in `adapters/example-arcads-seedance.md`), or tell me which video API to use
   and I'll draft it."* **Do not invent endpoints.**
3. Read `adapters/active.md` fully before any call. It defines: auth, upload, submit,
   poll, and the backend's capability matrix (durations, aspect ratios, i2v/v2v/t2v,
   audio, pricing, known gotchas).

Whenever this file says `submit(...)`, `poll(...)`, `upload(...)`, or "the backend's
max duration", resolve it against `adapters/active.md`.

## Read order

1. Repo **`MASTER_CONTEXT.md`** / project brand file, if present (voice, defaults, banned words).
2. **`adapters/active.md`** — the live backend.
3. **[reference.md](reference.md)** — the adapter contract + generic video mechanics.
4. **[prompting/guide.md](prompting/guide.md)**, then the right `prompting/prompt-library/*.md`.

## Decision tree: which flow?

| User goal | Go to |
|-----------|-------|
| "Clone this ad for my product" — input video + product → **a generated video** | [prompting/clone-ad/SKILL.md](prompting/clone-ad/SKILL.md) |
| "Turn this video into a template / analyze this style" → **a reusable `.md` template** | [prompting/analyze-video/SKILL.md](prompting/analyze-video/SKILL.md) |
| Generate from a brief — pick the matching **style** from the prompt library (below) | [prompting/prompt-library/](prompting/prompt-library/) |
| A style not covered yet | Build one with [prompting/prompt-library/_TEMPLATE.md](prompting/prompt-library/_TEMPLATE.md) |

### Prompt library — pick a style

| Style | When | File |
|-------|------|------|
| **UGC selfie** | phone-filmed review/testimonial, one person to camera | [ugc-selfie.md](prompting/prompt-library/ugc-selfie.md) |
| **Unboxing hype** | high-energy package → reveal → reaction | [unboxing-hype.md](prompting/prompt-library/unboxing-hype.md) |
| **Problem → solution** | before/after direct-response arc | [problem-solution.md](prompting/prompt-library/problem-solution.md) |
| **Testimonial / authority** | composed founder/expert talking head, trust-led | [testimonial-authority.md](prompting/prompt-library/testimonial-authority.md) |
| **Feature walkthrough** | fast-paced demo hitting feature after feature | [feature-walkthrough.md](prompting/prompt-library/feature-walkthrough.md) |
| **Studio lookbook** | polished multi-look spot with calm voiceover | [studio-lookbook.md](prompting/prompt-library/studio-lookbook.md) |
| **Product hero** | no person, elemental reveal (splash/light/orbit) | [product-hero.md](prompting/prompt-library/product-hero.md) |
| **Premium reveal** | no person, dark-void text-narrative luxury drop | [premium-reveal.md](prompting/prompt-library/premium-reveal.md) |

If the user's request straddles two, pick the closest and note the blend; if none fit,
build a new one from `_TEMPLATE.md`.

**clone-ad vs analyze-video:** clone-ad's output is a finished video for one product;
analyze-video's output is a template you can reuse for many products. If the user wants
*both* "make me this video now" and "and keep the recipe", run analyze-video first, then
feed the template into clone-ad.

## Creative layer (mandatory)

Before composing any prompt, **read the matching `prompting/prompt-library/*.md`** and
align with the backend's prompting rules in `adapters/active.md` (every backend has its
own prompt-length sweet spot, forbidden words, and motion conventions — honor them).
Write **one coherent paragraph**, not keyword soup. Merge slot values from the user and
from `MASTER_CONTEXT.md` (project memory wins on conflicts).

## Gates before generating (all mandatory)

These are backend-independent. Run them in order; never skip ahead.

### 1. Session organization (if the backend supports it)
If `adapters/active.md` defines a project/folder concept, create or reuse a dated
container (e.g. `video-clone — YYYY-MM-DD`) so outputs are findable. If not, just save
locally under `outputs/`.

### 2. Generation count
Ask how many variations the user wants (default 1). N variations = N separate `submit`
calls with the identical payload, fired in parallel, polled concurrently. Present as a
numbered list for comparison.

### 3. Credit / cost estimate
Cost is **always an estimate** — most backends have no billing endpoint. Source in
priority order:
1. `logs/video-clone.jsonl` — past `costCharged` for the same model + similar config.
2. The pricing table in `adapters/active.md`.
3. Ask the user, then write the answer into `adapters/active.md`.

Present the breakdown, cite the source, label it an estimate, and **wait for explicit
confirmation**. Never invent numbers.

### 4. Dialogue confirmation gate (if anyone speaks)
For any video with spoken dialogue, before cost/generation:
- Extract the dialogue lines into a dedicated **numbered block**, separate from the
  visual description, with beat labels and silent beats marked `(silent beat — no dialogue)`.
- Count spoken words, compare against target duration (~2.5 words/sec), flag if it fits.
- Ask for approval explicitly: `Approve this dialogue? (yes / edit / rewrite)`.
- **Never** infer approval from an earlier confirmation. This is its own gate.

```
📝 Dialogue script (please confirm before I generate)

  1. [HOOK]    "opening line"
  2. [SHOW]    "feature call-out for the product"
  3. [DEMO]    (silent beat — physical demonstration)
  4. [VERDICT] "closing line / CTA"

Total spoken words: ~N  |  Target duration: Xs  |  Fits at natural pace: ✅/❌

Approve this dialogue? (yes / edit / rewrite)
```

### 5. Duration from word count
Pick `duration` from the script length using ~2.5 words/sec, rounded up to the nearest
value the backend allows (see the capability matrix in `adapters/active.md`). If the
script exceeds the backend's max clip length, offer to **split into multiple clips** at
sentence boundaries (and stitch later with ffmpeg) or switch to a longer-duration model.

## Execution checklist (agent)

1. Resolve backend (`adapters/active.md`); confirm auth works.
2. Session container (gate 1).
3. If video has speech: get the exact script, run the **dialogue gate** (gate 4).
4. Ask **variation count** (gate 2).
5. Compute + show **cost estimate**, get confirmation (gate 3).
6. Check a local `references/` folder for product/person/style images; `upload(...)` any
   refs the payload needs. Auto-upscale tiny images (longest side < 1024px → 1080px,
   RGB JPEG) before upload.
7. Compose the payload per `adapters/active.md` + the chosen prompt-library file. Respect
   the backend's i2v/v2v/t2v rules (many backends make reference-image and reference-video
   modes mutually exclusive — check the adapter).
8. `submit(...)` N times. **Immediately append a log entry** to `logs/video-clone.jsonl`
   (model, duration, params, ref counts, promptWordCount, jobId). Never log secrets or
   full prompt text.
9. `poll(...)` all jobs until `done` or `failed`. **Update the log entry** with status,
   cost, generation time, and output URL.
10. **QA** any still frames / thumbnails for obvious defects; for the video, spot-check the
    thumbnail. Regenerate with a corrected prompt if clearly broken (cap retries; each
    retry is billed).
11. Save outputs under `outputs/<descriptive-subfolder>/`, open the folder for the user
    (`open` / `xdg-open` / `explorer`), and present watch/download URLs.
12. If the script was split, offer to stitch with ffmpeg and provide both the stitched
    file and the individual clips.

## Errors

Map the backend's error codes in `adapters/active.md`. Generic guidance:
- **Auth (401/403):** fix the key per the adapter's auth section.
- **Validation/moderation:** tighten the prompt, remove flagged content, check enums
  (aspect ratio, duration). Do **not** blindly resubmit the identical payload.
- **Server (5xx):** retry once after a short wait; if it persists, stop and report.
- If a backend bills before a content check and the job later fails, treat credits as
  spent — note it for the user. Record such quirks in the adapter's "gotchas" section.

## Supporting files

- [reference.md](reference.md) — the adapter contract + generic mechanics.
- [adapters/_ADAPTER.template.md](adapters/_ADAPTER.template.md) — copy to `active.md`.
- [adapters/example-arcads-seedance.md](adapters/example-arcads-seedance.md) — worked example.
- [prompting/guide.md](prompting/guide.md) — brief → prompt.
- [prompting/clone-ad/SKILL.md](prompting/clone-ad/SKILL.md) — clone → generate.
- [prompting/analyze-video/SKILL.md](prompting/analyze-video/SKILL.md) — deconstruct → template.
- [logs/README.md](logs/README.md) — log schema.
