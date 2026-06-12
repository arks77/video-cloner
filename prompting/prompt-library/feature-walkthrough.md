# Feature walkthrough (fast-paced demo)

**Use when:** a punchy demo that hits **feature after feature** in quick cuts — a physical
product being used, or an app/UI in action. High information density, energetic pace, made
to answer "what does it actually do?"

**Backend rules:** comply with `adapters/active.md`. Every prompt = ONE max-length clip.
Often has a fast VO → if so, the **dialogue gate applies**; keep lines very short.

## What defines this style

Momentum. Each beat = one feature, shown not just told: a hand triggers it, the UI responds,
the result is visible. Cuts are quick and rhythmic; text labels or a brisk VO name each
feature. The viewer should feel the product is *capable* because they saw three things work
in ten seconds. Density is the style — but each beat must still read clearly.

## The structure (4 layers)

1. **Context** — what the product is and the using environment, set in one line.
2. **Feature beats** — 3 quick demos, each: action → response → result.
3. **Labels/VO** — the short tag naming each feature.
4. **Payoff** — the one-line "so you can ___" outcome + CTA.

## Layer-by-layer formula

### Layer 1: Context
**Pattern:** `{{PRODUCT}} in use, {{ENVIRONMENT}}, {{DEVICE_OR_HANDS}}.`

### Layer 2: Feature beats (per feature)
**Pattern:** `{{QUICK_CUT}} — {{ACTION}} → {{VISIBLE_RESPONSE}}. Label: "{{FEATURE_NAME}}"`
Keep three. Each must show a real cause→effect, not a static glamour shot.

### Layer 3: Labels / VO
Tags ≤4 words: `"One-tap export"`, `"Works offline"`. If VO, same brevity, fast delivery.

### Layer 4: Payoff
**Pattern:** `Closing: "{{OUTCOME_LINE}}" — {{CTA}}.`

## Beat structure (single clip)

| Beat | Content |
|------|---------|
| FEATURE 1 | action → response, label |
| FEATURE 2 | action → response, label |
| FEATURE 3 | action → response, label |
| PAYOFF | outcome line + CTA (can overlap feature 3's tail) |

## Multi-clip strategy

For a deeper product, one clip per feature cluster (e.g. "capture", "edit", "share"), each
a mini-walkthrough, unified by the same UI/device look and VO voice. Stitch into a full demo.

## Tone & pacing guide

Fast but legible — hold each feature just long enough to register the result. VO is brisk
and upbeat. Pacing cue: `energetic, clipped delivery — one breath per feature`.

## Complete template

```
{{PRODUCT}} in use, {{ENVIRONMENT}}, {{DEVICE_OR_HANDS}}.
[00:00] {{QUICK_CUT}} — {{ACTION_1}} → {{RESPONSE_1}}. Label: "{{FEATURE_1}}"
[00:0X] {{QUICK_CUT}} — {{ACTION_2}} → {{RESPONSE_2}}. Label: "{{FEATURE_2}}"
[00:0Y] {{QUICK_CUT}} — {{ACTION_3}} → {{RESPONSE_3}}. Label: "{{FEATURE_3}}"
[00:0Z] Closing: "{{OUTCOME_LINE}}" — {{CTA}}.
Energetic, clipped pace; each feature held just long enough to read the result.
```

## Example (a budgeting app — not the source content)

```
A budgeting app in use on a phone, at a kitchen table, thumb driving the screen.
[00:00] Quick cut — thumb snaps a receipt → the expense auto-categorizes. Label: "Scan & sort"
[00:03] Quick cut — taps a goal → a progress ring fills. Label: "Goals that move"
[00:06] Quick cut — swipes to a chart → spending by category animates in. Label: "See it clearly"
[00:09] Closing: "Know where it all goes." — Download free.
Energetic, clipped pace; each feature held just long enough to read the result.
```

## Adaptation checklist

- [ ] Exactly 3 feature beats, each action→response→result. [ ] Labels ≤4 words.
- [ ] Payoff names a concrete outcome + CTA. [ ] Legible despite speed.
- [ ] Dialogue gate passed if VO. [ ] Complies with `adapters/active.md`.
