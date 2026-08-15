# MUSE — Codex Project Instructions

This repository implements the MUSE physical two-console experience. Treat all approved visual design as **frozen** unless the user explicitly requests a change.

MUSE now has **two intentionally different visual systems**. Do not average them together and do not try to create one shared visual skin.

- **Arcade Console 1 — Human + AI:** retro pixel-love-letter arcade / early-desktop visual language.
- **Arcade Console 2 — AI Only:** minimal warm-white / black / neutral-grey Swiss-editorial interface with restrained periwinkle-blue functional accents.

The conceptual contrast between the two consoles is part of the exhibit. Visual convergence is a bug.

## Read this first

Before editing production code, read:

1. `docs/implementation/README.md`
2. `docs/implementation/00-source-of-truth.md`
3. The implementation plan for the console being changed.

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
- `docs/reference/ai-only-console2-canonical.png`

The legacy flow at `docs/reference/muse-experience-flow-legacy.md` is reference material only.

## Global rendering model

Both consoles use the same exhibition-stage geometry:

- internal design canvas: `1440 × 1080`
- aspect ratio: `4:3`
- scale the complete stage proportionally to the viewport
- do not independently reflow or reorder major regions at responsive breakpoints
- preserve deterministic geometry for visual regression

The shared stage geometry does **not** imply shared visual chrome.

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
- never restore the old labelled footer (`BUTTON`, `KNOB`, `HOLD BOTH`, `SYSTEM MENU`, etc.)

Do not use Console 2 minimal cards, Swiss typography, thin grey UI or blue text links inside Console 1 unless a future user instruction explicitly changes the design.

# Console 2 — AI Only: non-negotiable visual rules

Console 2 is governed by the attached canonical four-screen reference and the AI-only implementation bundle.

Console 2 must contain **none of the Console 1 arcade chrome**:

- no navy grid
- no purple desktop window
- no pixel sprites
- no magenta extrusion
- no rendered red/gold/red hardware strip
- no pixel typography
- no arcade CTA buttons
- no decorative love-letter environment

Console 2 visual language:

- warm off-white / bone stage, not bright pure white
- near-black primary text
- light neutral-grey rules and card borders
- restrained periwinkle / muted electric blue as the only functional accent
- Swiss / neo-grotesk typographic character
- generous whitespace
- thin outlines
- minimal navigation text (`← back`, `continue →`, `↻ regenerate`)
- no decorative UI added merely to make the screen feel richer

Persistent Console 2 identity appears top-left on every screen:

`MUSE`
`AI ONLY`
`ARCADE CONSOLE 2`

Do **not** render a tiny screen number. The screen numbers visible in the source montage are removed from production.

## Console 2 experience rules

Console 2 inherits context and must not repeat registration, recipient name or relationship selection.

The first four production responsibilities are:

1. Welcome back / inherited context acknowledged.
2. Short user prompt.
3. AI interpretation + analysis-only sentiment/emotion/romance + editable tone controls.
4. Generated AI letter + insights.

After the AI-only result, continue into the shared MUSE comparison/reflection flow.

Analysis combines:

- inherited Arcade 1 context,
- recipient + relationship context,
- the Console 2 short prompt.

Sentiment, emotion and romance are read-only analysis. Tone controls are AI-proposed and user-adjustable.

Current tone controls:

- warmth
- intimacy
- emotional depth
- playfulness
- nostalgia

The AI voice should be competent and neutral/computational, never villainous or parody-robotic.

## Regeneration rule

On the AI-only result screen, `regenerate` must regenerate **in place** while preserving the short prompt, inherited context and the visitor's current tone-control values. Do not force the visitor back to the analysis screen.

The visitor may explicitly use `back` to return and retune controls. In the static build, regeneration swaps deterministic fixture variants while preserving state.

## Current implementation scope

Build the complete static/prototype experience with navigation and deterministic fixtures.

Do not implement in this phase:

- production AI model calls
- camera / OCR / vision
- printer integration
- serial/MIDI/Arduino hardware input
- sound
- animation
- analytics
- backend persistence

Future interfaces/stubs may exist, but the visible experience must be complete without those integrations.

## Technology constraints

Use:

- React
- Vite
- TypeScript
- plain CSS / CSS Modules / a small token layer
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

Share logic where it is genuinely shared; **do not share visual shells across the two consoles**.

Recommended split:

- shared: stage scaler, session state, route/state machine, keyboard abstraction, testing utilities
- Console 1: `ArcadeOneShell` and pixel components
- Console 2: `AiOnlyShell` and minimal components
- reflection: shared reflection shell/components as documented by its own plan

Never make Console 2 a theme prop on `MuseWindow`. It is a distinct visual composition, not a reskin of the pixel desktop window.

## Copy rule

Copy is editable. Visual geometry and component styling are not.

Keep screen copy and fixture data in content/config files. Components consume data through props.

## Visual acceptance

When a visual reference exists:

1. render at exactly `1440 × 1080`,
2. capture a deterministic Playwright screenshot,
3. compare against the approved reference,
4. correct geometry/type/spacing/color rather than inventing compensating decoration,
5. confirm no unrelated console visual system changed.

## Change discipline

For every task:

1. state which implementation-plan file governs the work,
2. identify which console visual system is active,
3. inspect existing console-specific shared components before creating new ones,
4. make the smallest reversible change,
5. run typecheck/tests/relevant visual snapshots,
6. report changed files and unresolved reference mismatches.

If something is ambiguous, **stop and report the ambiguity instead of designing through it**.