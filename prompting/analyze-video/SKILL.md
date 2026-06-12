---
name: analyze-video
description: >
  Reverse-engineer a reference video into a reusable prompting template. Output is a new
  markdown template (like the prompt-library files) capturing the video's structure,
  pacing, camera work, edit style, and tone so it can be regenerated with any product,
  person, or setting through the configured backend. Use for "turn this into a template",
  "analyze this style", "deconstruct this video", "I want to make videos like this".
---

# Analyze video → reusable template

Someone found a video style they love. Deconstruct it into a **reusable template** — a
formula they can plug any product/person/setting into and get that style back.

Sibling skill: [clone-ad](../clone-ad/SKILL.md) generates one finished video instead.

Output is a new file in [`../prompt-library/`](../prompt-library/) built from
[`_TEMPLATE.md`](../prompt-library/_TEMPLATE.md). It must be self-contained — usable
without ever seeing the original video.

**Clip-length constraint:** the backend has a max clip length (see `capabilities` in
`adapters/active.md` — often 8–15s). The reference may be longer. Design the template for
a single max-length clip and include a multi-clip strategy for longer styles.

## Dependencies

- **ffmpeg/ffprobe** — frame extraction (Step 1). `brew install ffmpeg`.
- **whisper** — optional transcription (Step 2). `pip3 install openai-whisper`. Without it,
  ask the user for the dialogue.

## Step 1 — Extract frames + audio

```bash
bash "<skill-path>/prompting/analyze-video/scripts/extract-frames.sh" \
  "<video>" "/tmp/video-analysis" <num_frames>
```
Frame count: <10s→8, 10–20s→12, 20–30s→16, >30s→20. Read `metadata.txt`.

## Step 2 — Transcribe

```bash
whisper /tmp/video-analysis/audio.wav --model base --output_format txt --output_dir /tmp/video-analysis
```
The transcript reveals pacing, speech rhythm, filler usage, and dialogue↔action interleave.

## Step 3 — Study existing templates

Read [`../prompt-library/_TEMPLATE.md`](../prompt-library/_TEMPLATE.md) and an existing
example ([ugc-selfie.md](../prompt-library/ugc-selfie.md) is the richest) to match the
expected depth: **layers**, **patterns with `{{VARIABLES}}`**, **option banks**, **rules**,
and a **complete filled example**.

## Step 4 — Analyze for transferable patterns

Read all frames. For each dimension ask: *"Is this specific to THIS video (person, product,
setting) or is it THE STYLE (approach, structure, feel)?"* Only the style enters the template;
specifics become variables.

- **Structure & pacing** — beats, arc, rhythm, which 2–3 beats are essential.
- **Camera & framing** — primary POV, how framing shifts, signature move.
- **Edit style** — cuts, transitions, recurring motifs.
- **Dialogue & script** — hook format, structure, defining speech patterns.
- **Tone & energy** — 3–4 emotion words, energy arc, viewer relationship.
- **Lighting & technical** — lighting approach, intentional flaws, audio character.
- **What makes it DIFFERENT** — the 2–3 traits that distinguish it from generic UGC/product video.

### Max-clip compression plan
- **Minimum viable version:** which beats/elements are essential vs nice-to-have?
- **Multi-clip?** narrative arcs / feature rundowns need 2–3 clips; a single vibe may fit one.
- **How many spoken lines fit?** ~2–3 short sentences per max clip; count source lines.
- **Beat skeleton:** compress to hook → core → kicker.

## Step 5 — Build the template

Create a new markdown file from [`_TEMPLATE.md`](../prompt-library/_TEMPLATE.md). Key rules:
- Every generated prompt is **one max-length clip** — include a multi-clip strategy if the
  style needs more.
- Variables are **curated choices**, not open blanks — give an option bank per variable.
- Encode the **rules** (hook must be a question, exactly one silent beat, etc.), not just structure.
- The **example must use different content** than the source (proves it generalizes).
- Include a reference-image slot if the backend supports i2v.
- Dialogue must fit the clip length (~30–40 spoken words ceiling for ~15s).
- Comply with the backend's prompting rules in `adapters/active.md` (length, forbidden words).

## Step 6 — Save & present

1. Save to `../prompt-library/<style-name>.md`.
2. Summarize: the style identified, its layers, what makes it distinct, the file path.
3. Offer: *"Want me to generate a test using a different product to verify it works?"*
   If yes, generate for different content than the source (validates reusability) — this
   hands off to [clone-ad](../clone-ad/SKILL.md)'s generation steps via the active backend.
