# 24 — Arcade Console 2 / AI Only — Codex Build Playbook

Use this file to keep implementation incremental and reviewable. Do not ask Codex to build all four screens in one uncontrolled pass.

## Global read order

Every Console 2 task must begin by reading:

1. `AGENTS.md`
2. `docs/implementation/18-ai-only-source-of-truth.md`
3. `docs/implementation/19-ai-only-visual-system.md`
4. `docs/implementation/20-ai-only-component-architecture.md`
5. `docs/implementation/22-ai-only-screen-specifications.md`
6. `docs/implementation/23-ai-only-testing-acceptance.md`
7. `docs/implementation/25-ai-only-a2-00-display-title-refinement.md`
8. the relevant task section below
9. `docs/reference/ai-only-console2-canonical.jpg`
10. `docs/reference/ai-only-console2-system-refinement-v2.jpg`

Use the original four-screen image for content composition and the refinement-v2 image for current typography/chrome/control-deck language.

For `A2_00`, file `25` is the latest reviewed override and wins where it conflicts with the earlier A2_00 composition in file `22`.

Do not use Console 1 screenshots as visual references for Console 2.

---

# Task A — Audit existing Console 2 code

Goal: understand the current build and avoid accidental coupling to Console 1 or obsolete blue/text-nav rules.

Codex should:

1. inspect existing stage/session/navigation architecture,
2. identify the current Console 2 shell/tokens/components,
3. identify any current assumption that all consoles use the pixel shell,
4. identify any existing periwinkle/blue Console 2 accent tokens,
5. identify existing floating `← back` / `continue →` navigation,
6. identify current A2 routes/state shape,
7. identify screenshot/test infrastructure,
8. report exactly which files require visual-system migration.

Before changing code, state what will be **reused**, **replaced**, and **added**.

Acceptance:

- no duplicate stage scaler,
- no plan to theme `MuseWindow`,
- no accidental deletion of shared session/navigation logic,
- recognizes that the latest refinement supersedes earlier blue/floating-navigation styling.

---

# Task B — Refine the Console 2 foundation only

This is the next task if the earlier minimal shell already exists.

Implement/refactor only the shared Console 2 foundation:

- `aiOnly.tokens.css`
- `AiOnlyShell`
- `AiOnlyIdentity`
- display/content/system typography roles
- `SignalMarker`
- `SystemRule`
- `AiControlDeck`
- `AiArcadeButton`
- `AiRotaryDial`

Required visual changes:

- dominant black / grey / warm off-white / red system
- remove blue as default accent
- `MUSE` identity line becomes heavier/condensed
- no large outer rounded app-card treatment
- persistent grey lower deck
- 2px near-black deck separator
- outlined BACK and NEXT arcade buttons
- outlined right-side intensity dial with red pointer
- small red square markers
- **no bottom-center MUSE wordmark**

Do not implement screen-specific body content yet beyond a temporary calibration route if necessary.

Render at exactly `1440 × 1080`.

Capture stage-only screenshot.

Run typecheck/tests.

**STOP for visual review.**

Acceptance:

- no host/browser/preview UI in screenshot,
- deck begins at shared canonical y coordinate,
- hardware geometry matches shared tokens,
- identity is correctly positioned and heavier,
- red remains sparse,
- no Console 1 pixel hardware appears,
- no blue/periwinkle dominates,
- no bottom-center MUSE appears.

---

# Task C — Implement/refine `A2_00` only

This task is governed by both:

- `22-ai-only-screen-specifications.md`
- `25-ai-only-a2-00-display-title-refinement.md`

If they conflict on A2_00 visual hierarchy, **file 25 wins**.

Implement:

- persistent small top-left identity,
- a **separate oversized editorial `MUSE` display title** in the main content field,
- personalized welcome title/content,
- context-loaded subtitle,
- static `ContextSignal` updated to neutral + tiny red signal,
- restrained technical status/microcopy using red marker,
- begin action mapped to deck `NEXT`,
- a small amount of secondary structural linework if useful for editorial hierarchy.

Critical title rule:

- the giant `MUSE` title is distinct from the persistent top-left identity,
- do not satisfy the requirement by merely enlarging the small identity,
- do not put the giant title in the deck,
- do not make it red,
- do not copy `DIGITAL LOVE LETTER`,
- use the heavy condensed display role at approximately 118–150px, starting around 132px,
- it must be the primary visual anchor of A2_00.

Recommended starting title region:

```text
x: 76–90
y: 170–210
width: 560–720
```

Deck state:

- BACK visible but disabled
- NEXT enabled
- dial visible but inactive

Do not build A2_01–A2_03 in this task.

Capture a clean `1440 × 1080` screenshot and stop.

Acceptance:

