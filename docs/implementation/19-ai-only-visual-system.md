# 19 — Arcade Console 2 / AI Only — Visual System Specification

This file translates the canonical AI-only reference into implementation rules. It is intentionally prescriptive. Do not improvise a generic minimal dashboard.

Canonical reference:

`docs/reference/ai-only-console2-canonical.jpg`

## 1. Design character

Console 2 should feel like a quiet computational instrument or editorial system page:

- sparse
- measured
- neutral
- highly legible
- deliberate
- unemotional
- almost document-like

It is **not**:

- a SaaS dashboard
- a futuristic AI interface
- glassmorphism
- terminal UI
- brutalism
- Apple-style glossy minimalism
- retro computing
- pixel art

## 2. Stage geometry

Internal stage is always:

```css
--stage-width: 1440px;
--stage-height: 1080px;
```

All screen geometry below is specified in that coordinate space.

### Stage scaling

Use a single scale transform calculated from viewport dimensions:

```ts
scale = Math.min(viewportWidth / 1440, viewportHeight / 1080)
```

The stage is centered. Do not independently responsive-reflow inner content.

## 3. Outer frame

The reference has a nearly invisible perimeter line. Preserve it as a subtle container boundary, not as arcade chrome.

```css
--ai-frame-inset: 20px;
--ai-frame-border: 1px;
--ai-frame-radius: 8px;
```

Frame:

- inset 20px from each stage edge
- 1px neutral line
- 8px radius maximum
- no fill different from stage
- no shadow
- no inner shadow
- no bevel

The small screen numbers shown in the montage are removed.

## 4. Color tokens

These values are sampled/calibrated from the supplied canonical screenshot and are the starting production values.

```css
:root {
  --ai-bg: #E1DDD8;
  --ai-surface: #E6E3DE;
  --ai-ink: #10100F;
  --ai-ink-secondary: #42413F;
  --ai-ink-muted: #797774;
  --ai-line: #C3C0BD;
  --ai-line-soft: #D6D2CE;
  --ai-accent: #7184CA;
  --ai-accent-mid: #8492CD;
  --ai-accent-soft: #9FA8D1;
  --ai-accent-faint: #BBBFD9;
}
```

### Color discipline

- `--ai-bg` is the dominant stage color.
- Never replace `--ai-bg` with pure `#FFF`.
- `--ai-ink` is primary text and strong borders.
- Accent blue is functional only: active navigation, slider fill/thumb, key insight values, small analytical icons.
- No additional accent colors.
- Sentiment/emotion/romance do **not** receive semantic green/red/pink colors.
- Avoid large blue surfaces.

If a screenshot regression reveals a measurable mismatch caused by display capture/compression, adjust the token once globally; do not patch individual screens with new colors.

## 5. Typography

### Target character

Use a neutral Swiss / neo-grotesk sans-serif with:

- low visual personality
- clean lowercase
- even strokes
- compact punctuation
- strong small-size legibility
- no geometric-tech styling
- no rounded friendly forms

### Initial implementation font

Preferred open-source bundled substitute: **Liberation Sans**.

Implementation order:

1. If a licensed/local project font is later provided, replace through the token only.
2. For current build, bundle/import Liberation Sans if the project can do so without runtime network dependency.
3. Fallback stack:

```css
font-family: "Liberation Sans", Arial, "Helvetica Neue", Helvetica, sans-serif;
```

Do not independently choose Inter, Poppins, Montserrat, Space Grotesk, DM Sans, Roboto Mono or another fashionable UI font.

### Font roles

```css
--ai-font-hero: 64px;
--ai-line-hero: 0.98;
--ai-font-screen-title: 48px;
--ai-line-screen-title: 1.02;
--ai-font-section: 20px;
--ai-line-section: 1.15;
--ai-font-body: 18px;
--ai-line-body: 1.42;
--ai-font-small: 14px;
--ai-line-small: 1.32;
--ai-font-micro: 12px;
--ai-line-micro: 1.2;
```

### Weight system

Use only:

- 400 regular
- 600 semibold
- 700 bold for `MUSE` identity only when needed

Do not make every heading bold. The reference's large screen headings are primarily size/space-driven rather than heavy-weight-driven.

### Case

- primary screen headings: sentence/lowercase style exactly as copy specifies
- top-left `MUSE`: uppercase
- top-left `AI ONLY` and `ARCADE CONSOLE 2`: uppercase
- analysis card labels: lowercase/sentence case matching reference
- do not auto-uppercase buttons/navigation

## 6. Global safe area

```css
--ai-safe-x: 72px;
--ai-safe-top: 56px;
--ai-safe-bottom: 54px;
```

Persistent identity anchors at:

```text
x = 72
y = 58
```

Navigation baseline anchors approximately:

```text
y = 990
left x = 72
center x = 720
right x = 1368
```

Use these as grid anchors, not arbitrary per-screen values.

## 7. Persistent identity lockup

Component: `AiOnlyIdentity`

Position:

- x 72
- y 58
- width approximately 180

Structure:

```text
MUSE
AI ONLY
ARCADE CONSOLE 2
```

Recommended type:

- `MUSE`: 20px / 700 / near-black
- `AI ONLY`: 12px / 600 / muted ink
- `ARCADE CONSOLE 2`: 12px / 600 / near-black
- tight 1–3px vertical gaps

No icon.
No heart.
No console badge.
No screen number.
No colored block behind identity.

