# MUSE Codex Implementation Plan — Index

This folder breaks the implementation into small, durable plans so Codex can work on the project without receiving one giant prompt.

## Goal

Build the complete MUSE arcade experience as a static, navigable React prototype that reproduces the approved pixel-arcade design system consistently across every screen. The design system is locked; copy may evolve.

The current build deliberately postpones animation, AI, camera, printer, audio, and physical hardware integration. Those systems receive stable interfaces now so they can be added later without redesigning the screens.

## Canonical read order

| Order | File | Purpose |
|---|---|---|
| 1 | `00-source-of-truth.md` | Resolves old vs new MUSE documents and defines what wins when references conflict. |
| 2 | `01-static-build-scope.md` | Defines exactly what this implementation phase includes and excludes. |
| 3 | `02-technical-architecture.md` | Project structure, React architecture, state management, routing, staging and build strategy. |
| 4 | `03-design-system-implementation.md` | Turns the approved visual language into components and CSS tokens. |
| 5 | `04-assets-and-pixel-rendering.md` | Asset folders, sprite rules, nearest-neighbour rendering, texture treatment and asset manifest. |
| 6 | `05-content-and-data-model.md` | Copy separation, session data, screen content contracts and stubs. |
| 7 | `06-navigation-and-input-model.md` | Screen state machine, keyboard simulation and future hardware abstraction. |
| 8 | `07-screen-inventory.md` | Canonical screen IDs and complete experience order. |
| 9 | `08-arcade-1-human-ai-screens.md` | Detailed screen specs for the first Human + AI arcade. |
| 10 | `09-arcade-2-ai-only-screens.md` | Detailed screen specs for the AI-only arcade experience. |
| 11 | `10-reflection-choice-exit-screens.md` | Reflection, comparison, stance, print handoff and exit screens. |
| 12 | `11-testing-and-visual-regression.md` | Playwright, screenshot baselines, flow tests and regression discipline. |
| 13 | `12-accessibility-and-exhibition-mode.md` | Readability, focus states, kiosk behaviour, failure recovery and exhibition constraints. |
| 14 | `13-implementation-phases.md` | Exact phased build order and acceptance gates. |
| 15 | `14-codex-task-playbook.md` | Ready-to-use Codex task prompts and task sizing rules. |
| 16 | `15-deferred-integrations.md` | Later animation, AI, camera, printer, sound and physical control integration seams. |
| 17 | `16-definition-of-done.md` | Global and per-screen completion checklist. |
| 18 | `17-preflight-audit.md` | Mandatory repository/visual-source audit before implementation begins. |

## Reference files

- `../reference/muse-ui-style-system-v2.md` — canonical visual system.
- `../reference/muse-experience-flow-legacy.md` — older experience narrative; useful for interaction details but not canonical for current station ordering.

## Key implementation principle

> **The shell is frozen. Only screen content and state change.**

The same arcade world must remain recognisable on every screen. New questions do not justify new chrome, new window geometry, new control styling, or a new layout language.

## Recommended Codex working model

Use one worktree/branch for the static experience foundation and then keep tasks small inside it until the shell is stable. After the shell is approved, additional worktrees can handle isolated areas such as screen implementation, tests, or future integrations.

Suggested planning branch/worktree name:

`codex/muse-static-experience`

Before writing code, Codex should run the process defined in `17-preflight-audit.md` and create a root `PRE_FLIGHT_REPORT.md`.

Do not merge partial visual experiments into the main branch. The approved design should land as a coherent system, not as unrelated per-screen implementations.
