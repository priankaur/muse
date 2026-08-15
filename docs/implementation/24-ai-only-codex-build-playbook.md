# 24 — Arcade Console 2 / AI Only — Codex Build Playbook

Use this file to keep implementation incremental and reviewable. Do not ask Codex to build all four screens in one uncontrolled pass.

## Global rule

Every Console 2 task must begin by reading:

1. `AGENTS.md`
2. `docs/implementation/18-ai-only-source-of-truth.md`
3. `docs/implementation/19-ai-only-visual-system.md`
4. the relevant plan for the task
5. `docs/reference/ai-only-console2-canonical.jpg`

Do not use Console 1 screenshots as visual references for Console 2.

---

# Task A — Audit existing code before changing it

Goal: understand the current build and prevent accidental coupling to Console 1.

Codex should:

1. inspect existing stage/session/navigation architecture,
2. list which shared pieces can safely be reused,
3. identify any current assumption that all consoles use the pixel shell,
4. identify current `A2_*` routes/components,
5. identify existing state shape for Arcade 2,
6. report likely refactor points,
7. make no visual changes yet.

Output a concise implementation note before proceeding.

Acceptance:

- no code invented from assumptions,
- no duplicate stage scaler if one already exists,
- no plan to make Console 2 a `MuseWindow` theme.

---

# Task B — Build the Console 2 visual foundation only

Create/implement:

- `aiOnly.tokens.css`
- `AiOnlyShell`
- `AiOnlyIdentity`
- perimeter frame
- typography setup
- `AiNavigation`

Do not implement screen-specific content yet except a temporary blank calibration route.

Render at 1440×1080.

Take screenshot.

STOP for visual review.

Acceptance:

- warm off-white calibrated background,
- correct identity position,
- no screen number,
- thin frame,
- no Console 1 chrome,
- correct font character,
- bottom nav anchors if visible in calibration state.

---

# Task C — Implement A2_00 only

Implement:

- personalized title,
- context-loaded subtitle,
- static `ContextSignal`,
- begin indicator/action.

Do not build A2_01–A2_03 yet.

Capture 1440×1080 screenshot and compare with canonical reference.

STOP.

---

# Task D — Implement A2_01 prompt screen

Implement:

- canonical title/subtitle,
- `AiPromptField`,
- 120-char counter,
- validation,
- back/continue navigation.

Tests:

- empty invalid,
- typed prompt preserved,
- 120-char cap,
- correct routes.

Capture screenshot.

STOP if layout/token changes would affect A2_00 and re-run its screenshot.

---

# Task E — Implement A2_02 interpretation screen

Implement:

- exactly 3 read-only `AnalysisCard`s,
- exactly 5 editable `ToneControl`s,
- default fixture data,
- back/continue state behaviour.

No API.
No loading page.
No chart library.
No icon library.

Tests:

- analysis not editable,
- 5 controls editable,
- values persist through navigation.

Capture screenshot.

---

# Task F — Implement A2_03 result screen

Implement:

- `AiLetterDocument`,
- layered sheet outlines,
- `LetterInsights`,
- exactly 4 insight categories,
- back/regenerate/continue.

Implement at least 3 deterministic result fixtures.

Regenerate must preserve prompt and tone controls.

Capture initial and regenerated screenshots.

---

# Task G — Connect shared reflection handoff

Guard that:

- Console 1 Human + AI result exists,
- Console 2 active result exists.

Then wire `continue` from `A2_03` to the existing first shared reflection screen.

Do not redesign reflection as part of this task.

---

# Task H — Full AI-only regression pass

Run:

- typecheck
- unit/component tests if configured
- Playwright flow tests
- all four canonical screenshot tests
- Console 1 smoke/visual tests to ensure no regression

Verify:

- `A2_00 -> A2_01 -> A2_02 -> A2_03 -> reflection`
- all back paths
- regenerate state preservation
- no recipient/relationship repetition
- no Console 1 chrome mounted in Console 2

---

# Codex behaviour rules during implementation

Codex must NOT:

- redesign a screen because content feels sparse,
- add explanatory copy not present in content config,
- create a generic header bar,
- add a progress indicator,
- add AI sparkle decoration,
- add gradient/glow effects,
- use multiple semantic colors,
- install a component library,
- change the 1440×1080 rendering model,
- reuse Console 1 visual components,
- invent a new AI-only screen,
- merge analysis and result responsibilities differently from the plan,
- animate anything in the first build.

## What Codex should do when blocked

If a visual reference or product behaviour is ambiguous:

1. state the ambiguity,
2. point to the conflicting/missing source,
3. identify the smallest implementation that is definitely safe,
4. stop before making irreversible visual decisions.

Never solve ambiguity by choosing a fashionable default.

---

# Commit/task sizing recommendation

Prefer small commits such as:

```text
feat(console2): add AI-only shell and tokens
feat(console2): implement welcome screen
feat(console2): implement prompt screen
feat(console2): implement analysis and tone controls
feat(console2): implement letter result and insights
test(console2): add AI-only visual regressions
```

Do not combine Console 1 visual refactors with Console 2 implementation unless a genuinely shared stage/session bug requires it.

# Pull request summary requirements

When Console 2 implementation is ready for review, PR/body should state:

- which AI-only plan files were followed,
- screenshots generated,
- any measured deviations from canonical reference,
- font actually used,
- state fixtures used,
- whether Console 1 regression tests still pass,
- any intentionally deferred items.

# Deferred items — do not pull into current tasks

- production AI calls
- API prompt engineering
- hardware controls
- animations
- sound
- printer
- handwriting/stamps/doodles/personal letter decoration
- production analytics/error handling

Those are separate future workstreams.