# 42 — MUSE Reflection Experience — Foundation Visual Calibration

**Status:** Approved reflection-shell baseline after first 1440×1080 screenshot review.

This file is the latest visual authority for the shared Reflection foundation/shell. Read it after files `38`–`41`.

Where this file conflicts with more generic foundation guidance in files `39` or `41`, **this file wins for the current shell geometry and calibration**.

## Review result

The first Reflection foundation screenshot is **approved as the baseline**.

It successfully reads as a distinct third chapter of the exhibition rather than as Arcade 1 or Arcade 2.

The current screenshot correctly contains:

- exact `1440 × 1080` stage;
- warm-white field;
- no Console 1 pixel chrome;
- no Console 2 identity/control deck;
- no arcade buttons or dial graphics;
- no persistent MUSE branding;
- no red system-accent language;
- minimal top-left reflection progress;
- minimal lower-left BACK text action;
- minimal lower-right CONTINUE text action;
- large intentional empty field for screen-specific reflection content.

## Locked stage background

The reviewed screenshot background resolves to approximately:

```css
--reflection-bg: #FAF9F6;
```

This matches the intended Quiet Editorial Gallery direction.

Do not make the reflection field:

- pure white;
- grey like the Console 2 hardware deck;
- lavender;
- navy;
- tinted differently per screen.

Keep the stage background fixed across `R_01`–`R_05`.

## Progress indicator

Current placement is approved.

Use:

```text
REFLECTION 01 / 05
```

at the shared top-left anchor.

Approximate canonical anchor:

```text
x: 72px
y: 58–64px
```

Visual role:

- 12–14px;
- regular/medium neutral grotesk;
- tracked slightly;
- muted grey;
- no box/background;
- no progress bar;
- no dots;
- no hearts/stars.

Only the number changes between reflection screens.

Do not add a MUSE logo beside the progress indicator.

## Bottom navigation anchors

The current lower navigation anchor positions are approved.

Approximate visual anchors:

```text
BACK:
  x: 72px
  baseline near y: 1010px

CONTINUE:
  right edge near x: 1368px
  baseline near y: 1010px
```

Use the same coordinates on all reflection screens unless content-overflow review explicitly requires a change.

Do not add a separate footer band, control deck, border or hardware housing around these actions.

## Navigation contrast states

The calibration screenshot uses very pale navigation text. That is acceptable for a **disabled/calibration state**, but active actions must remain clearly readable in exhibition lighting.

Define explicit states:

### Enabled

```css
color: #111111; /* or shared reflection ink */
opacity: 1;
```

### Disabled

Recommended:

```css
color: #B8B7B2;
```

or equivalent shared disabled token with sufficient visible distinction from the warm-white field.

### Hover/focus/keyboard state

Use restrained black/grey treatment only:

- underline;
- slightly stronger weight;
- thin focus outline if required for accessibility.

Do not use:

- red;
- purple;
- blue;
- filled CTA backgrounds;
- pill buttons;
- arcade press visuals.

## R_01 navigation state

When `R_01` is implemented:

- BACK may be enabled if product routing allows returning to `A2_03`;
- CONTINUE remains disabled until the required reflection-tag selection rule is satisfied;
- do not hide navigation and cause layout shift; preserve anchors and change state only.

The exact routing behavior remains governed by the reflection flow/state plan.

## Main content field

The large open region between progress and navigation is intentionally blank in the calibration shell.

This whitespace is **not missing UI**.

Do not add shared shell elements merely to fill it.

Specifically do not add:

- MUSE branding;
- decorative rules across the entire page;
- console identity labels;
- progress bars;
- icons;
- background textures;
- colored accents;
- hardware controls;
- generic survey container/card.

Screen-specific content (`R_01`–`R_05`) will occupy this field while the shell remains visually quiet.

## No shared separator/footer rule

Unlike Console 2, Reflection does **not** need a persistent horizontal separator above navigation.

The absence of a control-deck divider in the reviewed screenshot is approved.

Do not add a footer line by default.

Screen-specific thin rules may appear inside comparison/letter components as defined in files `39` and `40`.

## Typography character

The shell should use the Reflection neutral-grotesk system only.

Preferred stack remains:

```css
"Helvetica Neue", Helvetica, Arial, "Liberation Sans", sans-serif
```

The progress and navigation should feel editorial and quiet rather than machine-like.

Do not use:

- Arcade 1 pixel/mono type;
- Console 2 condensed MUSE display type;
- Console 2 system mono as a dominant reflection face.

## Separation from Console 2

The approved shell is intentionally even quieter than Console 2.

Do not reintroduce any of these while building screen content:

- `MUSE / AI ONLY / ARCADE CONSOLE 2` lockup;
- red square markers;
- bottom grey hardware deck;
- outlined BACK/NEXT physical buttons;
- intensity dial;
- machine-status copy;
- strong system rules used as console chrome.

## Separation from Console 1

Do not introduce:

- navy grid;
- purple/lavender desktop window;
- pixel sprites;
- magenta CTAs;
- pixel typography;
- arcade-button graphics;
- love-letter decorations around the page.

Letter documents may later have the approved subtle paper tint, but the shared shell remains neutral.

## Regression contract

Once `R_01` begins implementation, changes to shared Reflection components must preserve:

- `1440 × 1080` stage geometry;
- background `#FAF9F6` starting token;
- progress anchor;
- bottom navigation anchors;
- absence of console chrome;
- absence of a footer/control deck;
- absence of persistent decorative color;
- neutral typography character.

Screen-specific content must be inserted into the main field without moving the shared shell anchors.

## Acceptance checklist

Foundation remains approved only if:

- stage screenshot is exactly `1440 × 1080`;
- progress reads `REFLECTION NN / 05` in the same anchor;
- active navigation is readable and disabled navigation is clearly secondary;
- no Console 1 visual component mounts;
- no Console 2 visual shell/control component mounts;
- no MUSE identity is added by default;
- no persistent footer separator/deck is added;
- main field remains warm white and visually quiet;
- reflection still reads as a contemporary editorial/gallery chapter.

## Next gate

The Reflection foundation is now approved.

Codex may proceed to **Phase C / `R_01` only** from file `41`.

`R_01` should implement:

- normalized side-by-side letter analysis;
- the shared comparison schema;
- the experience-feeling multi-select tags;
- Reflection navigation states;

Then capture a clean `1440 × 1080` screenshot and **STOP for visual review** before implementing `R_02`.
