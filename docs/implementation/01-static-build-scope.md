# 01 — Static Build Scope

## Objective

Create a complete, navigable implementation of the MUSE experience with every planned screen represented in the locked visual system.

The goal of this phase is to prove:

- the entire experience can be walked end-to-end,
- the design system remains consistent across different content types,
- shared components are reusable,
- session state passes correctly between screens,
- future hardware and AI systems can plug in without redesigning the UI.

## In scope

### Application foundation

- React + Vite + TypeScript project.
- Fixed 1440 × 1080 internal 4:3 stage.
- Proportional stage scaling to browser/exhibition viewport.
- Static local application with no required network service.
- Shared screen registry and deterministic state machine.
- Development deep-link or debug mechanism for opening any screen directly.

### Visual system

- Full arcade world background.
- Outer HUD.
- Sharp-cornered MUSE desktop window.
- Window title-bar controls.
- Pale lavender/paper surface.
- 8-bit/pixel typography roles.
- CTA, text fields, tags, dividers, meters, status cards and letter-preview containers.
- Sparse decorative sprite layer.
- 3D control strip.

### Experience

- Registration mock screen or mocked registration-entry handoff.
- All Arcade 1 Human + AI screens.
- All Arcade 2 AI-only screens.
- Reflection screens.
- Letter comparison.
- Final stance selection.
- Print/token-wall handoff screen.
- Exit/complete state.

### Functional prototype behaviour

- Text entry works locally.
- Choice/tag selection works locally.
- Screen transitions work.
- Back/forward logic works where allowed.
- Session values are stored in memory during the current run.
- Camera screen uses a static placeholder/demo image rather than device access.
- AI screens use deterministic fixture text rather than API calls.
- Analysis screens use deterministic fixture results.
- Printer action is represented by an interface call/stub and UI status only.

## Explicitly out of scope for this phase

Do not implement these yet:

- OpenAI or other model API calls.
- Prompt engineering production pipeline.
- Vision/OCR/handwriting extraction.
- Camera permissions or real capture.
- Physical rotary encoder integration.
- Arcade-button USB/serial/MIDI integration.
- Sound effects or procedural audio.
- Sprite animation or motion loops.
- Printer driver or OS print invocation.
- Email sending.
- Persistent database/session service.
- analytics/telemetry.
- admin/operator dashboard.
- production privacy/retention backend.

## Why this phase is deliberately static

The UI is highly custom and visually constrained. Debugging design accuracy, state logic, hardware, AI, camera and audio simultaneously would make it difficult to identify the cause of problems.

This phase establishes a stable visual and interaction skeleton. Each deferred system will later replace a fixture/stub behind an existing interface.

## Success criteria

The static phase is complete when a visitor can walk the full experience using mouse/keyboard simulation and:

- no screen looks like a new product,
- no screen recreates shared chrome independently,
- all planned information is represented,
- state survives across both arcade sequences,
- Arcade 2 never asks for information that should have been inherited,
- the final reflection can compare the two fixture letters,
- Playwright can complete the main path from start to exit,
- screenshots of reference-backed screens are visually within the accepted baseline tolerance.
