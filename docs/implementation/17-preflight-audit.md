# MUSE Codex Pre-Flight Audit

Before implementing visual work, perform a **PRE-FLIGHT AUDIT** for the specific console being changed.

MUSE now has two intentionally different visual systems. The audit must confirm that Codex is using the correct references and is not blending them.

## Shared required checks

Verify:

1. `AGENTS.md` exists and has been read.
2. `docs/implementation/00-source-of-truth.md` exists and has been read.
3. `docs/implementation/README.md` exists and points to the current console-specific plans.
4. fixed stage architecture supports `1440 × 1080` / `4:3`.
5. relevant route/session/navigation code has been inspected before adding duplicates.

# Console 1 — Human + AI preflight

Verify presence of:

- `docs/reference/muse-ui-style-system-v2.md`
- latest approved Console 1 window-frame visual reference if available
- latest approved Console 1 welcome reference if available
- latest approved Console 1 form reference if available
- decorative pixel sprite assets
- red arcade-button asset
- gold rotary-dial asset
- lavender paper/background texture
- selected pixel typography strategy

If those visual sources are missing, do not fabricate replacements.

# Console 2 — AI Only preflight

For any `A2_*` implementation, verify presence/readability of:

1. `docs/implementation/18-ai-only-source-of-truth.md`
2. `docs/implementation/19-ai-only-visual-system.md`
3. `docs/implementation/20-ai-only-component-architecture.md`
4. `docs/implementation/21-ai-only-data-state-interactions.md`
5. `docs/implementation/22-ai-only-screen-specifications.md`
6. `docs/implementation/23-ai-only-testing-acceptance.md`
7. `docs/implementation/24-ai-only-codex-build-playbook.md`
8. `docs/reference/ai-only-console2-canonical.jpg`
9. typography implementation matching the approved neutral Swiss/neo-grotesk target

Console 2 visual blockers include a missing canonical image, missing AI-only plan bundle, or an architecture that only supports the Console 1 pixel shell.

## Missing-reference policy

Do **not** substitute missing visual references with your own design decisions.

If an important source is missing:

- do not fabricate it;
- do not generate an approximation;
- do not borrow a visual reference from the other console;
- report exactly what is missing;
- identify the recommended repository path;
- proceed only with work independent of the missing source.

Whenever forced to choose between **"looks approximately right"** and **"wait for the reference"**, wait for the reference.

## Required audit output

Create/update `PRE_FLIGHT_REPORT.md` containing:

- target console
- repository status
- files found
- files missing
- visual ambiguities
- architecture conflicts
- implementation blockers
- safe tasks that can proceed
- tasks that must wait

Keep it concise and actionable.

## Visual authority order

1. Latest explicitly approved console-specific screenshot/reference.
2. `AGENTS.md`.
3. Console-specific implementation bundle.
4. Older style documents.
5. Older screenshots.
6. Legacy flow documents.

Never use a Console 1 screenshot as a visual source for Console 2 or vice versa.

## Deprecated cross-console assumptions

Do not assume:

- every MUSE screen uses `MuseWindow`;
- every MUSE screen has the red/gold/red hardware strip rendered on-screen;
- Console 2 is a color variant of Console 1;
- one typography system applies to both consoles;
- one card/button language applies to both consoles.

## Foundation validation — Console 1

Validate shared pixel primitives before multiplying screens:

- stage/background/HUD
- `MuseWindow`
- title bar
- sprite layer
- hardware strip

Capture 1440×1080 screenshot and stop for review.

## Foundation validation — Console 2

Follow `24-ai-only-codex-build-playbook.md`:

1. audit existing architecture,
2. build `AiOnlyShell` + tokens + identity + frame + navigation only,
3. render 1440×1080,
4. capture screenshot,
5. stop for review before multiplying AI-only screens.

## Core rule

> **Share infrastructure where appropriate. Never merge the two visual languages.**