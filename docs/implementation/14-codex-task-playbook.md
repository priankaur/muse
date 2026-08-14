# 14 — Codex Task Playbook

Use small, verifiable Codex tasks. Each task should have one visual or architectural responsibility and an objective acceptance check.

## Worktree strategy

Recommended first worktree/branch:

`codex/muse-static-experience`

Keep Phase 0–5 in this branch until the shell and first reference screens are accepted. This avoids parallel agents creating competing versions of the same design system.

After the shell is frozen, parallel worktrees may be used for:

- Arcade 1 remaining screens,
- Arcade 2 screens,
- reflection screens,
- tests.

They must all depend on the same shared shell commit.

## Task template

Every Codex prompt should include:

```text
Read AGENTS.md and the relevant docs/implementation plan before editing.
Do not redesign shared chrome.
Implement only the task below.
Run typecheck/tests and capture the specified screenshot.
Report changed files and reference mismatches.
```

## Task 1 — Scaffold

```text
Read AGENTS.md and docs/implementation/01-static-build-scope.md plus 02-technical-architecture.md.
Scaffold/normalize the project to React + Vite + TypeScript.
Add the fixed 1440x1080 ArcadeStage and proportional viewport scaling.
Do not build visual chrome yet.
Add Playwright and a smoke test that verifies the stage renders.
```

Acceptance:

- app runs,
- stage is fixed 4:3,
- typecheck passes.

## Task 2 — Tokens/background/HUD

```text
Implement the global tokens, dark navy grid background, top-left MUSE lockup, top-right console label API, and static FloatingSpriteLayer.
Use docs/implementation/03-design-system-implementation.md and 04-assets-and-pixel-rendering.md.
Do not create the content window yet.
Capture a 1440x1080 screenshot.
```

## Task 3 — Window chrome

```text
Implement MuseWindow and WindowTitleBar only.
Match the approved blank window-frame reference exactly.
The main frame must use sharp 90-degree corners.
The purple title bar must be blank.
Keep the yellow menu square on the left, white X square on the right, pale lavender textured surface, heavy dark outline, and pink right/bottom backplate.
Do not add screen content.
Add a visual regression snapshot for the window component.
```

This is a hard approval gate.

## Task 4 — Hardware strip

```text
Implement the shared HardwareControlStrip with one red 3D arcade button on the left, one gold 3D rotary dial centered, and one identical red 3D arcade button on the right.
No text labels or extra controls.
Use the approved assets/reference.
Add a visual snapshot.
```

## Task 5 — UI primitives

```text
Implement typography roles, PixelHeartDivider, PrimaryCta, PixelTextField, ChoiceTag, RichTextHighlight and LetterPreview.
Create a development-only component gallery route and visual snapshot.
Do not implement product screens yet.
```

## Task 6 — A1_01 greeting reference

```text
Implement A1_01 using only the shared shell and primitives.
Use the current Hello [User Name] reference as the visual target.
Body copy must come from content config.
CTA copy must come from content config.
Do not modify MuseWindow or HardwareControlStrip unless the reference proves a shared-token issue; if you do, explain the change and rerun their snapshots.
```

## Task 7 — A1_02 recipient form

```text
Implement A1_02 recipient/relationship form.
Use the approved relationship reference.
Add real local text input, relationship selection, Other free-text behaviour and validation.
Use shared tag/input/CTA components.
Add visual and interaction tests.
```

## Task 8 — State machine

```text
Implement the ScreenId registry, MuseSession state and semantic actions described in docs/implementation/05-content-and-data-model.md and 06-navigation-and-input-model.md.
Wire A1_00/A1_01/A1_02 through the registry.
Add dev deep-link ?screen=A1_02 that seeds fixture state.
```

## Task 9 — Remaining Arcade 1

Split this into 2–3 tasks rather than one huge request:

- human-writing/camera block (`A1_03`–`A1_06`),
- notes/tuning/processing (`A1_07`–`A1_09`),
- result/handoff (`A1_10`–`A1_11`).

Each task must reuse the shell.

## Task 10 — Arcade 2

Split into:

- welcome/prompt/analysis,
- intensity/generation/result.

Verify recipient/relationship data are inherited and not requested again.

## Task 11 — Reflection

Split into:

- reflection Q1–Q5,
- letter comparison,
- final stance and completion.

## Task 12 — Full flow test

```text
Add one Playwright test that walks the complete fixture experience from registration seed to R_08.
Cover the Other relationship and camera-retake branches in separate tests.
Do not update visual baselines unless a reviewed design change requires it.
```

## Codex review request template

After a milestone:

```text
Review the current branch against AGENTS.md and docs/implementation/00-source-of-truth.md.
Look specifically for design drift, duplicated shell components, rounded main-window corners, title-bar text, old footer labels, repeated recipient questions in Arcade 2, hard-coded copy inside visual components, and inconsistent control-strip assets.
Report findings first. Do not change code until findings are listed.
```
