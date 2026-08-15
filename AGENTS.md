# MUSE — Codex Project Instructions

This repository implements the MUSE physical two-console experience. Treat all approved visual design as **frozen** unless the user explicitly requests a change.

MUSE has **two intentionally different visual systems**. Do not average them together and do not create one shared visual skin.

- **Arcade Console 1 — Human + AI:** retro pixel-love-letter arcade / early-desktop visual language.
- **Arcade Console 2 — AI Only:** minimal editorial/technical system UI using black, grey, warm off-white and restrained signal red, with its own monochrome physical-control deck.

The conceptual contrast is part of the exhibit. Visual convergence is a bug.

## Read this first

Before editing production code, read:

1. `docs/implementation/README.md`
2. `docs/implementation/00-source-of-truth.md`
3. the implementation plan for the console being changed.

For Console 1 also read:

- `docs/reference/muse-ui-style-system-v2.md`
- `docs/implementation/03-design-system-implementation.md`
- `docs/implementation/08-arcade-1-human-ai-screens.md`

For Console 2 also read, in order:

- `docs/implementation/18-ai-only-source-of-truth.md`
- `docs/implementation/19-ai-only-visual-system.md`
- `docs/implementation/20-ai-only-component-architecture.md`
- `docs/implementation/21-ai-only-data-state-interactions.md`
- `docs/implementation/22-ai-only-screen-specifications.md`
- `docs/implementation/23-ai-only-testing-acceptance.md`
- `docs/implementation/24-ai-only-codex-build-playbook.md`
- `docs/implementation/25-ai-only-a2-00-display-title-refinement.md`
- `docs/implementation/26-ai-only-a2-00-visual-calibration.md`
- `docs/reference/ai-only-console2-canonical.jpg`
- `docs/reference/ai-only-console2-system-refinement-v2.jpg`

For Console 2, the original four-screen image is authoritative for screen-specific content composition. The refinement-v2 image is the higher visual authority for typography character, color emphasis, separators, red markers and lower physical controls.

For `A2_00`, file `26-ai-only-a2-00-visual-calibration.md` is the latest reviewed authority. File `25` explains the large display-title correction; file `26` locks the current screenshot composition and final calibration details.

The legacy flow at `docs/reference/muse-experience-flow-legacy.md` is reference material only.

## Global rendering model

Both consoles use the same exhibition-stage geometry:

- internal design canvas: `1440 × 1080`
- aspect ratio: `4:3`
- scale the complete stage proportionally to viewport
- do not independently reflow/reorder major regions at responsive breakpoints
- preserve deterministic geometry for visual regression

Shared stage geometry does **not** imply shared visual chrome.

# Console 1 — Human + AI: non-negotiable visual rules

Console 1 uses the approved pixel arcade system only.

- deep navy grid world
- love-letter pixel sprites
- top-left `MUSE SYSTEM v1.0 / LOVE LETTERS, REWIRED.` lockup
- top-right Console 1 label when specified
- large sharp-cornered desktop window
- blank purple title bar
- yellow menu square left, white X square right
- pale textured lavender interior
- stepped pixel depth
- pixel-display + pixel-mono typography
- magenta primary CTAs
- separate bottom hardware strip: red 3D button — gold 3D dial — red 3D button
- never restore old labelled footer (`BUTTON`, `KNOB`, `HOLD BOTH`, `SYSTEM MENU`, etc.)

Do not import Console 2 editorial/technical components into Console 1 unless explicitly instructed.

# Console 2 — AI Only: non-negotiable visual rules

Console 2 must contain **none of the Console 1 pixel chrome**:

- no navy grid
- no purple desktop window
- no pixel love-letter sprites
- no magenta extrusion
- no Console 1 glossy red/gold/red hardware strip
- no pixel typography
- no arcade CTA buttons
- no decorative love-letter environment

Console 2 current visual language:

- warm off-white main field
- light neutral-grey lower control deck
- near-black primary text
- muted grey secondary/system text
- restrained signal red as micro-accent
- heavy condensed neo-grotesk character for the `MUSE` identity/display role
- neutral Swiss/neo-grotesk content typography
- mono/semi-mono system/control labels
- precise black/grey rules and separators
- generous whitespace
- minimal physical controls rendered in a clean industrial/technical style

**Blue/periwinkle is superseded as the dominant Console 2 accent.** Do not restore it as the default action/slider/icon color.

## Console 2 identity and display-title distinction

Persistent top-left identity:

```text
MUSE
AI ONLY
ARCADE CONSOLE 2
```

Rules:

- no tiny screen number
- `MUSE` line is heavier/condensed and assertive
- no icon/heart/badge
- do not add a second `MUSE` wordmark in the bottom-center control deck

The refinement reference's `DIGITAL LOVE LETTER` headline demonstrates typographic weight/character only. Do not copy that phrase into product UI.

On `A2_00`, also render a **separate giant `MUSE` display title** in the main field. This is distinct from the small persistent identity and is the primary visual anchor of the entry screen.

Latest A2_00 calibration from file `26`:

