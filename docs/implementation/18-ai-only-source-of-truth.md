# 18 — Arcade Console 2 / AI Only — Source of Truth

This document is the primary product/design contract for Console 2. It overrides the earlier `09-arcade-2-ai-only-screens.md` where that older file conflicts.

## Canonical visual reference

`docs/reference/ai-only-console2-canonical.png`

The reference is canonical, not merely moodboard inspiration.

The montage contains four screen compositions. Production removes the tiny screen numbers visible in the montage; all other intentional visual relationships should be reproduced closely.

## Product role

Console 2 is the **AI Only** path. It follows Console 1 — Human + AI — and inherits session context instead of asking the visitor to repeat setup.

The contrast is intentional:

- Console 1 feels tactile, expressive, colourful and arcade-like.
- Console 2 feels restrained, sparse, neutral and computational.

Console 2 should still be usable and polished. It must not be written or styled as a parody of AI.

## Stage

- fixed internal canvas: `1440 × 1080`
- aspect ratio: `4:3`
- entire stage scales proportionally to viewport
- no mobile-style reflow
- no independent responsive rearrangement of major regions

## Console 2 identity

Persistent top-left lockup on every AI-only screen:

- `MUSE`
- `AI ONLY`
- `ARCADE CONSOLE 2`

Do not include a screen number.

## Explicitly prohibited Console 1 carry-over

Console 2 must not render:

- navy grid background
- MuseWindow / desktop window frame
- purple title bar
- yellow menu square
- white X square
- lavender paper window
- pixel love-letter sprites
- magenta CTA buttons
- pixel-display typography
- 3D red-button / gold-dial / red-button on-screen strip
- decorative arcade chrome

These are not optional theme choices. They belong to Console 1 only.

## AI-only first four screens

### `A2_00` — Welcome back

Acknowledge inherited session context and readiness.

### `A2_01` — Short prompt

Ask what the visitor wants AI to focus on. Keep input short and direct.

### `A2_02` — Interpretation + controls

AI proposes an interpretation from combined context. Display:

Read-only analysis:

- sentiment analysis
- emotion detection
- romance / romantic-intent detection

Editable AI-proposed tone controls:

- warmth
- intimacy
- emotional depth
- playfulness
- nostalgia

User may adjust tone controls before generation.

### `A2_03` — Generated letter + insights

Show generated letter and read-only insight rail containing:

- sentiment
- emotion
- romance
- tone profile

Actions:

- back
- regenerate
- continue

`continue` enters the shared MUSE comparison/reflection flow.

## Analysis input contract

The AI-only interpretation is based on a combination of:

1. inherited Arcade 1 context,
2. recipient and relationship context,
3. the visitor's short Console 2 prompt.

In the static build this must be represented by deterministic fixtures. Do not fabricate an API or require network access.

## Inherited context

At minimum Console 2 may access:

- visitor first name
- recipient name
- relationship
- visitor-originated Human + AI source/context carried from Arcade 1
- Arcade 1 completion/result reference required for later comparison

Console 2 must never request recipient name or relationship again.

## Voice

Console 2 system copy is:

- concise
- neutral
- calm
- competent
- computational
- non-judgmental

Avoid:

- emotionally affirming language
- poetic system narration
- overt empathy
- villainous machine language
- fake scientific certainty

Examples of appropriate register:

- `welcome back, kristian`
- `your context from the first experience has been loaded.`
- `what would you like AI to focus on?`
- `here’s what I understand.`

## Regenerate behaviour — current recommendation and implementation rule

Regeneration should happen **in place**.

Why:

- it preserves the minimal one-direction flow,
- it avoids forcing the visitor to redo interpretation controls,
- it makes regeneration feel like a machine operation rather than a new emotional decision,
- the user still has `back` if they want to change settings.

Behaviour:

- preserve inherited context
- preserve the short prompt
- preserve all user-adjusted tone-control values
- select/generate a new letter variant
- update insights associated with the new variant
- remain on `A2_03`

Static prototype: cycle deterministic fixture variants.

## Decoration of the letter

Handwriting, stamps, doodles, colour or other letter-personalisation may be explored later. They are explicitly out of scope for the current implementation. The initial result uses a restrained typed-document presentation from the reference.

## Motion

No animation in the current build.

No:

- entry motion
- loaders as visual spectacle
- pulsing analysis
- animated sliders
- transitions

State may change immediately for static prototyping.

## Handoff

After `A2_03` `continue`, route into the shared comparison/reflection flow. Do not add extra AI-only screens unless explicitly approved.

## Ambiguity rule

When a Console 2 implementation detail is not specified:

1. inspect the canonical reference,
2. choose the smallest neutral implementation consistent with it,
3. do not borrow a Console 1 pattern,
4. do not add a generic SaaS convention merely because it is common,
5. if visual/product behaviour remains ambiguous, report it and stop rather than inventing.