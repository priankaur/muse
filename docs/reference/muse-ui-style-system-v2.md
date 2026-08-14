# MUSE UI Style System — Canonical Arcade Experience

**Status:** canonical visual system for implementation.

This file is the visual source of truth for Codex. The design may only change when the user explicitly approves a design change. Copy can change freely without redesigning the shell.

## 1. Visual direction

MUSE is a warm 8-bit love-letter arcade running inside an early desktop-computer window. It combines:

- deep navy arcade world,
- subtle square pixel grid,
- sparse floating love-letter stationery sprites,
- large sharp-cornered desktop window,
- pale paper-lavender content surface,
- blank purple title bar,
- yellow menu square at left,
- white X square at right,
- chunky pixel typography,
- magenta/purple/yellow UI accents,
- tactile 3D red arcade buttons and a 3D gold rotary dial.

The result must look like a real playable arcade system, not a website with a pixel font.

## 2. Locked composition

Use a fixed 4:3 logical stage at `1440 × 1080`. The entire stage scales proportionally to fit the viewport. Do not independently reflow major elements for responsive breakpoints.

Persistent layers:

1. dark navy grid background,
2. outer HUD / MUSE lockup,
3. sparse stationery sprite layer,
4. centered MUSE desktop window,
5. screen-specific content inside the window,
6. fixed hardware strip below the window.

Everything must be horizontally balanced. Do not allow unexplained empty space to accumulate on one side.

## 3. Main window — non-negotiable

The main content window is the dominant object and must be implemented once as a shared component.

- rectangular silhouette,
- **sharp 90-degree corners**, never rounded,
- heavy dark pixel outline,
- pale warm lavender/paper interior,
- thin hard magenta backplate/extrusion visible on right and bottom,
- no blur shadow,
- no glass effects,
- no modern card styling.

### Title bar

Exact visual structure:

`[yellow menu square][blank purple bar................................][white X square]`

Rules:

- purple title bar contains **no text**,
- do not repeat `MUSE SYSTEM` inside the title bar,
- yellow menu block flush left,
- white close block flush right,
- dark pixel separators/outlines,
- same dimensions on every screen.

## 4. Window surface

Use a warm pale lavender rather than pure white. Starting family:

- `#D0BCDB`
- `#CFBBDA`
- `#CDB9D7`

Add only an extremely subtle paper/fibrous texture. It should feel tactile, not noisy or photographic.

The exact same surface treatment should be used across welcome, form, tuning, reflection and result windows unless an explicit experience-state variant is approved.

## 5. World/background

Starting palette:

- deep navy `#01152F`
- secondary navy `#0A1A37`
- grid `#10294E`

The grid should be visible but quiet. It supports the arcade/system atmosphere without competing with the window.

## 6. Outer HUD

Top-left system lockup stays outside the window. Current canonical lockup:

`MUSE SYSTEM v1.0`

`LOVE LETTERS, REWIRED.`

with a small pixel heart.

When a console identifier is needed, it lives top-right outside the window. It should never become a large panel competing with the content.

## 7. Floating sprite language

Use only love-letter / making-related pixel sprites, for example:

- airmail envelope,
- heart postage stamp,
- paper/note,
- letters folder,
- pen,
- paperclip,
- notebook/diary,
- small hearts,
- tiny sparkles.

A small moon may exist only as a secondary atmospheric object; do not let moons/stars replace the stationery language.

Keep decoration sparse: roughly 4–7 meaningful edge objects plus tiny heart/sparkle punctuation. Mix sizes intentionally. The window remains the hero.

Sprites must be separate transparent assets, not baked into the background or window.

## 8. Typography

Use centralized pixel/bitmap typography roles rather than arbitrary sizes.

Roles:

- `DisplayXL` — hero word such as MUSE,
- `DisplayL` — major question,
- `Greeting` — `HELLO, [USER NAME]`,
- `HeadingM` — section title,
- `BodyPixel` — narrative copy,
- `UiLabel` — form labels,
- `ButtonLabel` — CTA/tag labels,
- `MetaLabel` — HUD/system information.