- persistent identity remains in its shared anchor,
- separate giant `MUSE` display title exists,
- the giant title dominates the main field,
- welcome/context content remains present and secondary,
- red markers remain sparse,
- no bottom-center MUSE,
- deck geometry unchanged unless explicit calibration is required.

**STOP for visual review.**

---

# Task D — Implement/refine `A2_01` prompt

Implement:

- title/subtitle
- `AiPromptField`
- 120-char counter
- validation
- deck BACK/NEXT behavior

Do not render duplicate floating back/continue arrows if deck navigation is present.

Tests:

- BACK route
- empty prompt disables NEXT
- prompt persists
- 120-char cap

Capture screenshot and stop if shared-token changes affect A2_00.

---

# Task E — Implement/refine `A2_02` interpretation + controls

Implement:

- exactly 3 read-only analysis blocks
- exactly 5 editable tone controls
- default deterministic fixture values
- monochrome/grey slider treatment with red active/focus signal only
- deck BACK/NEXT
- dial enabled for the currently active/focused tone control according to the interaction contract

No API.
No loading screen.
No chart library.
No icon package.
No semantic multicolor analysis.

Tests:

- analysis is not editable
- exactly 5 tone controls editable
- values persist
- dial changes only active tone control
- dial does nothing if no tone control is active

Capture screenshot.

---

# Task F — Implement/refine `A2_03` result

Implement:

- `AiLetterDocument`
- layered sheet outlines
- exactly 4 `LetterInsights` categories
- `AiRegenerateAction`
- deck BACK/NEXT

Implement at least 3 deterministic result fixtures.

Regenerate must preserve prompt + tone controls.

The deck dial remains visible but neutral/inactive unless explicitly mapped later.

Do not create a fourth physical button for regenerate.

Capture initial and regenerated screenshots.

---

# Task G — Connect shared reflection handoff

Guard:

- Console 1 Human + AI result exists
- Console 2 active result exists

Then wire deck `NEXT` from `A2_03` to the existing first shared reflection screen.

Do not redesign reflection in this task.

---

# Task H — Full AI-only regression pass

Run:

- typecheck
- unit/component tests if configured
- Playwright flow tests
- four canonical AI-only screenshots
- Console 1 smoke/visual tests

Verify:

```text
A2_00 -> A2_01 -> A2_02 -> A2_03 -> reflection
```

Also verify:

- all BACK paths
- regenerate state preservation
- no recipient/relationship repetition
- no Console 1 visual chrome
- stable control-deck geometry across all screens
- no bottom-center MUSE
- no dominant blue
- red markers remain sparse
- A2_00 has both the small persistent identity and the separate oversized `MUSE` display title

---

# Codex behavior rules

Codex must NOT:

- redesign screens because whitespace feels empty
- copy `DIGITAL LOVE LETTER` as product copy
- copy reference-only system IDs
- copy the bottom-center MUSE wordmark
- restore blue as dominant accent
- use red as a large decorative fill
- create a generic header/navigation bar
- add progress UI
- add AI sparkle decoration
- add gradient/glow effects
- install a component library
- change 1440×1080 rendering model
- reuse Console 1 pixel visual components
- use Console 1 glossy red button/gold dial assets
- invent new AI-only screens
- animate anything in the first build
- duplicate BACK/NEXT as both floating links and hardware deck controls
- omit the A2_00 giant MUSE display title because the small identity already exists

## When blocked

If a visual/product requirement is ambiguous:

1. state the ambiguity,
2. identify which reference/document conflicts,
3. explain the smallest definitely-safe implementation,
4. stop before making an irreversible design choice.

Never choose a fashionable default simply to keep coding.

---

# Commit sizing recommendation

Prefer small commits:

```text
refactor(console2): apply refined AI-only tokens and typography
feat(console2): add system control deck
feat(console2): add giant A2_00 MUSE display title
feat(console2): refine welcome screen
feat(console2): refine prompt screen
feat(console2): refine analysis and tone controls
feat(console2): refine letter result and insights
test(console2): update refined visual regressions
```

Do not combine Console 1 visual refactors with Console 2 work unless a genuinely shared infrastructure issue requires it.

---

# PR summary requirements

When ready for review, report:

- AI-only plan files followed
- screenshots generated
- measured deviations from both references
- actual bundled fonts used
- current color tokens
- current deck geometry tokens
- fixture data used
- Console 1 regression status
- intentionally deferred items

---

# Deferred items

Do not pull these into the current visual implementation:

- production AI model calls
- API prompt engineering
- **physical serial/MIDI/Arduino hardware integration**
- animations
- sound
- printer
- handwriting/stamps/doodles/personal letter decoration
- production analytics/error handling

The **on-screen representation** of Console 2 BACK/NEXT buttons and intensity dial is part of the current build. Only real physical hardware wiring is deferred.