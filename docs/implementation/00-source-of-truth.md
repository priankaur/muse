# 00 — Source of Truth and Conflict Resolution

MUSE has evolved through several design explorations. Older documents and generated screens contain superseded naming, station ordering, footer instructions and visual treatments. Codex must not average those versions together.

## Priority order

When sources conflict, use this order:

1. Explicit latest user instruction in the current implementation task.
2. `AGENTS.md`.
3. Console-specific implementation plans in `docs/implementation/`.
4. Console-specific canonical visual references in `docs/reference/`.
5. Older design-system docs.
6. Legacy flow documents and older generations.

A lower-priority source is obsolete where it conflicts with a higher-priority source.

# MUSE has two intentionally different visual systems

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

Console 2 uses **two complementary references**:

1. `docs/reference/ai-only-console2-canonical.jpg` — canonical four-screen content composition / flow reference.
2. `docs/reference/ai-only-console2-system-refinement-v2.jpg` — latest visual-system/chrome refinement and higher authority for typography, palette, separators, red signal markers and physical-control deck.

Production rules:

- same 4:3 / 1440×1080 stage geometry as Console 1
- warm off-white main field
- neutral light-grey lower control deck
- near-black primary typography
- muted grey secondary/system typography
- sparse signal red as the main accent
- heavy condensed neo-grotesk character for the `MUSE` identity/display role
- neutral Swiss/neo-grotesk content typography
- mono/semi-mono technical labels where appropriate
- high whitespace
- precise horizontal rules and separators
- persistent top-left identity: `MUSE / AI ONLY / ARCADE CONSOLE 2`
- remove tiny screen numbers
- persistent Console 2 control deck with outlined `BACK`, outlined `NEXT`, and outlined intensity dial with a small red pointer
- **no bottom-center MUSE wordmark**
- absolutely no Console 1 pixel arcade chrome

The earlier periwinkle/blue accent direction is superseded. Do not restore blue as the dominant default Console 2 accent.

Console 2 must **not** use:

- navy grid background
- purple MuseWindow
- pixel sprites
- magenta extrusion
- Console 1 glossy red/gold/red control strip
- pixel fonts
- arcade button CTAs
- decorative love-letter UI

Console 2's visible controls are intentionally present, but they are a different visual family: monochrome/industrial outlines, off-white faces, grey linework and minimal red signal detail.

# Current experience structure

1. Registration / session creation.
2. Arcade 1 — Human + AI.
3. Arcade 2 — AI Only, inheriting context.
4. Shared comparison/reflection.
5. Final stance / choice.
6. Physical/print handoff later.

Arcade 2 does not repeat registration, recipient name or relationship selection.

## Arcade 2 canonical first four responsibilities

- `A2_00` Welcome back / inherited context loaded.
- `A2_01` Short prompt.
- `A2_02` Analysis + AI-proposed editable tone controls.
- `A2_03` Generated letter + insights.

There is no required standalone generating page in the current static visual sequence.

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

## Console 2 control semantics

Persistent visible deck:

- `BACK` = semantic back action where available
- `NEXT` = semantic begin/continue action where available
- `INTENSITY DIAL` = may control the currently active tone parameter on `A2_02`; it must not invent a new sixth tone value

If an action is unavailable, keep the hardware visible in a neutral disabled state rather than removing/reflowing the deck.

`REGENERATE` remains a restrained software/system text action on `A2_03` because no fourth physical control has been approved.

Real serial/MIDI/Arduino hardware wiring remains deferred; the on-screen visual representation is current scope.

## AI-only voice

Keep system copy neutral, restrained and computational. It should be competent and calm, not warm/empathic and not cartoonishly robotic.

The latest refinement reference may influence the style of system-status microcopy, but do not copy unrelated literal phrases or IDs from that reference unless separately approved.

## Regeneration — locked for current build

`regenerate` acts in place on the result screen:

- preserve inherited context
- preserve short prompt
- preserve current tone-control values
- preserve read-only analysis input state
- generate/select a new letter variant
- update matching result insights
- keep the visitor on the result screen

`BACK` remains available if the visitor wants to retune settings.

Static prototype: cycle deterministic fixture variants with no API call.

## Legacy material that remains useful

Legacy flow can still inform:

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
- old periwinkle/blue-dominant Console 2 accent system
- floating Back/Continue links duplicated alongside the new control deck
- bottom-center `MUSE` copied from the refinement reference
- `DIGITAL LOVE LETTER` copied as product copy
- reference-only IDs/status strings copied literally
- `MUSE SYSTEM` text inside Console 1's purple title bar
- rounded Console 1 main window
- `HOLD BOTH`
- `SYSTEM MENU`
- labelled Console 1 hardware footer
- dense decorative moon/star scenes
- tiny screen numbers from the AI-only reference montage

## Copy is not a design token

Copy can change without changing layout primitives. If content length changes, preserve the console-specific grid, type hierarchy, control deck and visual system before altering chrome or composition.