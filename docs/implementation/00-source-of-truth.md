# 00 — Source of Truth and Conflict Resolution

MUSE has evolved through several design explorations. Older documents and generated screens contain superseded naming, station ordering, footer instructions and visual treatments. Codex must not average those versions together.

## Priority order

When sources conflict, use this order:

1. Explicit latest user instruction in the current implementation task.
2. `AGENTS.md`.
3. Console-specific implementation plans in `docs/implementation/`.
4. Console-specific canonical visual reference screenshots in `docs/reference/`.
5. Older design-system docs.
6. Legacy flow documents and older generations.

A lower-priority source is obsolete where it conflicts with a higher-priority source.

# MUSE now has two intentionally different visual systems

This is a product requirement, not an implementation accident.

## Console 1 — Human + AI

Canonical visual system:

- 4:3 / 1440×1080 stage
- dark navy square-grid world
- sparse love-letter pixel sprites
- persistent pixel MUSE lockup
- large sharp-cornered desktop-style content window
- purple blank title bar
- yellow menu square + white close square
- pale warm lavender paper interior
- pixel typography
- magenta CTAs
- bottom red-button / gold-dial / red-button hardware strip

Reference: `docs/reference/muse-ui-style-system-v2.md` plus latest approved Console 1 screenshots.

## Console 2 — AI Only

Canonical visual system is the four-screen minimal AI-only reference at:

`docs/reference/ai-only-console2-canonical.png`

Production rules:

- same 4:3 / 1440×1080 stage geometry as Console 1
- warm off-white / bone canvas
- near-black typography
- thin neutral-grey rules and borders
- periwinkle / muted electric-blue functional accents
- Swiss / neo-grotesk typography
- high whitespace
- minimal cards and lines
- visible text navigation only: back / continue / regenerate where relevant
- persistent top-left identity: `MUSE / AI ONLY / ARCADE CONSOLE 2`
- remove the tiny screen number visible in the montage
- absolutely no Console 1 pixel arcade chrome

Console 2 must **not** use:

- navy grid background
- purple MuseWindow
- pixel sprites
- magenta extrusion
- 3D arcade-control strip as an on-screen graphic
- pixel fonts
- arcade button CTAs
- decorative love-letter UI

The physical cabinet may still use physical controls later. Their visible on-screen representation is intentionally absent in Console 2.

# Current experience structure

1. Registration / session creation.
2. Arcade 1 — Human + AI.
3. Arcade 2 — AI Only, inheriting context.
4. Shared comparison/reflection.
5. Final stance / choice.
6. Physical/print handoff later.

Arcade 2 does not repeat registration, recipient name or relationship selection.

## Arcade 2 canonical first four responsibilities

The approved reference establishes this sequence:

- `A2_00` Welcome back / inherited context loaded.
- `A2_01` Short prompt.
- `A2_02` Analysis + AI-proposed editable tone controls.
- `A2_03` Generated letter + insights.

There is no required standalone generating page in the current static visual sequence. A future production AI request may use a temporary local loading state without becoming a new full screen unless explicitly designed.

After `A2_03`, continue to the shared reflection/comparison flow.

## AI-only analysis source

Analysis/generation combines:

1. inherited Arcade 1 user/session context,
2. recipient + relationship context,
3. the visitor's Console 2 short prompt.

Read-only analysis:

- sentiment
- emotion
- romance / romantic intent

Editable AI-proposed tone controls:

- warmth
- intimacy
- emotional depth
- playfulness
- nostalgia

The visitor can adjust tone controls before generation.

## AI-only voice

Keep system copy neutral, restrained and computational. It should be competent and calm, not warm/empathic, and not cartoonishly robotic.

## Regeneration recommendation — locked for current build

`regenerate` acts in place on the result screen:

- preserve inherited context
- preserve short prompt
- preserve current tone-control values
- generate/select a new letter variant
- keep the visitor on the result screen

`back` remains available if the visitor wants to retune settings.

Static prototype behaviour: cycle through deterministic fixture variants with no API call.

## Legacy material that remains useful

The legacy flow can still inform:

- capture constraints on Console 1
- typed note behaviour
- reflection concepts
- postcard/print handoff
- token wall
- physical-control philosophy

Use legacy details only where they do not conflict with current console-specific plans.

## Deprecated details

Do not restore merely because they exist in older files:

- `Ex-Love` / `Next Love` naming
- AI-first Console 1 ordering
- Console 1 chrome on Console 2
- `MUSE SYSTEM` text inside the purple title bar
- rounded Console 1 main window
- `HOLD BOTH`
- `SYSTEM MENU`
- labelled hardware footer
- dense decorative moon/star scenes
- flat generic arcade controls
- tiny screen numbers from the AI-only reference montage

## Copy is not a design token

Copy can change without changing layout primitives. If content length changes, preserve the console-specific grid and type hierarchy before altering chrome or composition.