# 23 — Arcade Console 2 / AI Only — Testing and Acceptance

Console 2 is highly minimal. Small spacing, type and color errors are therefore more visible than they would be in a dense interface. Visual regression is mandatory.

## 1. Test categories

Implement:

1. route/flow tests
2. state-persistence tests
3. component interaction tests where valuable
4. 1440×1080 screenshot tests
5. anti-regression checks preventing Console 1 chrome on Console 2

## 2. Deterministic viewport

All canonical screenshots use:

```text
viewport/stage: 1440 × 1080
DPR for baseline: 1 where possible
animations: disabled
network-dependent content: none
fixture session: fixed
```

Do not create baselines at arbitrary browser dimensions.

## 3. Canonical fixture session

Use one named deterministic test fixture, e.g.:

```ts
const canonicalAiOnlySession = {
  visitor: { id: 'fixture-001', firstName: 'kristian' },
  recipient: { name: '...', relationship: 'partner' },
  arcade1: {
    completed: true,
    contextForArcade2: 'fixture context',
    humanAiLetter: 'fixture Human + AI letter'
  },
  arcade2: {
    shortPrompt: '',
    ...
  }
};
```

The exact recipient can remain fixture-only. Visual screenshots should avoid variable random content.

## 4. Route tests

Required flow:

```text
A2_00 -> A2_01 -> A2_02 -> A2_03 -> reflection
```

Assertions:

- begin opens prompt
- prompt back returns welcome
- empty prompt disables continue
- valid prompt opens interpretation screen
- interpretation back preserves prompt
- interpretation continue opens result
- result back preserves tone controls
- result continue enters shared reflection

## 5. Regenerate tests

At `A2_03`:

Before regenerate, capture:

- short prompt
- analysis object
- current tone values
- active variant index
- visible result body

After regenerate assert:

- short prompt unchanged
- analysis unchanged
- tone values unchanged
- active variant index changed
- visible result body changed
- matching insight fixture changed where designed
- route remains `A2_03`

Cycle enough times to verify wraparound.

## 6. Analysis/editability tests

`A2_02` must contain exactly:

Read-only analysis:

- sentiment
- emotion
- romance

Editable controls:

- warmth
- intimacy
- emotional depth
- playfulness
- nostalgia

Assert analysis cards contain no slider/input/select elements.

Assert five range controls exist and values can change.

## 7. Inheritance tests

Assert Console 2 does not render:

- registration form
- recipient-name input
- relationship selector

Welcome must use inherited first name.

## 8. Anti-chrome tests

For all `A2_*` screens assert no DOM elements/classes corresponding to Console 1 shell are mounted, including where applicable:

- `MuseWindow`
- `HardwareControlStrip`
- `FloatingSpriteLayer`
- pixel-window title bar
- red arcade button images
- gold dial image

Prefer stable `data-testid` or component boundaries rather than brittle CSS text matching.

## 9. Screenshot baselines

Create one canonical screenshot for each screen:

```text
tests/visual/baselines/ai-only/
  A2_00-welcome.png
  A2_01-prompt.png
  A2_02-interpretation.png
  A2_03-result.png
```

Also capture optional states:

```text
A2_01-prompt-focused.png
A2_02-tone-edited.png
A2_03-regenerated.png
```

## 10. Screenshot preparation

Before screenshot:

- use canonical fixture
- reset focus unless testing focused state
- disable caret blink if screenshot tool supports it
- disable transitions/animations globally
- ensure system font/bundled font has loaded
- wait for layout stable

## 11. Visual comparison priorities

When calibrating against `docs/reference/ai-only-console2-canonical.jpg`, compare in this order:

1. overall warm-background tone
2. outer frame inset
3. persistent identity position
4. main content bounding box
5. title size/line breaks
6. analysis/result column proportions
7. bottom navigation baseline
8. card/input borders and radii
9. accent blue hue
10. fine typography details

Do not start by tuning tiny icon strokes while the overall geometry is wrong.

## 12. Expected reference adaptation

The source montage may not itself be 4:3 per individual panel. Product requirement explicitly locks the implementation to 1440×1080.

Therefore visual regression should preserve the **reference's relative composition and whitespace language** while using the canonical 4:3 coordinate plan defined in `19` and `22`.

Do not crop the stage to imitate the montage panel aspect ratio.

## 13. Pixel-diff policy

Use screenshot tests primarily as a guard, but do not blindly accept large thresholds.

Recommended:

- initial calibration: manual visual review + overlay
- once approved: low pixel-diff tolerance
- token/font rendering may require a small anti-aliasing allowance

If CI environments produce font rasterization differences, use geometry-focused assertions in addition to screenshots rather than raising screenshot tolerance until the test becomes meaningless.

## 14. Geometry assertions

Where practical, Playwright should measure key elements and assert bounds with narrow tolerance.

Examples:

- identity x/y within ±2px
- outer frame inset within ±1px
- prompt width/height within ±2px
- main interpretation two-column positions within ±3px
- bottom nav baseline within ±2px

This catches layout drift even if screenshot antialiasing changes.

## 15. Color assertions

Use computed style assertions for core tokens:

- stage background
- primary ink
- line color
- accent

Do not hard-code per-screen colors in tests; validate token application.

## 16. Accessibility acceptance

Interactive visible navigation and controls must:

- be reachable by keyboard
- have visible focus treatment consistent with minimal design
- expose correct role/name/value
- not rely only on color for disabled state
- use native range semantics where possible

The visual reference remains primary, but accessibility should be solved without adding unrelated visible chrome.

## 17. Content overflow tests

At minimum test:

- first name up to a reasonable long fixture
- prompt at exactly 120 characters
- analysis summary wrapping to two lines
- tone label `emotional depth`
- letter body with enough content to occupy the reference page

If overflow occurs, fix content layout without changing global stage geometry.

## 18. Manual visual acceptance checklist per screen

### All screens

- warm off-white, not pure white
- identity at same coordinates
- no screen number
- no Console 1 styling
- no extra decorative UI
- correct neutral font character
- generous whitespace
- thin neutral frame

### A2_00

- hero vertically balanced
- context signal restrained, not futuristic
- begin indicator small

### A2_01

- title line break matches reference intent
- textarea is dominant input, not oversized form card
- counter aligned cleanly

### A2_02

- left/right columns feel balanced but not cramped
- analysis cards exactly three
- tone controls exactly five
- sliders visually thin

### A2_03

- letter reads as document, not dashboard panel
- insight rail is secondary to letter
- exactly four insight categories including emotion
- regenerate sits at bottom center

## 19. Stop condition

If the first Console 2 shell or `A2_00` is visibly off, do not continue implementing the remaining screens.

Calibrate shared tokens/layout first. Otherwise a small mistake gets multiplied across every screen.

## 20. Definition of visual approval

Console 2 is visually approved only when a reviewer can place the 1440×1080 implementation beside the canonical reference and recognize the same system immediately without seeing:

- borrowed arcade styling
- generic SaaS components
- accidental brand additions
- layout density drift
- color drift
- typography personality drift.