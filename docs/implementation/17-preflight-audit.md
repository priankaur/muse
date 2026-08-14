# MUSE Codex Pre-Flight Audit

Before implementing anything, perform a **PRE-FLIGHT AUDIT** of the repository.

The purpose of this step is to verify that Codex has enough visual and implementation context to reproduce the approved MUSE interface faithfully, without filling gaps with its own design decisions.

## Required source-material check

Verify whether the repository contains all of the following:

1. Canonical design-system documentation.
2. `AGENTS.md`.
3. Implementation-plan documents.
4. Canonical window-frame reference image.
5. Approved welcome-screen reference image.
6. Approved form-screen reference image.
7. Separate decorative sprite assets.
8. Red arcade-button asset.
9. Gold rotary-dial asset.
10. Lavender paper/background texture.
11. Heart-divider asset, if the implementation uses one.
12. Chosen display pixel font.
13. Chosen body pixel/mono font.

## Missing-reference policy

Do **not** substitute missing visual references with your own design decisions.

If one or more important visual assets or references are missing:

- do not fabricate them;
- do not generate approximations;
- do not redesign around the missing item;
- report exactly what is missing;
- identify the recommended repository path for each missing asset;
- continue only with work that is independent of those missing assets.

Whenever you are forced to choose between **"looks approximately right"** and **"wait for the reference"**, wait for the reference.

## Required audit output

Create a short `PRE_FLIGHT_REPORT.md` at the repository root containing:

- repository status;
- files found;
- files missing;
- visual ambiguities;
- implementation blockers;
- safe tasks that can proceed;
- tasks that must wait for visual references.

Do not turn this report into a long design document. Its purpose is to make blockers and safe next steps explicit before coding begins.

## Visual authority order

When references conflict, use this order:

1. Latest explicitly approved screenshot.
2. `AGENTS.md`.
3. Canonical UI style-system documentation.
4. Implementation documentation.
5. Older screenshots.
6. Legacy experience-flow documentation.

Never use an older screenshot to override a newer approved design.

## Deprecated visual elements

Older references may contain visual or content patterns that are no longer approved, including:

- rounded or alternate main-window frames;
- old footer labels;
- `HOLD BOTH / SYSTEM MENU`;
- `BUTTON / KNOB` explanatory labels;
- old `Ex-Love` naming;
- duplicated MUSE branding inside the content window;
- generic modern-card treatments;
- old control instructions repeated inside the UI.

Do not restore deprecated elements.

If it is unclear whether an element is current, flag the ambiguity instead of guessing.

## Foundation validation before screen implementation

Before building Screen 01, first implement and validate these reusable primitives:

- `ArcadeStage`;
- `BackgroundGrid`;
- `ExhibitBrand`;
- `ConsoleLabel`;
- `MuseWindow`;
- `WindowTitleBar`;
- `HardwareControls`;
- `SpriteLayer`.

`MuseWindow` and `HardwareControls` must become the **single shared implementation** used by every screen.

Do not duplicate their markup or styling inside individual screens.

## Canonical stage validation

After completing the foundation:

1. render the application at the canonical internal stage size of `1440 × 1080`;
2. capture one deterministic screenshot;
3. compare the shell visually against the latest approved reference;
4. list any remaining visual calibration differences;
5. stop for review.

Do **not** continue to Screen 02 until the shell has been reviewed and approved.

## First-run sequence

The intended first Codex run is:

**audit → scaffold → shell → screenshot → stop**

It is explicitly **not**:

**audit → build every screen → discover the shell is wrong everywhere**

## Core rule

> **The content may change. The visual system must not drift.**
