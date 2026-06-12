# Studio lookbook (polished, voiceover, multi-look)

**Use when:** a clean, produced spot — a product or model shown across several **looks /
angles** in a controlled studio, carried by a calm voiceover. Brand-forward, not scrappy.
The opposite of `ugc-selfie`.

**Backend rules:** comply with `adapters/active.md`. Every prompt = ONE max-length clip.
Has voiceover → the **dialogue gate applies**.

## What defines this style

Control and polish. Even lighting, a seamless backdrop, intentional wardrobe/prop choices,
and a measured voiceover that states benefits with confidence. The rhythm is a series of
clean **look changes** (angle, pose, or product variant) cut on the beat, each held just
long enough to register. It should feel like a brand campaign, not a phone clip.

## The structure (5 layers)

1. **Studio** — backdrop, surface, lighting setup.
2. **Subject** — the model or product and its styling.
3. **Look sequence** — the 2–3 distinct looks/angles shown in order.
4. **Voiceover** — the calm benefit-led script.
5. **Finish** — the closing brand beat / logo-clean hero.

## Layer-by-layer formula

### Layer 1: Studio
**Pattern:** `{{BACKDROP}} studio, {{LIGHTING}}, {{SURFACE}}.`
| Variable | Options |
|----------|---------|
| `{{BACKDROP}}` | seamless white, soft grey, warm beige, gradient color |
| `{{LIGHTING}}` | even soft key, large softbox, bright high-key, gentle directional |

### Layer 2: Subject
**Pattern:** `A {{SUBJECT}}, styled {{STYLING}}.` Keep it intentional and clean.

### Layer 3: Look sequence (per look)
**Pattern:** `{{CUT}} — {{ANGLE_OR_LOOK}}, {{POSE_OR_ARRANGEMENT}}.`
2–3 looks. Each is a clean change: new angle, new pose, or a product variant.

### Layer 4: Voiceover
One calm line per look at most, benefit-led: `"{{BENEFIT_LINE}}"`. Measured pace, no hype.

### Layer 5: Finish
**Pattern:** `Final beat: the {{PRODUCT}} centered, clean, {{CLOSING_LINE}}.`

## Beat structure (single clip)

| Beat | Content |
|------|---------|
| LOOK 1 | establish subject + first benefit line |
| LOOK 2 | angle/pose change + second benefit |
| FINISH | centered hero + closing line/CTA |

## Multi-clip strategy

A lookbook reel: one clip per look/colorway, each self-contained, unified by the same
backdrop, lighting, and VO voice. Stitch into a longer campaign cut.

## Tone & pacing guide

Calm, confident, unrushed. Cuts land on a steady beat. VO leaves a breath between lines.
Pacing cue: `the voice is warm and measured, pausing between benefits`.

## Complete template

```
{{BACKDROP}} studio, {{LIGHTING}}, {{SURFACE}}. A {{SUBJECT}}, styled {{STYLING}}.
[00:00] {{CUT}} — {{ANGLE_1}}, {{POSE_1}}. Voiceover: "{{BENEFIT_1}}"
[00:0X] {{CUT}} — {{ANGLE_2}}, {{POSE_2}}. Voiceover: "{{BENEFIT_2}}"
[00:0Y] Final beat: the {{PRODUCT}} centered and clean. Voiceover: "{{CLOSING_LINE}}"
The voice is warm and measured, pausing between benefits. Even, polished lighting throughout.
```

## Example (a linen shirt — not the source content)

```
Soft grey studio, even soft key light, seamless floor. A model in a relaxed linen shirt,
styled minimal and modern.
[00:00] Clean cut — three-quarter angle, hands in pockets. Voiceover: "Breathable from the
first wear."
[00:05] Clean cut — side profile, slow turn. Voiceover: "Cut to move with you, not against you."
[00:10] Final beat: the shirt centered on a hanger, clean. Voiceover: "Linen, done right.
Now in four shades."
The voice is warm and measured, pausing between benefits. Even, polished lighting throughout.
```

## Adaptation checklist

- [ ] 2–3 distinct looks/angles. [ ] One benefit line per look, calm VO.
- [ ] Dialogue gate passed. [ ] Consistent backdrop + lighting.
- [ ] Aspect ratio + duration valid. [ ] Complies with `adapters/active.md`.
