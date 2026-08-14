# 03 — Design System Implementation

This file translates the canonical MUSE visual system into code structure. It does not replace `docs/reference/muse-ui-style-system-v2.md`; it tells Codex how to implement it without visual drift.

## CSS token strategy

Create `src/styles/tokens.css`. All recurring visual values should have named tokens.

Recommended categories:

```css
:root {
  /* stage */
  --stage-w: 1440px;
  --stage-h: 1080px;

  /* world */
  --world-navy: #01152f;
  --world-navy-2: #0a1a37;
  --world-grid: #10294e;

  /* window */
  --window-surface: #d0bcdb;
  --window-surface-2: #cdb9d7;
  --window-bar: #523286;
  --window-backplate: #e72f77;
  --window-ink: #090f34;

  /* accent */
  --pink: #e63d78;
  --pink-dark: #b21e55;
  --purple: #6339ac;
  --yellow: #f6bb2a;
  --cream: #f8efda;
  --red-control: #e62b22;

  /* borders */
  --stroke-main: 5px;
  --stroke-heavy: 7px;

  /* spacing */
  --space-1: 8px;
  --space-2: 12px;
  --space-3: 16px;
  --space-4: 24px;
  --space-5: 32px;
  --space-6: 48px;
}
```

Values are starting tokens. Tune them against approved reference overlays and then keep the tuned values fixed.

## Component hierarchy

### `ArcadeStage`

Responsibilities:

- owns 1440 × 1080 logical coordinate space,
- applies stage scale,
- clips overflow,
- establishes stacking contexts.

It must not know specific screen content.

### `ArcadeBackground`

Responsibilities:

- deep navy base,
- subtle square grid,
- no content.

Prefer CSS grid lines or one exact approved background asset. Do not combine floating sprites into the background texture.

### `OuterHud`

Contains only persistent outer information:

- top-left brand lockup,
- top-right console label when the current screen requires it.

The HUD is outside the desktop window.

### `FloatingSpriteLayer`

Uses absolute-positioned individual assets. For the static phase, sprites do not animate.

Sprite position belongs to a screen/layout configuration object rather than the sprite component itself.

### `MuseWindow`

The most important locked component.

Requirements:

- rectangular silhouette,
- sharp 90-degree corners,
- heavy dark/black pixel outline,
- pale textured lavender interior,
- thin/hard magenta backplate visible on right/bottom,
- no blurred shadow,
- consistent width/height family.

Do not implement `border-radius` on the main window.

The content area must be a child slot. Never paste the frame image behind full-screen text and call that the component; keep content semantic and editable.

### `WindowTitleBar`

Exact structure:

```text
[yellow menu square][purple blank bar................................][white X square]
```

Rules:

- title bar is one horizontal row,
- yellow square flush to the left border,
- white square flush to the right border,
- purple bar fills the remaining width,
- black/dark border separates controls and bar,
- no text in the purple bar,
- menu/X visuals use the approved pixel construction.

### `HardwareControlStrip`

Exact visible sequence:

```text
[red 3D arcade button]      [gold rotary dial]      [red 3D arcade button]
```

Rules:

- same dimensions and spacing on every screen,
- no text labels,
- no instruction captions,
- no Hold Both cluster,
- no System Menu label,
- no alternate control artwork per screen.

The strip is visual and interactive, but screen-specific action mapping is handled by the input layer.

## Window layout grid

Use a consistent internal content frame rather than per-screen arbitrary positioning.

Suggested slots:

```text
content top padding
heading region
optional divider
primary content region
secondary/options region
CTA region
content bottom padding
```

Narrative and form screens can use different sub-layout components but share the same outer content bounds.

## Typography roles

Do not use a single font size everywhere.

Define semantic classes/components:

- `DisplayXL` — hero word such as MUSE.
- `DisplayL` — major question/heading.
- `HeadingM` — section heading.
- `Greeting` — `HELLO, [USER NAME]` style.
- `BodyPixel` — narrative body.
- `UiLabel` — form/helper label.
- `ButtonLabel` — CTA and tag label.
- `MetaLabel` — small HUD/system copy.

Font family decisions must be centralized. If the exact final pixel font is not yet supplied, use a clearly named temporary slot and do not proliferate substitutes across components.

## Primary CTA

Visual language:

- hot pink/magenta face,
- dark outline,
- hard pixel extrusion/depth,
- uppercase yellow/cream pixel label,
- wide horizontal shape,
- sharp/stepped corners consistent with the approved button.

States:

- default,
- focused,
- pressed,
- disabled.

No blur shadow. Pressed state should collapse the hard extrusion by a few logical pixels rather than animate elastically.

## Text fields

- cream/pale fill,
- dark/purple pixel outline,
- rectangular or subtly pixel-stepped corners,
- no modern rounded input radius,
- visible block caret/focus state,
- text size large enough for arcade distance.

## Relationship/choice tags

- consistent height across a row,
- cream face,
- dark/purple outline,
- centered label,
- width can vary for label length while preserving row rhythm,
- selected/focused state must use more than colour alone.

Selected state can use:

- pink face + dark border,
- small pixel heart/check marker,
- or inverse treatment defined once in the component.

## Divider

The canonical divider is a purple horizontal rule with a small pixel heart centered in the gap.

Build it once as `PixelHeartDivider`.

## Narrative emphasis

Highlighted words in narrative copy may use a solid rectangular accent box behind the word/phrase. Use the exact highlight style from the approved greeting reference:

- solid magenta or purple block,
- contrasting text,
- no rounded pill styling.

## Z-index contract

Suggested order:

1. background grid
2. tiny outer sprites
3. HUD
4. large edge sprites
5. window backplate
6. main window
7. screen content
8. hardware strip
9. development-only overlay

No sprite may overlap critical form fields or the CTA unless the reference explicitly shows that overlap.
