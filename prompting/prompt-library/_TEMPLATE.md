# <Style Name>

**Use when:** <the kind of video this template produces>

**Backend rules:** comply with `adapters/active.md` (prompt-length window, forbidden words,
motion specificity). Every prompt = ONE max-length clip (see the backend capability matrix).

## What defines this style

<2–3 paragraphs: what makes this style distinctive and why it works. This is the "theory"
section — it helps the writer make good variable choices, not just fill blanks.>

## The structure (layers)

<Identify the building blocks of THIS style. Don't force a fixed layer count — if it's a
5-layer style, make it 5. Let the video drive it.>

## Layer-by-layer formula

### Layer N: <name>

<What this layer does and why it matters.>

**Pattern:**
```
<repeatable sentence structure with {{VARIABLES}}>
```

**Variables:**

| Variable | Options | Notes |
|----------|---------|-------|
| `{{VAR}}` | option a, option b, option c | <guidance> |

## Beat structure (single max-length clip)

<3-beat skeleton: hook → core → kicker. Which beats have dialogue vs silent action?
Max ~2–3 spoken lines total.>

## Multi-clip strategy (if the style needs more than one clip)

<How to split across 2–3 clips, each standing alone but together recreating the full style.>

## Tone & pacing guide

<How to calibrate energy, speech patterns, rhythm. Include a pacing-cue bank.>

## Technical specs

<Lighting, camera quality, audio character, the intentional "flaws" that make it authentic.>

## Complete template

```
<one copy-paste prompt block for ONE clip, all variables as {{PLACEHOLDERS}},
max 3 beats, max 2–3 dialogue lines>
```

## Example (different product/person/setting than any source)

<the template fully filled with concrete values, proving it generalizes>

## Adaptation checklist

- [ ] All layers covered.
- [ ] Dialogue fits the clip length (~2.5 words/sec).
- [ ] Reference-image slot used if the backend supports i2v.
- [ ] Complies with `adapters/active.md` prompting rules.
- [ ] Aspect ratio + duration valid for the chosen model.
