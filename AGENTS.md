# MUSE — Codex Project Instructions

This repository implements the MUSE physical arcade experience. Treat the visual design as **approved and frozen** unless the user explicitly asks for a design change.

## Read this first

Before editing production code, read these files in order:

1. `docs/implementation/README.md`
2. `docs/implementation/00-source-of-truth.md`
3. `docs/reference/muse-ui-style-system-v2.md`
4. `docs/implementation/01-static-build-scope.md`
5. `docs/implementation/02-technical-architecture.md`
6. The screen-plan file relevant to the task.

The legacy experience file at `docs/reference/muse-experience-flow-legacy.md` is **reference material only**. The newer Human + AI → AI-only experience structure documented in this implementation bundle overrides older Ex-Love / Next Love ordering and naming.

## Non-negotiable design rules

- Do not redesign the interface.
- Do not introduce a new visual language because a screen has different content.
- The same background, HUD, window chrome, typography system, spacing logic, and hardware strip must be reused across screens.
- The main desktop-style content window is rectangular with **sharp 90-degree pixel corners**. Never round the main window.
- The purple title bar is visually blank. Do not add `MUSE SYSTEM` or a page title into the title bar.
- The title bar keeps the yellow menu square on the left and white close square on the right.
- The outer top-left lockup remains `MUSE SYSTEM v1.0 / LOVE LETTERS, REWIRED.` with the pixel heart.
- The outer top-right label remains the console label when specified by the screen plan.
- The window interior uses the same pale, warm, paper-lavender surface across the experience unless a plan explicitly defines a state change.
- The hardware strip is always: **red 3D arcade button — gold 3D rotary dial — red 3D arcade button**.
- Do not restore old footer labels such as `BUTTON`, `KNOB`, `HOLD BOTH`, `SYSTEM MENU`, `CONFIRM / SELECT`, or `BROWSE / ADJUST`.
- Do not restore `Hold Both` as an interaction.
- Use the approved stationery sprite language. Do not add random game motifs.
- Do not add gradients, blur shadows, glassmorphism, soft modern cards, rounded SaaS controls, or generic component-library styling unless a reference explicitly contains it.
- Keep decorative density low. The content window is the hero.

## Current implementation scope

The first build is a **complete static/prototype experience** with all screens and navigation, using stubbed data where later integrations will exist.

For this phase, do not implement:

- AI model calls
- vision/OCR
- camera APIs
- printer integration
- hardware serial/MIDI input
- sound
- animation or sprite floating loops
- analytics
- backend persistence

Build the correct screens and state transitions first. Future integration seams are documented, but they should remain interfaces/stubs only.

## Technology constraints

Use:

- React
- Vite
- TypeScript
- plain CSS, CSS Modules, or a small global CSS token layer
- Playwright for visual and flow regression tests

Do not introduce without explicit approval:

- Next.js
- Tailwind
- Material UI
- Bootstrap
- Chakra
- shadcn
- Framer Motion
- Redux
- a general-purpose design-system package

The interface is custom and reference-driven. Generic UI libraries are likely to create visual drift.

## Rendering model

- The experience is a fixed 4:3 arcade composition.
- Use an internal stage of `1440 × 1080` unless the physical display specification changes.
- Scale the complete stage proportionally to fit the viewport.
- Do not independently reflow/reorder major UI regions for responsive breakpoints.
- Use integer/pixel-aligned positioning wherever possible.
- Pixel-art assets use `image-rendering: pixelated` / nearest-neighbour scaling.

## Implementation rule: shell first

All screens must be compositions of reusable primitives. Never recreate the shell per screen.

Required shared components include:

- `ArcadeStage`
- `ArcadeBackground`
- `OuterHud`
- `FloatingSpriteLayer`
- `MuseWindow`
- `WindowTitleBar`
- `HardwareControlStrip`
- `ArcadeButton3D`
- `RotaryDial3D`
- `PixelDivider`
- `PrimaryCta`
- `PixelTextField`
- `ChoiceTag`
- typography primitives

If a task asks for a new screen, build it inside the existing shell. Do not fork the window or hardware implementation.

## Copy rule

Copy is editable. Layout and component styling are not.

Screen copy, labels, relationship options, prompts, and placeholders must live in configuration/content files rather than being buried in visual components. Components should accept content as props.

## Visual acceptance

When a visual reference exists, use it as a regression target. Before calling a screen complete:

1. Render at the canonical 1440 × 1080 stage.
2. Capture a Playwright screenshot.
3. Compare against the approved reference at the same crop/scale.
4. Fix geometry, type scale, spacing, border thickness, and asset placement rather than compensating with new styling.
5. Confirm no unrelated shared component changed.

## Change discipline

For every task:

1. State which implementation-plan file governs the change.
2. Inspect existing shared components before creating new ones.
3. Make the smallest change that satisfies the screen spec.
4. Run `typecheck`, tests, and relevant visual snapshots.
5. Report changed files and any unresolved reference mismatch.

If a requirement is ambiguous, preserve the locked design and make the smallest reversible implementation. Do not invent new product behaviour to fill gaps.
