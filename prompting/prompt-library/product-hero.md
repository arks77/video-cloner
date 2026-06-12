# Product hero (no person, generic)

**Use when:** a premium, no-person product showcase — the product alone, driven by camera
motion, lighting, and elemental effects (splash, mist, light sweep). Great for reveals.

**Backend rules:** comply with `adapters/active.md`. Every prompt = ONE max-length clip.
Usually silent (no dialogue gate) — optional voiceover only if the backend speaks.

## What defines this style

No face, no hands holding it casually — the **product is the hero**, lit and moved like a
jewelry ad. The feel comes from (1) a **controlled environment** (dark void, seamless
backdrop, or a single textured surface), (2) **deliberate camera motion** (slow push-in,
orbit, rack focus), and (3) **one elemental accent** (a water splash, a drift of mist, a
sweep of light) timed to a beat. Restraint is the whole point — one hero move, not five.

## The structure (4 layers)

1. **Environment** — backdrop, surface, mood.
2. **Product placement** — how it sits/floats, orientation to camera.
3. **Camera move** — the single signature motion.
4. **Elemental accent + lighting** — the one effect and how light behaves.

## Layer-by-layer formula

### Layer 1: Environment
**Pattern:** `The {{PRODUCT}} on a {{SURFACE}} in a {{ENVIRONMENT}}, {{MOOD}}.`
| Variable | Options |
|----------|---------|
| `{{SURFACE}}` | wet black stone, brushed metal, seamless white sweep, raw concrete |
| `{{ENVIRONMENT}}` | dark void, softly lit studio, foggy backdrop |

### Layer 2: Product placement
**Pattern:** `It {{POSE}}, label facing camera, {{ORIENTATION}}.`
Keep the label readable; specify "remains visually unchanged" if using a reference image.

### Layer 3: Camera move (pick ONE)
`slow push-in`, `360° orbit`, `top-down descend`, `rack focus from background to label`.

### Layer 4: Elemental accent + lighting
One accent only: `a single water splash crowns the cap`, `thin mist drifts past`,
`a sweep of light travels across the label`. Lighting: directional key + subtle rim.

## Beat structure (single clip)

| Beat | Content |
|------|---------|
| ESTABLISH | product in environment, camera begins its move |
| ACCENT | the elemental effect hits at the midpoint |
| RESOLVE | camera settles on the hero shot, label crisp |

## Multi-clip strategy

For a fuller reveal, split: clip 1 = silhouette/teaser in shadow, clip 2 = the accent
reveal, clip 3 = the clean hero beauty shot. Keep environment + lighting consistent.

## Complete template

```
The {{PRODUCT}} on a {{SURFACE}} in a {{ENVIRONMENT}}, {{MOOD}}. It {{POSE}}, label facing
camera. {{CAMERA_MOVE}} over the full clip. At the midpoint, {{ELEMENTAL_ACCENT}}.
{{LIGHTING}} with a subtle rim light separating the product from the background. The product
remains visually unchanged throughout. {{OPTIONAL_VOICEOVER}}
```

## Example (a glass serum bottle — not the source content)

```
The amber glass serum bottle on wet black stone in a dark void, calm and premium. It stands
upright, dropper cap on, label facing camera. A slow push-in over the full clip. At the
midpoint, a single droplet falls and rings the base in a clean ripple. Directional key light
from the upper left with a subtle rim light separating the bottle from the background. The
product remains visually unchanged throughout.
```

## Adaptation checklist

- [ ] Exactly one camera move. [ ] Exactly one elemental accent.
- [ ] Label readable / "remains unchanged" anchor present.
- [ ] Aspect ratio + duration valid. [ ] Complies with `adapters/active.md`.
