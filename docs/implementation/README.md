# MUSE Codex Implementation Plan — Index

This folder breaks the implementation into small, durable plans so Codex can work without receiving one giant prompt.

## Goal

Build the complete MUSE two-console experience as a React prototype while preserving two intentionally different approved visual systems:

- **Arcade Console 1 — Human + AI:** retro pixel-love-letter arcade / early-desktop UI.
- **Arcade Console 2 — AI Only:** restrained editorial/technical system UI using black, grey, warm off-white and sparse signal red, with its own monochrome physical-control deck.

Copy may evolve. Console-specific visual systems are locked.

The project began as a static-first build. Arcade 1 now has an explicitly approved second phase for scoped motion/sound feedback and a fixture-driven human-letter analysis step. Production AI/vision, camera hardware, printer, real physical control wiring and backend persistence remain deferred unless a later plan explicitly activates them.

## Core canonical read order

| Order | File | Purpose |
|---|---|---|
| 1 | `00-source-of-truth.md` | Resolves old vs new MUSE documents and establishes two distinct console visual systems. |
| 2 | `01-static-build-scope.md` | Defines the original static implementation scope and exclusions; later explicit overrides are documented in files `28`–`30`. |
| 3 | `02-technical-architecture.md` | React architecture, state, stage and build strategy. |
| 4 | `03-design-system-implementation.md` | Console 1 pixel-arcade design-system implementation. |
| 5 | `04-assets-and-pixel-rendering.md` | Console 1 asset/pixel rules. |
| 6 | `05-content-and-data-model.md` | Shared copy/session contracts and stubs. |
| 7 | `06-navigation-and-input-model.md` | Screen state machine and input abstraction. |
| 8 | `07-screen-inventory.md` | Canonical screen IDs and current experience order. |
| 9 | `08-arcade-1-human-ai-screens.md` | Console 1 detailed screens, now including `A1_06A` human-letter analysis. |
| 10 | `09-arcade-2-ai-only-screens.md` | Superseded pointer to the current AI-only bundle; do not implement from old content. |
| 11 | `10-reflection-choice-exit-screens.md` | Shared post-console reflection/comparison/choice. |
| 12 | `11-testing-and-visual-regression.md` | Global visual/flow testing discipline. |
| 13 | `12-accessibility-and-exhibition-mode.md` | Kiosk/readability/accessibility constraints. |
| 14 | `13-implementation-phases.md` | Global phased build order. |
| 15 | `14-codex-task-playbook.md` | General Codex task sizing. |
| 16 | `15-deferred-integrations.md` | Deferred integration tracking plus explicit Arcade 1 motion/sound and analysis exceptions. |
| 17 | `16-definition-of-done.md` | Global completion checklist. |
| 18 | `17-preflight-audit.md` | Repository/visual-source audit before implementation. |

## Arcade 1 — current enhancement bundle

For any new Arcade 1 motion/audio or human-letter analysis work, read these after `AGENTS.md`, `03` and `08`:

| Order | File | Purpose |
|---|---|---|
| A1-E1 | `28-arcade1-motion-audio-interactions.md` | Exact CTA/button/dial/page motion, semantic audio architecture, timings, reduced-motion and testing rules. |
| A1-E2 | `29-arcade1-human-letter-analysis.md` | New `A1_06A` step with sentiment, emotions recognized, human-letter character count and visual meaning. |
| A1-E3 | `30-arcade1-enhancement-build-playbook.md` | Incremental Codex task sequence and stop gates for implementing the two enhancement tracks safely. |

### Arcade 1 enhancement rule

The shell remains frozen. These files add **behavior and one new content responsibility**, not a redesign.

Recommended flow around capture is now:

```text
A1_05 capture
-> A1_06 review
-> A1_06A human-letter analysis
-> A1_07 notes/correction
-> A1_08 tuning
-> A1_09 processing
-> A1_10 result
```

The recognized human-letter character count on `A1_06A` is separate from the 120-character note counter on `A1_07`.

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
| A2-8 | `25-ai-only-a2-00-display-title-refinement.md` | Adds the separate giant editorial `MUSE` display title and A2_00 title hierarchy. |
| A2-9 | `26-ai-only-a2-00-visual-calibration.md` | Latest A2_00 visual calibration after screenshot review. |
| A2-10 | `27-ai-only-a2-01-copy-refinement.md` | Latest A2_01 exhibition-continuation copy authority. |
| A2-11 | `31-ai-only-a2-01-visual-calibration.md` | A2_01 approved composition/readability calibration. |
| A2-12 | `32-ai-only-a2-01-contextual-placeholder.md` | Requires the prompt hint to use one/two short sentences from Arcade 1 context instead of generic stock copy. |
| A2-13 | `33-ai-only-a2-01-contextual-hint-calibration.md` | Latest A2_01 contextual-hint screenshot calibration. |
| **A2-14** | **`34-ai-only-post-generation-analysis-flow.md`** | **LATEST flow override: A2_02 is tone controls only; sentiment/emotion/romance analysis appears only after the AI-only letter is generated on A2_03. This file wins over conflicting analysis timing in files 18/21/22/23/24.** |

For any work on `A2_00`, file `26` is the latest authority. Read `25` for the display-title rationale, then use `26` for the current approved/calibrated composition.

For any work on `A2_01`, files `27`, `31`, `32`, and `33` govern the current copy, visual calibration, contextual hint source, and latest hint calibration.

For any work on `A2_02` or `A2_03`, **read file `34` before implementing**. It is the latest authority for analysis timing and screen responsibility. In particular, do not render sentiment/emotion/romance analysis on A2_02.

## Console 2 reference hierarchy

Use both references:

1. `../reference/ai-only-console2-canonical.jpg` — canonical four-screen content composition and flow except where later explicit product-flow overrides such as file `34` apply.
2. `../reference/ai-only-console2-system-refinement-v2.jpg` — latest and higher authority for visual system/chrome.

Important exclusions from the refinement reference:

- do not copy `DIGITAL LOVE LETTER` as product copy,
- do not copy reference-only system IDs,
- do not add the bottom-center `MUSE` wordmark,
- do not interpret the reference as permission to use Console 1 pixel styling.

## Other reference files

- `../reference/muse-ui-style-system-v2.md` — Console 1 canonical pixel visual system.
- `../reference/muse-experience-flow-legacy.md` — older narrative reference only.

## Key implementation principle

> **Share the experience infrastructure; do not merge the two visual systems.**

The 1440×1080 stage, state model, semantic actions and testing utilities can be shared. Console 1 and Console 2 must have distinct visual shells/components.

## Recommended Codex working model

Use `codex/muse-static-experience` for the current implementation and keep tasks small. Before modifying a console, identify the console-specific plan governing the work.

For the new Arcade 1 enhancement pass, follow `30-arcade1-enhancement-build-playbook.md` and stop after each task gate. Do not implement motion, sound and analysis UI in one uncontrolled commit.

For Console 2, always apply the latest numbered overrides before older generic screen specs. As of this update, `34-ai-only-post-generation-analysis-flow.md` is the latest flow authority for A2_02/A2_03.

Codex should run `17-preflight-audit.md` when repository visual assets/references may be incomplete.

Do not merge partial visual experiments into main. Approved design should land as coherent console-specific systems.