- keep the current strongly left-weighted editorial composition;
- keep exactly two primary red square markers: status + begin instruction;
- keep one restrained 1px hairline beneath the large MUSE title;
- do not reintroduce the earlier radial/dotted context-transfer graphic;
- verify the giant MUSE actually resolves to the approved condensed display face and is not a broad fallback font;
- keep the small persistent identity visually subordinate to the giant title;
- keep the current large whitespace field empty rather than adding helper UI.

## Console 2 red marker language

Use tiny filled red squares as sparse signal anchors.

Current signal token starts at approximately `#EC5B29`, sampled from the refinement reference.

Do not:

- turn red into a large background/fill color
- scatter red markers everywhere
- semantic-color sentiment/emotion/romance

## Console 2 lower control deck

Console 2 has its own persistent on-screen physical-control representation, visually derived from the refinement reference.

It is **not** Console 1's hardware strip.

Deck:

- persistent light-grey region at bottom
- separated from main field by strong thin near-black horizontal rule
- left: outlined circular `BACK` arcade button
- left/center: outlined circular `NEXT` arcade button
- right: outlined rotary/intensity dial with restrained red indicator
- no bottom-center MUSE label

Control construction:

- off-white faces
- black circular outlines
- grey inner linework
- red only as small indicator detail
- no pixel styling
- no gold
- no glossy red button bodies

Back/Next semantics should be represented primarily through the deck controls rather than duplicated floating arrow links.

`REGENERATE` on the result screen remains a restrained software/system text action because there is no fourth approved physical hardware control.

## Console 2 experience rules

Console 2 inherits context and must not repeat registration, recipient name or relationship selection.

The first four production responsibilities are:

1. Welcome back / inherited context acknowledged.
2. Short user prompt.
3. AI interpretation + read-only sentiment/emotion/romance + editable tone controls.
4. Generated AI letter + insights.

After the AI-only result, continue into the shared MUSE comparison/reflection flow.

Analysis combines:

- inherited Arcade 1 context,
- recipient + relationship context,
- Console 2 short prompt.

Sentiment, emotion and romance are read-only analysis.

Tone controls are AI-proposed and user-adjustable:

- warmth
- intimacy
- emotional depth
- playfulness
- nostalgia

The visible intensity dial may mirror/control only the currently active tone control according to the documented interaction contract. It must not create a sixth hidden tone value.

AI voice remains competent and neutral/computational, never villainous or parody-robotic.

## Regeneration rule

On `A2_03`, regenerate happens **in place** while preserving:

- inherited context
- short prompt
- read-only analysis state
- current user-adjusted tone values

It changes only the active generated-letter variant and matching result insights.

## Current implementation scope

Build the complete static/prototype experience with navigation and deterministic fixtures.

Do not implement in this phase:

- production AI model calls
- camera / OCR / vision
- printer integration
- real serial/MIDI/Arduino hardware input
- sound
- animation
- analytics
- backend persistence

The **on-screen Console 2 button/dial representation is current scope**. Only real physical hardware wiring is deferred.

## Technology constraints

Use:

- React
- Vite
- TypeScript
- plain CSS / CSS Modules / small token layer
- Playwright for flow and screenshot regression

Do not introduce without explicit approval:

- Next.js
- Tailwind
- Material UI
- Bootstrap
- Chakra
- shadcn
- Framer Motion
- Redux
- generic design-system libraries

## Architecture rule

Share logic where genuinely shared; **do not share visual shells across consoles**.

Recommended split:

- shared: stage scaler, session state, route/state machine, keyboard/semantic action abstraction, testing utilities
- Console 1: `ArcadeOneShell` and pixel components
- Console 2: `AiOnlyShell`, refined editorial components and `AiControlDeck`
- reflection: shared reflection shell/components as documented by its own plan

Never make Console 2 a theme prop on `MuseWindow`.

## Copy rule

Copy is editable. Visual geometry/component styling is not.

Keep screen copy and fixtures in config/content files. Components consume data via props.

Do not copy reference-only words/IDs unless they are explicitly approved product copy.

## Visual acceptance

When a visual reference exists:

1. render at exactly `1440 × 1080`,
2. capture **stage only**,
3. compare against the relevant approved references,
4. correct geometry/type/spacing/color via shared tokens/components,
5. confirm no unrelated console visual system changed.

For Console 2 specifically verify:

- no dominant blue
- no bottom-center MUSE
- stable grey deck + black separator
- outlined BACK/NEXT buttons
- outlined dial with small red indicator
- heavy condensed persistent `MUSE` identity
- on `A2_00`, separate oversized `MUSE` display title exists and dominates the main field
- on `A2_00`, no radial context-transfer graphic
- on `A2_00`, exactly two primary red square markers
- sparse red markers elsewhere

## Change discipline

For every task:

1. state which implementation-plan file governs the work,
2. identify which console visual system is active,
3. inspect existing console-specific shared components before creating new ones,
4. make the smallest reversible change,
5. run typecheck/tests/relevant visual snapshots,
6. report changed files and unresolved reference mismatches.

If something is ambiguous, **stop and report the ambiguity instead of designing through it**.