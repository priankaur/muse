# 18 — Arcade Console 2 / AI Only — Source of Truth

This document is the primary product/design contract for Console 2. It overrides the earlier `09-arcade-2-ai-only-screens.md` where that older file conflicts.

## Canonical visual references and precedence

Console 2 now uses **two complementary references**:

1. `docs/reference/ai-only-console2-canonical.jpg` — canonical source for the four-screen content composition and flow.
2. `docs/reference/ai-only-console2-system-refinement-v2.jpg` — **latest visual-system refinement** and higher authority for typography character, color emphasis, rules/separators, micro-accent markers, and the lower physical-control deck.

If the two images conflict visually, the refinement-v2 image wins for visual system/chrome while the original four-screen montage remains authoritative for screen-specific content composition.

Production removes any screen numbers or irrelevant reference-only metadata. Do not copy literal IDs, the phrase `DIGITAL LOVE LETTER`, or other reference copy unless a screen content file explicitly contains it.

## Product role

Console 2 is the **AI Only** path. It follows Console 1 — Human + AI — and inherits session context instead of asking the visitor to repeat setup.

The contrast is intentional:

- Console 1 feels tactile, expressive, colourful and pixel-arcade-like.
- Console 2 feels restrained, sparse, editorial, technical and computational.

Console 2 is still a physical arcade console, so the latest refinement intentionally reintroduces a **minimal physical-control representation** without importing Console 1's visual language.

Console 2 must not become a parody of AI. It should be competent, calm, precise and less emotionally expressive than the Human + AI path.

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

`MUSE` must use the latest reference's **heavy condensed neo-grotesk weight/character**: visually as bold and assertive as the `DIGITAL LOVE LETTER` display type in the refinement reference, while remaining in the identity's top-left location unless a screen plan explicitly introduces a separate hero title.

Do **not** copy the bottom-center `MUSE` wordmark visible in the refinement reference. The lower control deck has no centered MUSE label.

## Current visual character

The current dominant palette is:

- black / near-black
- neutral grey
- warm off-white
- restrained signal red

Blue is no longer part of the primary Console 2 visual language and must not be used as the default accent.

Use **small red square markers** as micro-accent anchors. Red is a signal color, not a large surface color.

Use precise horizontal rules and separators to structure the interface. The screen should feel designed through typography, alignment, whitespace and linework rather than cards or decoration.

## Console 2 physical-control representation

The latest refinement adds a persistent lower control deck separated from the main content by a strong thin rule.

The deck contains:

- left: outlined circular `BACK` arcade button
- left/center: outlined circular `NEXT` arcade button
- right: large outlined rotary dial / knob with a restrained red indicator
- dial label: `INTENSITY DIAL` where that is the current hardware role

These controls are **not** Console 1 controls.

Do not render:

- glossy red pixel buttons
- gold pixel rotary dial
- 3D pixel extrusion
- navy arcade control housing
- Console 1 hardware strip labels or styling

Console 2 controls are monochrome/industrial/technical: black outlines, off-white faces, neutral grey linework and minimal red signal detail.

## Explicitly prohibited Console 1 carry-over

Console 2 must not render:

- navy grid background
- `MuseWindow` / desktop window frame
- purple title bar
- yellow menu square
- white X square
- lavender paper window
- pixel love-letter sprites
- magenta CTA buttons
- pixel-display typography
- Console 1 red/gold/red pixel hardware strip
- decorative love-letter arcade chrome

These belong to Console 1 only.

## AI-only first four screens

### `A2_00` — Welcome back

Acknowledge inherited session context and readiness.

### `A2_01` — Short prompt

Ask what the visitor wants AI to focus on. Keep input short and direct.

### `A2_02` — Interpretation + controls

AI proposes an interpretation from combined context.

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

The user may adjust tone controls before generation.

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

In the static build this is represented by deterministic fixtures. Do not fabricate a production API or require network access.

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

The refinement reference may inspire system-status microcopy and metadata typography, but do not copy unrelated literal reference phrases into the experience.

## Regenerate behaviour

Regeneration happens **in place** on `A2_03`.

Preserve:

- inherited context
- short prompt
- all user-adjusted tone-control values
- read-only interpretation input state

Change:

- generated letter variant
- result-specific insights

Remain on `A2_03`.

Static prototype: cycle deterministic fixture variants.

## Decoration of the letter

Handwriting, stamps, doodles, colour or other letter-personalisation may be explored later. They are out of scope for the current implementation. The initial result uses a restrained typed-document presentation.

## Motion

No animation in the current build.

No:

- entry motion
- animated loaders as visual spectacle
- pulsing analysis
- animated sliders
- page transitions

## Handoff

After `A2_03` `continue`, route into the shared comparison/reflection flow. Do not add extra AI-only screens unless explicitly approved.

## Ambiguity rule

When a Console 2 detail is not specified:

1. inspect both canonical references,
2. use refinement-v2 for system/chrome decisions,
3. use the original four-screen reference for screen content composition,
4. choose the smallest implementation consistent with both,
5. do not borrow a Console 1 pattern,
6. do not add a generic SaaS convention,
7. report remaining ambiguity instead of inventing a new design.