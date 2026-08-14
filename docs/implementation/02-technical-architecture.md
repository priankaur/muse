# 02 — Technical Architecture

## Stack

Use a deliberately small stack:

- Vite
- React
- TypeScript
- CSS Modules plus one global token/reset stylesheet
- Vitest for unit-level logic if needed
- Playwright for end-to-end and visual regression testing

Avoid framework complexity that does not support the physical arcade use case.

## Proposed repository layout

```text
/
├── AGENTS.md
├── package.json
├── vite.config.ts
├── tsconfig.json
├── playwright.config.ts
├── public/
│   └── assets/
│       ├── background/
│       ├── branding/
│       ├── sprites/
│       ├── controls/
│       ├── window/
│       ├── texture/
│       ├── demo/
│       └── fonts/             # only licensed project fonts supplied by the owner
├── src/
│   ├── app/
│   │   ├── App.tsx
│   │   ├── AppStateProvider.tsx
│   │   ├── screenRegistry.ts
│   │   └── stageScale.ts
│   ├── components/
│   │   ├── arcade/
│   │   ├── window/
│   │   ├── controls/
│   │   ├── form/
│   │   ├── typography/
│   │   └── content/
│   ├── screens/
│   │   ├── registration/
│   │   ├── arcade1/
│   │   ├── arcade2/
│   │   ├── reflection/
│   │   └── exit/
│   ├── content/
│   │   ├── screenCopy.ts
│   │   ├── relationshipOptions.ts
│   │   └── fixtures.ts
│   ├── domain/
│   │   ├── session.ts
│   │   ├── actions.ts
│   │   └── stateMachine.ts
│   ├── integrations/
│   │   ├── ai.ts
│   │   ├── camera.ts
│   │   ├── hardware.ts
│   │   ├── printer.ts
│   │   └── email.ts
│   ├── styles/
│   │   ├── tokens.css
│   │   ├── global.css
│   │   └── pixel.css
│   └── test/
│       └── fixtures/
├── tests/
│   ├── e2e/
│   └── visual/
└── docs/
    ├── implementation/
    └── reference/
```

## Fixed stage model

The arcade is not a responsive web page. It is a fixed composition rendered inside a browser.

Canonical stage:

```ts
export const STAGE_WIDTH = 1440;
export const STAGE_HEIGHT = 1080;
```

The stage should remain at those logical dimensions and scale as one unit.

### Scale calculation

At runtime:

```text
scale = min(viewportWidth / 1440, viewportHeight / 1080)
```

Apply the resulting scale to the full stage. Center it in the viewport. Any remaining area outside the 4:3 composition can use the deep navy base colour.

Do not let the browser independently wrap tags, move the control strip, resize the window, or reorder content because the viewport changes.

## Root component tree

```text
App
└── AppStateProvider
    └── ArcadeStage
        ├── ArcadeBackground
        ├── OuterHud
        ├── FloatingSpriteLayer
        ├── ActiveScreen
        │   └── MuseWindow
        │       └── screen-specific content
        └── HardwareControlStrip
```

`ArcadeStage`, `OuterHud`, `MuseWindow`, and `HardwareControlStrip` must not be duplicated by screens.

## Screen registry

Use stable string IDs, not array indexes.

Example:

```ts
export type ScreenId =
  | 'REG_01'
  | 'A1_00'
  | 'A1_01'
  | 'A1_02'
  | 'A1_03'
  | 'A1_04'
  | 'A1_05'
  | 'A1_06'
  | 'A1_07'
  | 'A1_08'
  | 'A1_09'
  | 'A1_10'
  | 'A1_11'
  | 'A2_00'
  | 'A2_01'
  | 'A2_02'
  | 'A2_03'
  | 'A2_04'
  | 'A2_05'
  | 'R_01'
  | 'R_02'
  | 'R_03'
  | 'R_04'
  | 'R_05'
  | 'R_06'
  | 'R_07'
  | 'R_08';
```

The registry defines component, previous/next rules, console context, and debug title.

## Navigation

Do not use browser-history semantics as the primary state model. This is a kiosk flow.

Use explicit actions such as:

- `GO_NEXT`
- `GO_BACK`
- `CONFIRM`
- `FOCUS_NEXT`
- `FOCUS_PREVIOUS`
- `ADJUST_UP`
- `ADJUST_DOWN`
- `TEXT_SUBMIT`

A central reducer/state machine decides whether the action is valid on the current screen.

## Development deep-link

For rapid visual iteration, support a development-only query such as:

`/?screen=A1_02&debug=1`

This should seed deterministic fixture state so Codex can open a screen without walking the whole experience.

Never expose debug chrome in production/exhibition mode.

## Integration boundaries

Every deferred external system gets an interface immediately, with a fixture implementation:

```ts
interface AiService { ... }
interface CameraService { ... }
interface HardwareService { ... }
interface PrinterService { ... }
interface MailService { ... }
```

The screen talks to the interface, not to a concrete API. The static phase injects local fixtures.

## Error strategy

The static prototype should not silently fail.

Provide an internal recoverable error state for:

- missing required session data,
- invalid screen deep-link,
- missing fixture result,
- incomplete relationship selection,
- required text field left empty.

Do not invent an unrelated visual treatment for errors. Use the same window system and a simple pixel alert block.
