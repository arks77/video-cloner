# Premium reveal (no person, text-narrative)

**Use when:** a luxury / high-ticket product reveal with no person — a dark, moody space,
slow camera, and **on-screen text beats** that build a short narrative before the product
lands. Think watch / fragrance / supplement "drop" energy.

**Backend rules:** comply with `adapters/active.md`. Every prompt = ONE max-length clip.
Usually silent or single voiceover line — check the backend's forbidden-word list (many
reject "cinematic", "stunning", "8k"); describe the look concretely instead.

## What defines this style

Restraint and anticipation. Unlike `product-hero` (one elemental splash), the reveal is
**narrative**: 2–4 short text lines appear and fade, each raising tension, until the product
emerges from shadow on the final beat. The mood is dark, the motion is slow, the lighting
is a single sculpting source. Nothing is busy — empty space *is* the luxury signal.

## The structure (4 layers)

1. **Void & mood** — the dark/empty environment and its atmosphere.
2. **Text beats** — the 2–4 escalating on-screen lines (the narrative spine).
3. **Camera** — one slow, deliberate move toward the reveal.
4. **Reveal & light** — how the product emerges and how light sculpts it.

## Layer-by-layer formula

### Layer 1: Void & mood
**Pattern:** `A {{ENVIRONMENT}} in near-darkness, {{MOOD}}, with deep shadows and negative space.`
| Variable | Options |
|----------|---------|
| `{{ENVIRONMENT}}` | black seamless void, dark marble plinth, smoke-filled chamber, moonlit concrete room |
| `{{MOOD}}` | quiet and expensive, tense and anticipatory, cold and minimal |

### Layer 2: Text beats (the spine)
**Pattern (per beat):** `Text appears and fades: "{{LINE}}"`
2–4 short lines, each ≤6 words, escalating. The last line names the payoff or brand promise.

### Layer 3: Camera (pick ONE)
`slow push-in through shadow`, `low dolly rising to the product`, `drift around a silhouette`.

### Layer 4: Reveal & light
**Pattern:** `On the final beat the {{PRODUCT}} emerges from shadow as {{LIGHT_EVENT}}.`
| `{{LIGHT_EVENT}}` | a single key light blooms across it / a beam sweeps the label / a soft glow rises behind it |

## Beat structure (single clip)

| Beat | Content |
|------|---------|
| TENSION | void + text line 1–2, camera begins moving, product still hidden |
| BUILD | text line 3, shape of the product hinted in shadow |
| REVEAL | final text line, light blooms, product fully resolves |

## Multi-clip strategy

Teaser series: clip 1 = pure text + shadow (no product), clip 2 = silhouette tease,
clip 3 = full reveal. Keep the void, palette, and type rhythm identical across clips.

## Tone & pacing guide

Slow. Let each text line breathe a full beat before the next. No quick cuts. If a voiceover
is used, one low, unhurried line only — placed on the reveal.

## Complete template

```
A {{ENVIRONMENT}} in near-darkness, {{MOOD}}, deep shadows and negative space.
[00:00] Text appears and fades: "{{LINE_1}}"
[00:0X] {{CAMERA_MOVE}}. Text appears and fades: "{{LINE_2}}"
[00:0Y] The shape of {{PRODUCT}} is hinted in shadow. Text: "{{LINE_3}}"
[00:0Z] The {{PRODUCT}} emerges from shadow as {{LIGHT_EVENT}}, label crisp and readable.
A single sculpting key light, no clutter. The product remains visually unchanged.
```

## Example (a matte-black watch — not the source content)

```
A black seamless void in near-darkness, quiet and expensive, deep shadows and negative space.
[00:00] Text appears and fades: "Time is the only currency."
[00:04] A slow push-in through shadow. Text appears and fades: "Spend it well."
[00:08] The shape of a watch is hinted in shadow. Text: "Engineered to outlast you."
[00:12] The matte-black watch emerges from shadow as a single key light blooms across the
dial, hands and index crisp. One sculpting key light, no clutter. The watch remains
visually unchanged.
```

## Adaptation checklist

- [ ] 2–4 escalating text lines, last names the payoff. [ ] One slow camera move.
- [ ] Product hidden until the final beat. [ ] No forbidden words (check `active.md`).
- [ ] Aspect ratio + duration valid.