Major display moments can use uppercase. Longer body copy should prioritize readability and may use sentence casing.

Do not shrink text until it is unreadable just to fit copy. Copy is editable; window geometry is not.

## 9. Primary CTA

Canonical primary CTA:

- wide magenta/hot-pink face,
- dark pixel outline,
- hard pixel depth/extrusion,
- uppercase cream/yellow label,
- sharp/stepped corners,
- horizontally centered.

No rounded pill buttons and no blur shadows.

Pressed state later collapses the hard depth by a few pixels rather than using modern elastic animation.

## 10. Text emphasis

Important emotional phrases in narrative copy can be highlighted with a solid rectangular colour block behind the text.

- use magenta or purple box,
- contrasting text,
- sharp rectangular edges,
- never a rounded pill.

## 11. Forms and tags

### Text field

- pale/cream fill,
- dark purple/navy pixel outline,
- rectangular/pixel-stepped geometry,
- large readable input text,
- obvious focus state,
- no modern rounded input styling.

### Relationship tags

- consistent height,
- cream/pale face,
- purple/dark outline,
- centered pixel label,
- width follows label while preserving rhythm,
- selected/focused state uses colour plus outline/marker, not colour alone.

`Other` reveals/enables its own text field.

## 12. Divider

Canonical divider is a purple horizontal line with a small pixel heart centered in a gap. Build once and reuse.

## 13. Hardware strip — non-negotiable

Every main arcade screen uses the same visual hardware strip:

`[small red 3D arcade button]     [larger gold 3D rotary dial]     [small red 3D arcade button]`

Rules:

- buttons are red and visually identical,
- dial is gold with a visible pointer/notch,
- all three use pixel-built 3D shading/highlights rather than smooth photorealism,
- hardware strip stays centered and spread evenly,
- no text labels,
- no `BUTTON`, `KNOB`, `HOLD BOTH`, `SYSTEM MENU`, `CONFIRM / SELECT`, or `BROWSE / ADJUST` captions.

These controls must be implemented once and reused across screens.

## 14. Layout rhythm

Narrative screens generally use:

1. greeting/title,
2. heart divider,
3. concise centered body,
4. optional solid text highlights,
5. one centered CTA.

Form screens generally use:

1. concise screen title/greeting,
2. divider,
3. numbered/clear question,
4. input/tag group,
5. next question if needed,
6. CTA.

Tuning screens use:

1. parameter name,
2. large discrete pixel meter/value,
3. low/high labels,
4. minimal explanatory copy.

Letter-result screens reduce decorative noise and let the letter dominate.

## 15. Pixel rendering

Pixel assets use nearest-neighbour scaling:

```css
image-rendering: pixelated;
image-rendering: crisp-edges;
```

Avoid fractional logical sizes for small sprites and controls. Do not blur or smooth pixel assets.

## 16. Motion — deferred

Do not implement animation in the first static build. When added later, use stepped low-frame movement:

- gentle sprite bobbing,
- button depth collapse,
- dial frame/tick movement,
- short stepped panel appearances,
- loading increments.

Avoid smooth modern easing and frantic motion.

## 17. Do not reintroduce deprecated elements

- rounded main-window corners,
- `MUSE SYSTEM` text inside the title bar,
- old labelled control footer,
- Hold Both interaction,
- System Menu footer copy,
- dense collage decoration,
- random arcade/game sprites unrelated to letters,
- glassmorphism,
- gradients used as generic modern decoration,
- soft blurred shadows,
- generic SaaS UI,
- flat generic circles replacing the approved 3D controls.

## 18. Visual acceptance checklist

Before approving any screen verify:

- fixed 4:3 arcade composition,
- dark navy grid world,
- central window horizontally balanced,
- sharp 90-degree main-window corners,
- blank purple title bar,
- yellow menu left / white X right,
- consistent lavender paper surface,
- sparse letter-related sprites,
- readable pixel typography,
- one obvious primary action,
- no accidental new component style,
- red button / gold dial / red button strip unchanged,
- no old instructional labels,
- screen is readable from standing distance.

The implementation principle is: **the content evolves; the arcade world does not.**
