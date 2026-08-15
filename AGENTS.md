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

For current Console 1 enhancement work, ALSO read:

- `docs/implementation/28-arcade1-motion-audio-interactions.md`
- `docs/implementation/29-arcade1-human-letter-analysis.md`
- `docs/implementation/30-arcade1-enhancement-build-playbook.md`

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
- `docs/implementation/27-ai-only-a2-01-copy-refinement.md`
- `docs/reference/ai-only-console2-canonical.jpg`
- `docs/reference/ai-only-console2-system-refinement-v2.jpg`

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

## Console 1 motion + sound — current approved scope

The earlier blanket deferral of animation/sound is superseded for Arcade 1 by file `28`.

Current approved interaction feedback includes:

- CTA press/depth collapse;
- red arcade-button press;
- discrete gold-dial detent rotation/tick;
- short stepped content/page transitions;
- semantic click/confirm/dial/page sounds;
- restrained processing/result reveal after core feedback review;
- gentle stepped sprite bobbing only after core interaction feedback is stable.

Rules:

- use CSS/keyframes + small semantic state helpers, not Framer Motion;
- preserve the exact resting geometry of approved components;
- do not move the entire MuseWindow around during every transition;
- do not use modern spring/bounce easing;
- do not add background music;
- respect `prefers-reduced-motion`;
- audio must unlock from user gesture and fire from semantic events, never component re-renders;
- page transitions must not double-commit routes on repeated presses.

## Console 1 human-letter analysis — current approved scope

After accepting the captured human letter, Arcade 1 now includes:

```text
A1_06 -> A1_06A -> A1_07
```

`A1_06A` is a read-only machine readback **before AI enhancement**.

It must show exactly four primary outputs:

1. sentiment analysis;
2. emotions recognized;
3. character count of recognized/extracted human-letter text;
4. visual meaning / qualified interpretation of visible non-text cues.

Important distinctions:

- `A1_06A` character count is the human letter extraction count;
- `A1_07` keeps its separate 120-character note counter;
- analysis is fixture-driven in the current build;
- production OCR/vision/model calls remain deferred;
- visual meaning must use uncertainty-aware language and must not be presented as psychological fact;
- do not copy Console 2 analysis-card styling into Arcade 1;
- do not renumber A1_07–A1_11 merely to insert this new responsibility.

The visitor sees the machine readback, then can add/correct context in `A1_07`, then tune the enhancement in `A1_08`.

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

On `A2_00`, also render a separate giant `MUSE` display title in the main field. File `26` is the current visual calibration.

Latest A2_00 calibration:

- strongly left-weighted editorial composition;
- exactly two primary red square markers: status + begin instruction;
- one restrained 1px hairline beneath the large MUSE title;
- no radial/dotted context-transfer graphic;
- verify the giant MUSE resolves to the approved condensed display face;
- keep large whitespace field intentionally empty.

## Console 2 A2_01 exhibition-continuation copy

Current default copy from file `27`:

```text
you've shaped a love letter with AI.
now see what AI creates on its own.
```

Supporting line:

```text
give it one short direction. it will generate the rest.
```

Do not restore the old generic AI-focus question unless explicitly requested.

## Console 2 red marker language

Use tiny filled red squares as sparse signal anchors.

Current signal token starts at approximately `#EC5B29`.

Do not turn red into a large fill or semantic-color sentiment/emotion/romance.

## Console 2 lower control deck

Console 2 has its own persistent on-screen physical-control representation:

- persistent light-grey region at bottom;
- strong thin near-black horizontal separator;
- left: outlined `BACK` button;
- next: outlined `NEXT` button;
- right: outlined rotary/intensity dial with restrained red indicator;
- no bottom-center MUSE label.

It is not Console 1's hardware strip.

`REGENERATE` remains a restrained software/system text action because there is no fourth approved hardware control.

## Console 2 experience rules

Console 2 inherits context and must not repeat registration, recipient name or relationship selection.

The four responsibilities are:

1. Welcome back / inherited context acknowledged.
2. Short prompt framed as continuation from Human + AI to AI-only generation.
3. AI interpretation + read-only sentiment/emotion/romance + editable tone controls.
4. Generated AI letter + insights.

After result, continue to shared comparison/reflection.

Tone controls:

- warmth
- intimacy
- emotional depth
- playfulness
- nostalgia

The visible intensity dial may control only the currently active tone control. It must not create a sixth hidden value.

AI voice remains competent and neutral/computational.

## Current integration scope

Current build may include:

- Arcade 1 scoped motion and interaction audio from file `28`;
- Arcade 1 fixture-driven human-letter analysis UI/data seam from file `29`;
- complete static/prototype Console 2 visuals/interactions.

Still deferred unless later activated:

- production AI/model calls;
- production OCR/vision;
- live camera integration;
- printer integration;
- real serial/MIDI/Arduino hardware input;
- backend persistence;
- final production sound mix/assets;
- Console 2 animation/sound.

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

- shared: stage scaler, session state, route/state machine, semantic input abstraction, testing utilities;
- Console 1: `ArcadeOneShell`, pixel components, Arcade 1 feedback/audio layer, human-letter analysis screen/service seam;
- Console 2: `AiOnlyShell`, refined editorial components and `AiControlDeck`;
- reflection: shared reflection shell/components as documented by its own plan.

Never make Console 2 a theme prop on `MuseWindow`.

## Copy rule

Copy is editable. Visual geometry/component styling is not.

Keep screen copy and fixtures in config/content files. Components consume data via props.

## Visual acceptance

When a visual reference exists:

1. render at exactly `1440 × 1080`;
2. capture stage only;
3. compare against approved references;
4. correct via shared tokens/components rather than compensating decoration;
5. confirm the other console did not change.

For Arcade 1 motion work, also verify the post-animation settled frame is visually identical to the approved static geometry.

## Change discipline

For every task:

1. state which implementation-plan file governs the work;
2. identify which console visual system is active;
3. inspect existing console-specific shared components before creating new ones;
4. make the smallest reversible change;
5. run typecheck/tests/relevant visual snapshots;
6. report changed files and unresolved reference mismatches.

If something is ambiguous, stop and report it instead of designing through it.
