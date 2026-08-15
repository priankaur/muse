# MUSE Codex Pre-Flight Audit

Before implementing visual work, perform a **PRE-FLIGHT AUDIT** for the specific console being changed.

MUSE has two intentionally different visual systems. The audit must confirm that Codex is using the correct references and is not blending them.

## Shared required checks

Verify:

1. `AGENTS.md` exists and has been read.
2. `docs/implementation/00-source-of-truth.md` exists and has been read.
3. `docs/implementation/README.md` points to the current console-specific plans.
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
9. `docs/reference/ai-only-console2-system-refinement-v2.jpg`
10. typography implementation that can support:
   - heavy condensed neo-grotesk display/identity,
   - neutral Swiss/neo-grotesk content,
   - mono/semi-mono system/control labels.

Also inspect the existing Console 2 implementation for obsolete assumptions from the earlier visual direction:

- periwinkle/blue default accent tokens
- floating `← back` / `continue →` as persistent navigation
- large rounded outer stage/card treatment
- absence of the refined lower control deck
- light/regular `MUSE` identity weight

Console 2 visual blockers include a missing reference, missing plan bundle, or an architecture that only supports the Console 1 pixel shell.

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

1. Latest explicitly approved console-specific reference.
2. `AGENTS.md`.
3. Console-specific implementation bundle.
4. Older style documents.
5. Older screenshots.
6. Legacy flow documents.

For Console 2 specifically:

- original four-screen reference = content composition authority
- system-refinement-v2 reference = latest visual/chrome authority

Never use a Console 1 screenshot as a visual source for Console 2 or vice versa.

## Deprecated cross-console assumptions

Do not assume:

- every MUSE screen uses `MuseWindow`;
- Console 2 uses Console 1's glossy red/gold/red hardware strip;
- Console 2 is a color variant of Console 1;
- one typography system applies to both consoles;
- one card/button language applies to both consoles.

Console 2 **does** now contain its own on-screen physical-control deck. That is not cross-console sharing.

## Foundation validation — Console 1

Validate shared pixel primitives before multiplying screens:

- stage/background/HUD
- `MuseWindow`
- title bar
- sprite layer
- Console 1 hardware strip

Capture 1440×1080 screenshot and stop for review.

## Foundation validation — Console 2

Follow `24-ai-only-codex-build-playbook.md`:

1. audit current Console 2 code,
2. apply the refined black/grey/off-white/red token system,
3. implement/refine `AiOnlyShell`, `AiOnlyIdentity`, `SignalMarker`, rules and typography,
4. implement the persistent `AiControlDeck` with outlined BACK/NEXT buttons and right intensity dial,
5. confirm no bottom-center MUSE exists,
6. render exactly 1440×1080,
7. capture stage-only screenshot,
8. stop for visual review before multiplying changes across all screens.

## Core rule

> **Share infrastructure where appropriate. Never merge the two visual languages.**