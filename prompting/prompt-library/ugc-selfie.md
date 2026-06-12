# UGC selfie-style (generic, backend-agnostic)

**Use when:** authentic phone-filmed product review / testimonial — one person talking to
camera, reacting to a product. The workhorse format for social video ads.

**Backend rules:** comply with `adapters/active.md`. Every prompt = ONE max-length clip.

## What defines this style

It must read as *real*, not produced. The power is in imperfection: a handheld phone, an
ordinary room, a person who sounds like they're texting a friend — not reading a script.
Three things sell it: (1) a **pattern-interrupt hook** in the first second, (2) **specific
sensory detail** about the product instead of generic praise, and (3) **natural speech
rhythm** with pauses, filler words, and a real reaction beat.

## The structure (5 layers)

1. **Format header** — duration, "UGC/selfie", device, lighting, angle.
2. **Person** — appearance, skin texture, clothing (real, not glam).
3. **Setting** — a lived-in space with one or two specific clutter details.
4. **Beats + dialogue** — jump-cut scenes, each with framing + action + a spoken line.
5. **Tone & flaws** — pacing cue + intentional technical imperfections.

## Layer-by-layer formula

### Layer 1: Format header
**Pattern:**
```
{{DURATION}} UGC selfie-style product review, filmed on a smartphone, {{LIGHTING}}, {{ANGLE}}.
```
| Variable | Options |
|----------|---------|
| `{{LIGHTING}}` | natural window light, overhead kitchen light, soft ring light, golden-hour balcony light |
| `{{ANGLE}}` | arm's-length selfie, slightly-above selfie, propped-phone medium shot |

### Layer 2: Person
**Pattern:** `A {{AGE}} {{DESCRIPTOR}} with {{REAL_SKIN_DETAIL}}, wearing {{CASUAL_OUTFIT}}.`
Keep it real: visible pores, a stray hair, a plain t-shirt. Avoid "flawless", "model".

### Layer 3: Setting
**Pattern:** `In a {{ROOM}} with {{ONE_OR_TWO_CLUTTER_DETAILS}} visible behind them.`
Specific clutter (a coffee mug, an unmade bed corner) sells authenticity.

### Layer 4: Beats + dialogue
**Pattern (per beat):** `{{TRANSITION}} — {{FRAMING}}, {{ACTION}}: "{{DIALOGUE}}"`
Silent beat: `{{TRANSITION}} — {{FRAMING}}, {{ACTION}}.` (no dialogue)

### Layer 5: Tone & flaws
Always include **one explicit pacing cue** (this is what stops robotic delivery):
`pauses between thoughts`, `leaves a beat after each sentence`, `relaxed unhurried pace`,
`takes a natural breath mid-sentence`. Plus flaws: slight mic clipping, minor focus hunt,
small handheld sway.

## Beat structure (single clip)

| Beat | Content |
|------|---------|
| HOOK | reaction or question, tight on face: grab attention in <2s |
| SHOW/DEMO | tilt product to camera or use it; one specific sensory call-out |
| VERDICT | back to face, soft or direct CTA |

## Multi-clip strategy

For a longer arc (problem → discovery → result), split into 2–3 clips: clip 1 = problem +
hook, clip 2 = product in use, clip 3 = result + CTA. Anchor the same person, room, and
product across clips (use an image reference if the backend supports i2v).

## Complete template

```
{{DURATION}} UGC selfie-style product review, filmed on a smartphone, {{LIGHTING}}, {{ANGLE}}.
A {{AGE}} {{DESCRIPTOR}} with {{REAL_SKIN_DETAIL}}, wearing {{CASUAL_OUTFIT}}, in a {{ROOM}}
with {{CLUTTER}} behind them.
[00:00] HOOK — tight on face, {{HOOK_ACTION}}: "{{HOOK_LINE}}"
[00:0X] SHOW — {{FRAMING}}, holds {{PRODUCT}} to camera: "{{FEATURE_LINE}}"
[00:0Y] DEMO — macro on {{PRODUCT_DETAIL}}, {{USE_ACTION}}. (silent beat)
[00:0Z] VERDICT — back to face: "{{CTA_LINE}}"
She speaks at a {{PACING_CUE}}. Phone-quality footage with {{TECH_FLAW}}.
```

## Example (protein bar, kitchen — not the source content)

```
12 seconds UGC selfie-style product review, filmed on a smartphone, natural window light,
arm's-length selfie. A late-20s guy with stubble and visible pores, wearing a grey hoodie,
in a small kitchen with a coffee mug and an open laptop behind him.
[00:00] HOOK — tight on face, eyebrows up: "Okay I did not expect a protein bar to taste like this."
[00:03] SHOW — medium, holds the bar to camera: "Twenty grams, no chalky aftertaste, that's the part."
[00:07] DEMO — macro on a bite, chewing, small nod. (silent beat)
[00:10] VERDICT — back to face: "Trying the whole box this week. Link's down there."
He speaks at a relaxed, unhurried pace, leaving a beat after each sentence. Phone-quality
footage with slight mic clipping and a small focus hunt.
```

## Adaptation checklist

- [ ] Hook lands in <2s. [ ] One specific sensory detail (not generic praise).
- [ ] Exactly one explicit pacing cue. [ ] One silent demo beat.
- [ ] Dialogue ≤ ~2.5 words/sec × duration. [ ] Complies with `adapters/active.md`.
