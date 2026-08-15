# 35 — Arcade Console 2 / AI Only — A2_02 Tone-Only Visual Calibration

**Status:** Approved visual baseline for `A2_02` after the post-generation analysis flow change in file `34`.

This file records the visual review of the revised A2_02 screenshot where pre-generation sentiment/emotion/romance analysis has been removed.

Where this file conflicts with earlier A2_02 layout guidance in files `22` or `24`, **this file wins** for the current visible composition. File `34` remains the product-flow authority for analysis timing.

## Review result

The revised A2_02 direction is **approved**.

The screen now correctly communicates one responsibility only:

> review and adjust how AI will shape the letter before generation.

The following are now locked:

- no visible sentiment analysis before generation;
- no visible emotion analysis before generation;
- no visible romance analysis before generation;
- centered heading and supporting line;
- one centered five-row tone-control module;
- no surrounding dashboard/card container;
- warm off-white main field;
- persistent top-left `MUSE / AI ONLY / ARCADE CONSOLE 2` identity;
- persistent fixed lower control deck;
- BACK and NEXT both enabled;
- INTENSITY DIAL visually present and active only for the selected/focused tone row;
- no floating Back/Continue links;
- no dominant blue;
- no Console 1 chrome;
- no bottom-center MUSE wordmark.

## Locked copy

### Heading

```text
here’s how AI will shape it.
```

### Supporting line

```text
adjust the tone before it writes.
```

Keep both strings configurable in the Console 2 content layer.

The current lowercase sentence treatment is approved.

Do not restore:

```text
here’s what I understand.
```

on A2_02 because that wording belongs to the superseded visible-analysis interpretation.

## Heading hierarchy

Preserve the current screenshot hierarchy:

- centered;
- near-black;
- neutral Swiss/neo-grotesk content/display role;
- large but clearly quieter than the oversized A2_00 `MUSE` hero;
- no red emphasis;
- no additional rule directly under the title unless later approved.

The supporting line remains muted grey and should not compete with the sliders.

## Tone-control module

Keep exactly five rows in this order:

1. warmth
2. intimacy
3. emotional depth
4. playfulness
5. nostalgia

Current fixture values remain acceptable:

```text
warmth             72%
intimacy           68%
emotional depth    70%
playfulness        40%
nostalgia          55%
```

### Approved composition

The current centered module is approved as the baseline.

Preserve:

- approximately 620–760px overall interaction width;
- left-aligned parameter labels;
- consistent slider start/end positions;
- right-aligned mono/system percentage values;
- generous vertical spacing between rows;
- no outer card/background box;
- no icons beside each parameter;
- no extra explanatory text per row.

Do not move the control group back into a right-hand dashboard column.

## Slider visual language

The current slider character is approved:

- thin neutral/black track;
- dark filled/active portion;
- light neutral remainder;
- small outlined circular thumb;
- no shadow;
- no glow;
- no blue;
- no thick progress-bar styling.

### Idle screenshot

The reviewed screenshot is an acceptable **no-row-focused** baseline.

Signal red does not need to appear on every slider in idle state.

The red system language is already present through the intensity-dial pointer and may be used only when a tone row becomes active/focused.

### Focus/active state

When a row becomes the current `activeToneControlId`, use one restrained technical signal only.

Preferred options, in order:

1. tiny signal-red square/marker beside the active label; or
2. signal-red thumb outline/pointer detail; or
3. slightly stronger label + tiny red marker.

Do not make the full slider track red.
Do not use large red fills.
Do not animate the slider in the current Console 2 static phase.

Focus state must remain visible without relying on red alone; also use outline/weight/contrast where appropriate.

## Percentage values

Keep values in the mono/system role.

They should be muted enough to remain secondary but clearly readable in exhibition lighting.

Do not convert values into badges, pills or large numerical cards.

## Intensity dial interaction

The deck dial is active only on A2_02.

Rules remain:

```text
activeToneControlId === null
→ dial changes nothing

activeToneControlId === 'warmth'
→ dial changes warmth only

activeToneControlId === 'nostalgia'
→ dial changes nostalgia only
```

The dial is not a sixth global intensity value.

The dial must never change sentiment, emotion or romance because those are post-generation analysis outputs on A2_03.

## Navigation

Current deck state:

```text
BACK = enabled
NEXT = enabled
INTENSITY DIAL = conditionally active for selected tone row
```

Routes:

```text
BACK -> A2_01
NEXT -> generate/select AI-only result -> A2_03
```

Do not add a separate visible `GENERATE` CTA inside the main content region unless explicitly requested later.

The physical NEXT control is the generation commit.

## Generation transition

In the current static prototype:

- NEXT may synchronously select/generate the deterministic result fixture;
- no full-screen loading page;
- no pre-generation analysis screen;
- no fake analytics interstitial.

The next visible state is A2_03.

## Whitespace

The large open regions around and beneath the five controls are intentional.

Do not fill the space with:

- analytics;
- icons;
- decorative grids;
- extra rules;
- explanatory paragraphs;
- AI illustrations;
- progress UI.

A2_02 should feel controlled and sparse.

## Regression constraints

Any shared-token/component change made while polishing A2_02 must not alter:

- A2_00 approved composition;
- A2_01 approved composition;
- control-deck geometry;
- identity position;
- global stage/background colors.

## Acceptance checklist

A2_02 is locked only if:

- rendered at exactly 1440×1080;
- zero visible sentiment/emotion/romance analysis blocks exist;
- exactly five tone controls exist in canonical order;
- title reads `here’s how AI will shape it.`;
- supporting line reads `adjust the tone before it writes.`;
- sliders remain monochrome/neutral in idle state;
- percentage values are readable;
- focused row has a restrained accessible active state;
- dial edits only the active tone row;
- dial is inert with no active tone row;
- NEXT generates/selects A2_03 result;
- no extra generation screen appears;
- A2_00/A2_01 visual regressions remain unchanged.

## Next gate

A2_02 is approved as the visual baseline.

Codex may proceed to `A2_03` **only** after verifying the active-row/dial interaction and regressions above.

For A2_03, analysis appears only after the generated letter exists, as defined by file `34`.

Do not reintroduce analysis on A2_02.