## 8. Navigation grammar

Navigation is text-only and visually quiet.

Components:

- `AiBackLink`
- `AiContinueLink`
- `AiRegenerateLink`

### Back

```text
←  back
```

- neutral/muted ink
- bottom-left
- 16–18px

### Continue

```text
continue  →
```

- accent blue
- bottom-right
- 16–18px

### Regenerate

```text
↻  regenerate
```

- accent blue
- bottom-center on result screen
- 16–18px

No filled button backgrounds.
No pills.
No borders around navigation.
No oversized arrows.

Hover/focus in development may darken or underline subtly. Do not change layout.

## 9. Border system

Use thin, calm strokes.

```css
--ai-border-thin: 1px;
--ai-border-strong: 1.5px;
--ai-radius-card: 7px;
--ai-radius-input: 6px;
```

Cards may use subtle 6–8px radius because the canonical AI-only reference contains slightly softened corners. This rule applies only to Console 2.

Never import Console 1's sharp pixel-border language here.

No box shadows on analysis cards.

The letter stack may use a very restrained soft shadow because the reference depicts physical layered sheets. Keep it below perceptual dominance:

```css
box-shadow: 0 10px 24px rgba(16,16,15,0.08);
```

Do not use shadows elsewhere without reference evidence.

## 10. Input field / textarea

Component: `AiPromptField`

Reference character:

- transparent/warm surface
- 1px neutral-grey border
- large rectangular field
- modest 6px radius
- no floating label
- no blue outline at rest
- character count aligned bottom-right inside or immediately at field edge

Canonical prompt cap for current fixture:

```text
120 characters
```

Textarea dimensions on 1440×1080 stage:

```text
width: 720px
height: 190px
```

Minimum internal padding:

```text
24px horizontal
22px vertical
```

Placeholder/example:

- 16px
- muted ink
- line height 1.35

Focus:

- border becomes `--ai-accent`
- 1px/1.5px only
- no glow

## 11. Analysis cards

Component: `AnalysisCard`

Used for sentiment, emotion and romance.

Geometry on `A2_02`:

```text
width: 500px
height: 112px minimum
vertical gap: 16px
```

Card:

- transparent or `--ai-bg`
- 1px `--ai-line`
- 7px radius
- no shadow
- 24px internal padding

Content structure:

```text
[small blue line icon] [label] [optional compact score/value]
                       [one restrained explanation line]
```

Icons must be simple stroked symbols, approximately 24px. Prefer CSS/SVG line icons created specifically for the project. Do not import a large icon library.

## 12. Tone controls

Component: `ToneControl`

Five controls, vertically stacked:

1. warmth
2. intimacy
3. emotional depth
4. playfulness
5. nostalgia

Each row contains:

```text
label     slider track/thumb     numeric percentage
```

Canonical row geometry:

```text
row height: 64px
label column: 180px
slider: 240px
value column: 72px
```

Slider track:

- total thickness 2px
- inactive: `--ai-line`
- filled section: `--ai-accent`

Thumb:

- 14px diameter
- `--ai-bg` fill
- 2px `--ai-accent` stroke
- no shadow

Display percentage is aligned right and uses near-black.

The tone controls must work with keyboard/mouse now and later accept semantic hardware actions without visual redesign.

## 13. Insight rail

Component: `LetterInsights`

On result screen, right-side rail width:

```text
240px
```

Heading:

```text
letter insights
```

Cards:

- 220–240px wide
- 104px minimum height
- 1px neutral line
- 7px radius
- 16–18px padding
- 14px label
- key value 18px, accent blue
- confidence line 12–13px muted

Canonical insight order:

1. sentiment
2. emotion
3. romance
4. tone profile

Do not hide emotion.

## 14. Letter document

Component: `AiLetterDocument`

Result layout should read as a layered typed sheet rather than a card dashboard.

Main sheet:

```text
width: 760px
height: 520px minimum
padding: 54px 64px
```

Stack behind:

- 1–2 offset paper-outline layers
- offset approximately 12px right/up per layer
- no color decoration
- thin neutral-grey borders

Main letter typography:

- 17–18px regular
- line-height 1.42
- left-aligned
- near-black

No handwriting/stamps/doodles/colour in current build.

## 15. Whitespace discipline

Whitespace is a primary design element.

Do not fill empty regions with:

- helper cards
- progress indicators
- icons
- explanations
- background shapes
- AI particles
- decorative lines

If a screen feels empty compared with a normal website, that is likely correct.

## 16. No motion in first build

All Console 2 components are static in the initial implementation.

No animated:

- analysis rings
- slider interpolation
- loading dots
- hover translations
- fade/slide page transitions

## 17. Visual anti-drift checklist

Reject the implementation if any of these occur:

- pure white background replaces warm off-white
- blue becomes saturated/cyan/electric neon
- cards gain modern heavy shadows
- buttons become filled rounded pills
- large icons appear
- every insight gets a different semantic color
- heading font becomes geometric or tech-styled
- content is packed tighter to avoid whitespace
- Console 1 assets appear anywhere
- top-left screen number is shown
- identity is moved into a header bar
- a generic design-system library determines spacing/radius

## 18. Reference calibration rule

The screenshot is the visual target. Tokens above are calibrated starting values. For visual regression, modify shared tokens/grid measurements first; never fix mismatches by creating screen-specific one-off styles unless the reference genuinely differs.