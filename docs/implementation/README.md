# MUSE Codex Implementation Plan — Index

This folder breaks the implementation into small, durable plans so Codex can work without receiving one giant prompt.

## Goal

Build the complete MUSE two-console experience as a static, navigable React prototype while preserving two intentionally different approved visual systems:

- **Arcade Console 1 — Human + AI:** retro pixel-love-letter arcade / early-desktop UI.
- **Arcade Console 2 — AI Only:** restrained editorial/technical system UI using black, grey, warm off-white and sparse signal red, with its own monochrome physical-control deck.

Copy may evolve. Console-specific visual systems are locked.

The current build deliberately postpones animation, production AI calls, camera, printer, audio and **real physical hardware integration**. The on-screen Console 2 BACK/NEXT buttons and intensity dial are part of the current visual build; only their real serial/MIDI/Arduino wiring is deferred.

## Core canonical read order

| Order | File | Purpose |
|---|---|---|
| 1 | `00-source-of-truth.md` | Resolves old vs new MUSE documents and establishes two distinct console visual systems. |
| 2 | `01-static-build-scope.md` | Defines what the current static implementation phase includes/excludes. |
| 3 | `02-technical-architecture.md` | React architecture, state, stage and build strategy. |
| 4 | `03-design-system-implementation.md` | Console 1 pixel-arcade design-system implementation. |
| 5 | `04-assets-and-pixel-rendering.md` | Console 1 asset/pixel rules. |
| 6 | `05-content-and-data-model.md` | Shared copy/session contracts and stubs. |
| 7 | `06-navigation-and-input-model.md` | Screen state machine and input abstraction. |
| 8 | `07-screen-inventory.md` | Canonical screen IDs and current experience order. |
| 9 | `08-arcade-1-human-ai-screens.md` | Console 1 detailed screens. |
| 10 | `09-arcade-2-ai-only-screens.md` | Superseded pointer to the current AI-only bundle; do not implement from old content. |
| 11 | `10-reflection-choice-exit-screens.md` | Shared post-console reflection/comparison/choice. |
| 12 | `11-testing-and-visual-regression.md` | Global visual/flow testing discipline. |
| 13 | `12-accessibility-and-exhibition-mode.md` | Kiosk/readability/accessibility constraints. |
| 14 | `13-implementation-phases.md` | Global phased build order. |
| 15 | `14-codex-task-playbook.md` | General Codex task sizing. |
| 16 | `15-deferred-integrations.md` | Later AI/hardware/camera/printer/sound/animation seams. |
| 17 | `16-definition-of-done.md` | Global completion checklist. |
| 18 | `17-preflight-audit.md` | Repository/visual-source audit before implementation. |

## Console 2 — AI Only canonical bundle

For **any `A2_*` task**, read these after `AGENTS.md` and `00-source-of-truth.md`:

| Order | File | Purpose |
|---|---|---|
| A2-1 | `18-ai-only-source-of-truth.md` | Current product/flow contract and reference precedence for Console 2. |
| A2-2 | `19-ai-only-visual-system.md` | Current black/grey/off-white/red visual language, typography, rules, deck geometry and anti-drift rules. |
| A2-3 | `20-ai-only-component-architecture.md` | Console 2 component boundaries, control-deck architecture and visual separation from Console 1. |
| A2-4 | `21-ai-only-data-state-interactions.md` | Inherited context, analysis, tone state, regenerate behaviour and fixtures. |
| A2-5 | `22-ai-only-screen-specifications.md` | Detailed 1440×1080 specs for all four screens using the refined shell/deck. |
| A2-6 | `23-ai-only-testing-acceptance.md` | Screenshot, geometry, control-state, flow/state and visual approval criteria. |
| A2-7 | `24-ai-only-codex-build-playbook.md` | Exact incremental Codex task sequence. |
| A2-8 | `25-ai-only-a2-00-display-title-refinement.md` | Latest reviewed override for A2_00: separate giant editorial `MUSE` display title, status-marker hierarchy and screenshot stop gate. |

**Important:** for any work on `A2_00`, file `25` is the latest authority and overrides the earlier A2_00 composition in file `22` where they conflict.

## Console 2 reference hierarchy

Use both references:

1. `../reference/ai-only-console2-canonical.jpg` — canonical **four-screen content composition and flow**.
2. `../reference/ai-only-console2-system-refinement-v2.jpg` — **latest and higher authority for visual system/chrome**: heavy typography, black/grey/off-white/red palette, red square markers, horizontal separators and the lower BACK/NEXT/dial deck.

Important exclusions from the refinement reference:

- do not copy `DIGITAL LOVE LETTER` as product copy,
- do not copy reference-only system IDs,
- do not add the bottom-center `MUSE` wordmark,
- do not interpret the reference as permission to use Console 1 pixel styling.

The latest A2_00 review clarified one additional point: the refinement reference's oversized headline is not merely a font sample. `A2_00` requires a **separate oversized `MUSE` display title in the main field**, in addition to the small persistent top-left identity. See file `25`.

## Other reference files

- `../reference/muse-ui-style-system-v2.md` — Console 1 canonical pixel visual system.
- `../reference/muse-experience-flow-legacy.md` — older narrative reference only.

## Key implementation principle

> **Share the experience infrastructure; do not merge the two visual systems.**

The 1440×1080 stage, state model, semantic actions and testing utilities can be shared. Console 1 and Console 2 must have distinct visual shells/components.

## Recommended Codex working model

Use `codex/muse-static-experience` for the current static implementation and keep tasks small. Before modifying a console, identify the console-specific plan governing the work.

For the current Console 2 refinement, follow `24-ai-only-codex-build-playbook.md`. For `A2_00`, also read and obey `25-ai-only-a2-00-display-title-refinement.md`, then stop for visual review before moving to later screens.

Codex should run `17-preflight-audit.md` when repository visual assets/references may be incomplete.

Do not merge partial visual experiments into main. Approved design should land as coherent console-specific systems.