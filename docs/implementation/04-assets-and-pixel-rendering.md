# 04 — Assets and Pixel Rendering

## Principle

The design must be assembled from reusable layers and individual assets. Do not flatten the whole UI into a screenshot and place invisible HTML controls over it.

The user explicitly wants background, sprites, window chrome, controls and UI pieces separated so the experience can evolve without repainting the entire screen.

## Asset folders

```text
public/assets/
├── background/
│   └── arcade-grid.png          # optional if CSS grid is not used
├── branding/
│   ├── muse-heart.png
│   └── ...
├── sprites/
│   ├── envelope-airmail.png
│   ├── postage-heart.png
│   ├── note-pink.png
│   ├── folder-yellow.png
│   ├── heart-pink.png
│   ├── moon-yellow.png
│   ├── sparkle-pink.png
│   └── sparkle-purple.png
├── controls/
│   ├── arcade-button-red.png
│   └── rotary-dial-gold.png
├── window/
│   ├── menu-square.png
│   ├── close-square.png
│   └── ...
├── texture/
│   └── lavender-paper.png
└── demo/
    ├── handwritten-letter-01.jpg
    └── ...
```

## Individual files, not sprite sheets for runtime

A concept sheet is useful as an art reference but is inconvenient for implementation. Convert approved sheet elements into individual transparent PNG/WebP assets before production use.

Each runtime sprite should have:

- transparent background,
- tight bounding box,
- no accidental black canvas,
- no baked outer glow,
- no scene background,
- pixel edges preserved.

## Pixel rendering

For pixel assets:

```css
.pixelAsset {
  image-rendering: pixelated;
  image-rendering: crisp-edges;
}
```

Avoid fractional CSS sizes for small assets. Prefer source dimensions that scale by integer multiples at the canonical 1440 × 1080 stage.

Do not apply:

- `filter: blur(...)`,
- soft CSS drop shadows,
- image smoothing,
- continuous transform scaling to individual sprites during the static phase.

The whole stage may scale proportionally for viewport fitting; individual logical asset positions should remain stable inside it.

## Paper-lavender window surface

The window interior should not be flat white.

Implement it as:

1. a stable lavender base colour,
2. an extremely subtle texture asset or CSS image,
3. low enough contrast that body copy remains clean.

The texture must not look like noise, marble, paper grain at photographic resolution, or a modern gradient.

If a texture image is used, repeat it or scale it consistently. The same asset must be used across all main windows.

## Window backplate

The hot-pink right/bottom extrusion can be CSS geometry. Do not bake the main surface, title bar, backplate and content into a single raster asset.

## Hardware assets

The red button and gold rotary dial are locked visual assets.

Use one source asset per control type and scale them identically on every screen. Interactive pressed/rotation states may later use alternate frames, but the static phase should use the same base assets everywhere.

## Sprite layout manifest

Create a typed manifest rather than scattering absolute positions through components.

Example:

```ts
export interface SpritePlacement {
  id: string;
  asset: SpriteAssetKey;
  x: number;
  y: number;
  width: number;
  rotation?: number;
  z?: number;
}
```

Then create layouts such as:

```ts
export const standardArcade1Sprites: SpritePlacement[] = [ ... ];
```

This makes visual consistency reviewable and allows future motion to be added without moving assets into screen components.

## Asset naming

Use semantic names, not generated filenames such as `imagegen-4.png`.

Good:

- `envelope-airmail-heart.png`
- `postage-stamp-heart-purple.png`
- `rotary-dial-gold.png`

Bad:

- `Screenshot 2026-08-14.png`
- `imagegen(3).png`

## Asset audit task

Before screen implementation, Codex should produce an asset-audit table with:

- required asset,
- file path,
- transparent yes/no,
- canonical logical size,
- approved reference source,
- status: ready / needs crop / missing.

Do not silently replace missing approved art with a different icon style. Use an explicit placeholder and report the missing asset.
