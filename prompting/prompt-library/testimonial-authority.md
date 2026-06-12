# Testimonial / authority (talking head)

**Use when:** a composed, credible person speaks directly to camera — a founder, an expert,
or a confident customer making the case. Calmer and more authoritative than `ugc-selfie`;
trust is the product.

**Backend rules:** comply with `adapters/active.md`. Every prompt = ONE max-length clip.
Speech-driven → the **dialogue gate applies**.

## What defines this style

Composure and credibility. One person, framed cleanly, looking down the lens, speaking in
complete, considered sentences — not scrappy reactions. The setting signals legitimacy (an
office, a clean home, a workspace that fits their authority). The persuasion is a small,
honest argument: a claim, a reason, a proof point. Eye contact and steadiness do the work;
no jump-cut chaos. It should feel like advice from someone who knows.

## The structure (4 layers)

1. **Person & credibility** — who they are and the authority cue.
2. **Setting** — the legitimizing environment.
3. **Argument beats** — claim → reason → proof, in measured lines.
4. **Close** — a calm, direct recommendation / CTA.

## Layer-by-layer formula

### Layer 1: Person & credibility
**Pattern:** `A {{DESCRIPTOR}} ({{AUTHORITY_CUE}}), looking directly into the lens.`
| `{{AUTHORITY_CUE}}` | the founder, a dermatologist, a 10-year user, a coach |

### Layer 2: Setting
**Pattern:** `In {{LEGITIMIZING_SETTING}}, {{LIGHTING}}.`
| `{{LEGITIMIZING_SETTING}}` | a clean modern office, a bright kitchen, a workshop, a studio |

### Layer 3: Argument beats
**Pattern (per beat):** `{{FRAMING}}: "{{LINE}}"` — claim, then reason, then a proof point.
Complete sentences, steady delivery, one idea per line.

### Layer 4: Close
**Pattern:** `Direct to camera: "{{RECOMMENDATION_OR_CTA}}"`

## Beat structure (single clip)

| Beat | Content |
|------|---------|
| CLAIM | who they are + the headline claim |
| REASON+PROOF | why it's true + one concrete proof point |
| CLOSE | calm recommendation / CTA |

## Multi-clip strategy

A testimonial set: one clip per speaker or per claim, unified by consistent framing and
lighting, intercut into a longer trust reel. Keep each speaker's setting stable across their
clips.

## Tone & pacing guide

Measured, warm, certain. No filler, no rush — pauses read as confidence, not hesitation.
Pacing cue: `speaks in calm, complete sentences with a steady, confident pace`.

## Complete template

```
A {{DESCRIPTOR}} ({{AUTHORITY_CUE}}), looking directly into the lens, in {{SETTING}}, {{LIGHTING}}.
[00:00] {{FRAMING}}: "{{CLAIM_LINE}}"
[00:0X] {{FRAMING}}: "{{REASON_AND_PROOF_LINE}}"
[00:0Y] Direct to camera: "{{CTA_LINE}}"
Speaks in calm, complete sentences with a steady, confident pace. Clean, even lighting; the
{{PRODUCT}} visible but not waved around.
```

## Example (a skincare founder — not the source content)

```
A woman in her 40s (the founder), looking directly into the lens, in a clean bright lab-style
office, soft even lighting.
[00:00] Medium close-up: "I started this because every 'gentle' cleanser I tried still left
my skin tight."
[00:05] Same framing, holds the bottle calmly: "So we built ours at a pH your skin actually
likes — we tested it for two years before launch."
[00:11] Direct to camera: "If your skin feels tight after washing, try it for a week. That's
all it takes."
Speaks in calm, complete sentences with a steady, confident pace. Clean even lighting; the
bottle visible but not waved around.
```

## Adaptation checklist

- [ ] Clear authority cue. [ ] Argument = claim → reason → proof. [ ] Complete sentences.
- [ ] Legitimizing setting. [ ] Dialogue gate passed.
- [ ] Aspect ratio + duration valid. [ ] Complies with `adapters/active.md`.
