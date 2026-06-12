# Unboxing hype (high-energy reaction)

**Use when:** a fast, excited unboxing — package → reveal → genuine reaction. A distinct,
higher-energy cousin of `ugc-selfie`: the product arriving and being opened *is* the story.

**Backend rules:** comply with `adapters/active.md`. Every prompt = ONE max-length clip.
Has speech → the **dialogue gate applies**; lines are short, exclamatory, overlapping energy.

## What defines this style

Anticipation → payoff → eruption. The hook is the sealed package and barely-contained
excitement; the core is the physical reveal (tear, lift, first touch); the kicker is an
unfiltered reaction. Handheld, slightly chaotic, fast. Authenticity comes from the reaction
being *bigger than the script* — gasps, "wait—", a laugh. The product details get noticed
*through* the excitement, not listed.

## The structure (5 layers)

1. **Format header** — duration, "UGC unboxing", device, lighting, angle.
2. **Person & energy** — who, and their barely-contained anticipation.
3. **The package** — what just arrived, sealed, teased to camera.
4. **Reveal beats** — tear → lift → first-touch, framing tight on hands/product.
5. **Reaction & flaws** — the unfiltered verdict + handheld imperfections.

## Layer-by-layer formula

### Layer 1: Format header
**Pattern:** `{{DURATION}} UGC unboxing, filmed on a smartphone, {{LIGHTING}}, {{ANGLE}}.`

### Layer 2: Person & energy
**Pattern:** `A {{DESCRIPTOR}}, {{ANTICIPATION_CUE}}.`
| `{{ANTICIPATION_CUE}}` | grinning before they start, talking fast, hands already on the box |

### Layer 3: The package
**Pattern:** `Holds up {{SEALED_PACKAGE}} to camera: "{{TEASE_LINE}}"`

### Layer 4: Reveal beats (per beat)
`{{TRANSITION}} — tight on hands, {{REVEAL_ACTION}}.` (tear / lift lid / pull product out)

### Layer 5: Reaction & flaws
Unfiltered: `"{{REACTION_LINE}}"`. Flaws: handheld shake, a whip-pan, mic peaking on a gasp.

## Beat structure (single clip)

| Beat | Content |
|------|---------|
| HOOK | sealed package up to camera, tease line, big energy |
| REVEAL | tight on hands tearing/opening (can be near-silent — let the moment land) |
| REACTION | first touch + unfiltered verdict + soft CTA |

## Multi-clip strategy

Series: clip 1 = "it's here" anticipation, clip 2 = the reveal, clip 3 = trying/using it +
verdict. Same person, same room, same package continuity (use an image ref if i2v supported).

## Tone & pacing guide

Fast, loud, genuine. One beat may be near-silent (the reveal) to let it breathe before the
reaction erupts. Pacing cue: `talks fast and overlaps themselves, a beat of silence on the
reveal, then erupts`.

## Complete template

```
{{DURATION}} UGC unboxing, filmed on a smartphone, {{LIGHTING}}, {{ANGLE}}.
A {{DESCRIPTOR}}, {{ANTICIPATION_CUE}}.
[00:00] HOOK — holds up {{SEALED_PACKAGE}} to camera: "{{TEASE_LINE}}"
[00:0X] REVEAL — tight on hands, {{REVEAL_ACTION}}. (let the moment land)
[00:0Y] REACTION — first touch of {{PRODUCT}}: "{{REACTION_LINE}}" {{CTA}}
Talks fast and overlaps themselves, a beat of silence on the reveal, then erupts.
Handheld with {{TECH_FLAW}}.
```

## Example (limited sneakers — not the source content)

```
12 seconds UGC unboxing, filmed on a smartphone, bright window light, arm's-length selfie.
A hyped guy in a hoodie, grinning before he starts, hands already on the box.
[00:00] HOOK — holds up a sealed shoebox to camera: "Bro. BRO. These finally came."
[00:04] REVEAL — tight on hands, lifts the lid and pulls back the tissue. (let it land)
[00:08] REACTION — first touch of the suede: "Okay the stitching is insane— I'm wearing these
tomorrow." Link's in bio.
Talks fast and overlaps himself, a beat of silence on the reveal, then erupts. Handheld with
a small whip-pan and mic peaking on the gasp.
```

## Adaptation checklist

- [ ] Sealed-package hook. [ ] One near-silent reveal beat. [ ] Unfiltered reaction line.
- [ ] Dialogue gate passed. [ ] Handheld flaws present.
- [ ] Aspect ratio + duration valid. [ ] Complies with `adapters/active.md`.
