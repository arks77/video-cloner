# Creative brief playbook

Use this **before** opening a `prompt-library/*.md` file or composing any prompt.

## 1. Capture marketing intent (ask the user)

- **Audience:** who is this for? (one sentence)
- **Job to be done:** what should the viewer feel or do after watching?
- **Offer / proof:** product name, one concrete benefit, optional social proof.
- **Hook:** the first 1–2 seconds — pattern interrupt, curiosity, relatable moment.
- **CTA:** exact words if spoken or on-screen.
- **Constraints:** length, aspect ratio, banned topics, brand words to avoid.

## 2. Turn intent into ONE coherent prompt

- Prefer **one paragraph** of clear direction over a bag of keywords.
- Name **subject, setting, camera/motion, lighting, style, audio mood** (when the backend
  supports audio).
- Translate vague adjectives ("premium", "fun") into visual specifics (materials, wardrobe,
  locations, pace).

## 3. Map to the backend

1. Pick the flow via the hub [SKILL.md](../SKILL.md) decision tree.
2. Open the matching `prompt-library/*.md` and align wording with the backend's prompting
   rules in `adapters/active.md` (prompt-length window, forbidden words, motion conventions).
3. Gather required IDs/handles (product id, project id, reference uploads) per `active.md`.

## 4. Merge with project memory

If `MASTER_CONTEXT.md` lists brand voice, banned phrases, or winning prompts, **prefer those**
over generic templates.

## 5. Pre-flight check

- [ ] Required payload fields present per `adapters/active.md`.
- [ ] Prompt matches the chosen style file + the backend's rules.
- [ ] No secrets in the request body (only IDs and creative text).
- [ ] Aspect ratio + duration valid for the model (capability matrix).
- [ ] Dialogue gate passed (if speech) and cost confirmed.
