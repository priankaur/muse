# MUSE Codex Implementation Plan — Index

This folder breaks the implementation into small, durable plans so Codex can work without receiving one giant prompt.

## Goal

Build the complete MUSE two-console experience as a static, navigable React prototype while preserving two intentionally different approved visual systems:

- **Arcade Console 1 — Human + AI:** retro pixel-love-letter arcade / early-desktop UI.
- **Arcade Console 2 — AI Only:** minimal warm-white / black / neutral-grey Swiss-editorial UI with restrained periwinkle accents.

Copy may evolve. Console-specific visual systems are locked.

The current build deliberately postpones animation, production AI calls, camera, printer, audio and physical hardware integration. Stable seams may be created now so those systems can be added later without redesigning screens.

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
| A2-1 | `18-ai-only-source-of-truth.md` | Current product/flow contract and conflict resolution for Console 2. |
| A2-2 | `19-ai-only-visual-system.md` | Exact minimal visual language, tokens, typography, geometry and anti-drift rules. |
| A2-3 | `20-ai-only-component-architecture.md` | Console 2 component boundaries and visual separation from Console 1. |
| A2-4 | `21-ai-only-data-state-interactions.md` | Inherited context, analysis, tone state, regenerate behaviour and fixtures. |
| A2-5 | `22-ai-only-screen-specifications.md` | Detailed 1440×1080 implementation spec for all four canonical screens. |
| A2-6 | `23-ai-only-testing-acceptance.md` | Console 2 screenshots, flow/state tests and approval checklist. |
| A2-7 | `24-ai-only-codex-build-playbook.md` | Exact incremental Codex task sequence. |

Canonical Console 2 image:

- `../reference/ai-only-console2-canonical.jpg`

## Reference files

- `../reference/muse-ui-style-system-v2.md` — Console 1 canonical pixel visual system.
- `../reference/ai-only-console2-canonical.jpg` — Console 2 canonical minimal visual source.
- `../reference/muse-experience-flow-legacy.md` — older narrative reference only.

## Key implementation principle

> **Share the experience infrastructure; do not merge the two visual systems.**

The 1440×1080 stage, state model, semantic navigation and testing utilities can be shared. Console 1 and Console 2 must have distinct visual shells/components.

## Recommended Codex working model

Use `codex/muse-static-experience` for the current static implementation and keep tasks small. Before modifying a console, identify the console-specific plan that governs the work.

Codex should run `17-preflight-audit.md` when repository visual assets/references may be incomplete.

Do not merge partial visual experiments into main. Approved design should land as coherent console-specific systems.