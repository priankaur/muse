# 39 — MUSE Reflection Experience — Visual System

**Status:** Current visual-system authority for all reflection screens.

Reflection is a third visual language, intentionally separate from both console experiences.

Recommended style name:

> **Quiet Editorial Gallery**

The design should feel like a calm museum comparison table or contemporary editorial exhibition panel: minimal, neutral, legible, spacious and reflective.

It must not feel like an arcade screen, an AI dashboard, a survey product, or a continuation of either console's chrome.

## One-line direction

A warm-white, black-and-grey editorial reflection interface with generous whitespace, precise typography, thin rules, equal-weight comparison layouts, and only the two letter documents sitting on very subtle tinted paper surfaces.

## Fixed stage

Keep the shared exhibition rendering model:

```text
1440 × 1080
4:3
```

Scale the complete stage proportionally.

Do not independently reflow major content regions.

## Palette

Reflection should be almost monochrome.

Starting tokens:

```css
--reflection-bg: #FAF9F6;
--reflection-ink: #111111;
--reflection-secondary: #5E5E5A;
--reflection-muted: #8B8B86;
--reflection-line: #D6D5D0;
--reflection-line-strong: #1A1A1A;
--reflection-selection: #111111;
--reflection-selection-text: #FAF9F6;
```

No red system accent from Console 2.
No purple/magenta from Console 1.
No bright semantic colors.

## Letter surfaces — only subtle color in the system

The letter documents are the only elements allowed to have a perceptible background tint.

Preferred approach:

Use the SAME subtle paper tint for both letters so color does not bias the comparison.

Starting token:

```css
--reflection-letter-paper: #F1EEE8;
```

Alternative if more separation from the background is needed:

```css
--reflection-letter-paper: #F2F0EB;
```

Both letter cards must use identical background color, border, dimensions, typography and elevation.

Do not use warm tint for Human + AI and cool tint for AI Only; that would visually bias the visitor.

Selected state must be communicated by border/marker/label treatment rather than changing one letter's paper color.

## Typography

Use one neutral contemporary grotesk family across reflection.

Preferred stack:

```css
font-family: "Helvetica Neue", Helvetica, Arial, "Liberation Sans", sans-serif;
```

If a bundled open-source equivalent is required, use a neutral grotesk with ordinary proportions.

Do not use:

- pixel fonts;
- condensed machine typography;
- mono for main content;
- playful display fonts;
- oversized poster type from A2_00.

### Roles

#### Reflection eyebrow / progress

```text
12–14px
uppercase or small caps
letter-spacing: 0.08–0.12em
muted grey
```

Examples:

```text
REFLECTION 01 / 05
COMPARE
```

#### Main question

```text
44–56px
400–500 weight
near-black
line-height: 1.05–1.12
```

Questions should feel conversational and calm, not like system commands.

#### Supporting copy

```text
16–19px
400
secondary grey
line-height: 1.4–1.55
```

#### Letter body

```text
16–18px
400
line-height: 1.45–1.55
near-black
```

## Header / progress

Use a tiny progress indicator at the top-left or top-center:

```text
REFLECTION 01 / 05
```

This is allowed because it is a sequence indicator, not a score.

No MUSE logo is required on every reflection screen.

If brand presence is needed, use a very small `MUSE / REFLECTION` text lockup only; do not import either console's identity design.

## Layout language

Reflection should use:

- large margins;
- centered or balanced editorial compositions;
- strong baseline/grid alignment;
- thin 1px rules;
- equal-weight comparison columns;
- no decorative sprites;
- no floating chrome;
- no hardware deck;
- no visible arcade controls;
- no framed desktop window.

## Letter comparison component

Create one reusable `ReflectionLetterCard`.

Recommended geometry for side-by-side comparisons:

```text
card width: 500–540px
card height: 470–560px depending on content
column gap: 48–72px
```

Card treatment:

- subtle paper tint;
- 1px neutral border;
- 0–2px radius maximum;
- no dramatic shadow;
- generous internal padding;
- label above or inside top edge;
- full text may use controlled clipping/scroll only if unavoidable.

Both cards must remain equal in size.

Preferred labels:

```text
LETTER A
HUMAN + AI
```

```text
LETTER B
AI ONLY
```

Use small neutral labels. Do not label one `YOUR LETTER` and the other `AI LETTER` if that creates visual bias in a question where voice recognition is being tested.

## Analysis comparison component

Create `ReflectionComparisonGrid` using shared dimensions for both letters.

Preferred appearance:

- no bordered dashboard cards;
- one label column + Letter A value + Letter B value;
- thin horizontal rules between rows;
- black/grey only;
- text descriptors or very thin monochrome bars;
- no circles/radars/gauges.

Example:

```text
                     LETTER A             LETTER B
-------------------------------------------------------
emotional warmth     high                 moderate
personal specificity high                 medium
vocabulary complexity medium              high
affectionate language high                restrained
```

## Tag selection

Create `ReflectionTag`.

Idle:

- white/warm-white field;
- 1px neutral border;
- near-black text;
- 4–8px radius, not a highly rounded pill;
- no shadow.

Selected:

- near-black fill;
- warm-white text;
- same geometry;
- optional small check mark.

Do not assign tag colors by emotion.

Recommended gap:

```text
10–14px
```

## Letter selection state

For R_02 and R_03, selecting a letter should use restrained visual feedback:

- border becomes 2px near-black;
- optional small filled black selection marker in top corner;
- label weight increases slightly;
- paper tint does not change.

Do not use green ticks, gold crowns, glow or celebratory motion.

## Stance choice cards

R_04 uses three equal `ReflectionChoiceCard` components.

Recommended layout:

```text
3 columns
width: 330–360px each
height: 210–250px
same spacing
```

Each card contains:

- short label;
- one short explanatory sentence;
- selection marker.

Idle:

- warm-white background;
- 1px line;
- black type.

Selected:

- black background;
- white type;

Do not use different colors/icons for the three philosophies.

## Primary continuation action

Reflection is no longer visually controlled by arcade hardware.

Use a simple text/button treatment:

```text
CONTINUE →
```

Recommended:

- black text;
- no large fill by default;
- thin underline or 1px border only if needed;
- lower-right alignment;
- disabled state grey.

BACK may appear as:

```text
← BACK
```

lower-left.

These are visual controls only. Real physical input may later dispatch the same semantic actions invisibly.

## R_05 exit screen

The final screen should be almost poster-like:

- one headline;
- three short numbered instructions;
- optional tiny diagram consisting only of simple black line icons if later approved;
- no comparison cards;
- no hardware chrome.

The physical token colors, boxes and postcard are part of the installation, not reasons to make the digital screen colorful.

## Motion

Default first implementation: static.

If motion is added later, use very small editorial fades/position changes only and keep it separate from Console 1 arcade motion.

Do not import Console 1 stepped pixel transitions or Console 2 machine UI behavior.

## What this style is NOT

Do not make reflection look like:

- Console 1 with the colors removed;
- Console 2 without the control deck;
- Typeform;
- a SaaS survey;
- an analytics dashboard;
- a game results screen;
- a voting app;
- a winner/loser comparison.

## Core visual principle

> **The reflection interface should disappear behind the thinking.**

The letters and the questions are the content. Everything else should be quiet enough to let the visitor compare, recognize and choose.
