# 22 — Arcade Console 2 / AI Only — Screen Specifications

This document defines the four canonical AI-only screens at 1440×1080. Copy remains configurable, but composition, hierarchy and component placement are locked unless a new approved visual reference changes them.

All screens use `AiOnlyShell` and `AiOnlyIdentity`.

## Shared screen coordinates

Use the 1440×1080 internal stage.

Persistent anchors:

```text
outer frame inset: 20px
identity: x 72, y 58
left nav: x 72, baseline y 990
center nav: x 720, baseline y 990
right nav: x 1368, baseline y 990
```

Do not render tiny screen numbers.

---

# `A2_00` — Welcome Back / Context Loaded

## Purpose

Acknowledge that Console 2 already knows who the visitor is and has inherited the previous experience context.

It must not feel like onboarding again.

## Required content

Config shape:

```ts
{
  titlePrefix: 'welcome back,',
  contextLine: 'your context from the first experience has been loaded.',
  beginLabel: 'press to begin'
}
```

Visitor name is dynamic and inserted as the second title line.

Example:

```text
welcome back,
kristian
```

## Composition

### Hero block

Approximate locked box:

```text
x: 330
width: 780
center aligned
start y: 250
```

Title:

- two lines
- 64px regular
- line-height 0.98
- near-black
- centered
- no decorative punctuation added

The user's name uses the same weight/size as the phrase. Do not make it blue or bold.

### Context line

```text
y: ~430
width: 520
```

- 18px
- muted ink
- centered
- max 2 lines

### Context signal

Centered below copy:

```text
center x: 720
center y: ~610
diameter: 180px
```

Use `ContextSignal` from the component plan:

- static dotted/radial form
- neutral-grey structure
- tiny blue center
- no labels
- no animation

### Begin control

Below signal:

```text
y: ~780
```

A small circular outlined target/press indicator may be shown because it exists in the canonical reference.

Rules:

- 34–40px outer circle
- 1.5px accent outline
- tiny accent center dot
- no 3D arcade representation

Text:

```text
press to begin
```

- 16px accent blue
- centered
- 12px below indicator

## Interaction

- click/Enter on begin -> `A2_01`
- no back link required on first Console 2 screen

## Prohibited additions

- progress meter
- explanation of AI analysis
- recipient name
- relationship name unless copy later explicitly requests it
- Console 1 handoff instructions
- colored illustration

---

# `A2_01` — Short Prompt

## Purpose

Ask the visitor for one short direction that guides the AI-generated letter without recreating the human writing task.

## Required copy

Reference-aligned default config:

```ts
{
  title: 'what would you like\nAI to focus on?',
  subtitle: 'give AI a short prompt to guide the letter.',
  placeholder: 'example: help me apologize for being distant lately\nand express how much she means to me.',
  maxLength: 120
}
```

Copy may later change. Geometry must not.

## Composition

### Title

Centered.

```text
x: 350
width: 740
y: 250
```

- 48px regular
- line-height 1.02
- near-black
- exactly two lines at canonical copy length

### Subtitle

```text
y: ~385
```

- 16px
- muted ink
- centered

### Prompt textarea

```text
x: 360
width: 720
height: 190
y: 455
```

Use `AiPromptField`.

Character count bottom-right inside field area:

```text
0 / 120
```

- 14px muted ink

Do not display a label above the textarea unless future copy specifically adds one.

## Navigation

Bottom:

- left: `← back`
- right: `continue →`

Continue is accent blue when valid.
When invalid, use muted neutral text and `aria-disabled`/disabled button semantics; do not add opacity animations or tooltip.

## Validation

Valid when:

```ts
prompt.trim().length > 0
```

Max 120 characters.

## Interaction

- back -> `A2_00`
- continue -> create/load deterministic interpretation state -> `A2_02`

No standalone generating/analysis-loading screen in current static flow.

---

# `A2_02` — Here’s What I Understand / Analysis + Tone Controls

## Purpose

Expose the machine's interpretation and allow the visitor to tune the generation parameters.

This screen deliberately juxtaposes **read-only machine analysis** with **editable tone controls**.

## Title

Reference-aligned default:

```text
here’s what I understand.
```

Position:

```text
x: 300
width: 840
y: 145
```

- 46px regular
- centered
- near-black

## Main grid

Two columns with generous gap.

```text
container x: 170
container width: 1100
top: 300
left column width: 500
column gap: 140
right column width: 460
```

### Left heading

```text
analysis
```

- 18px / 600
- near-black
- left aligned
- 18–24px above first card

### Analysis stack

Exactly three cards in this order:

1. sentiment analysis
2. emotion detection
3. romance detection

Each approximately:

```text
width: 500
height: 112
gap: 16
```

Reference-aligned fixture display:

#### Sentiment

```text
sentiment analysis        62 / 100
overall sentiment is positive with
moments of vulnerability.
```

#### Emotion

```text
emotion detection         71 / 100
love, longing, and hope are
the dominant emotions.
```

#### Romance

```text
romance detection         68 / 100
clear romantic intent with a desire
for closeness and reassurance.
```

Scores are static design fixtures for now. They must not be positioned as diagnostic truth in copy.

Analysis cards are read-only. No hover edit state.

### Right heading

```text
tone controls
```

- 18px / 600
- left aligned

Optional tiny information icon shown in the reference may appear at the far right of the heading row:

- simple 18px neutral outline `i`
- no tooltip required in static build
- do not use a large icon library

### Tone controls

Exactly five rows in order:

```text
warmth             72%
intimacy           68%
emotional depth    70%
playfulness        40%
nostalgia          55%
```

Use canonical values from fixture only as initial proposal.

Visitor can edit all five.

Tone rows start aligned with first analysis card and should visually form a single vertical rhythm.

## Navigation

- left: `← back`
- right: `continue →`

No separate `generate` filled button.

## Interaction

Back:

```text
A2_02 -> A2_01
```

Prompt value remains.

Continue:

```text
A2_02 -> A2_03
```

Static build chooses/generates fixture result from current tone-control state.

## Prohibited

- sliders for sentiment/emotion/romance
- colorful sentiment labels
- radar chart
- pie chart
- AI confidence visualization beyond the compact reference-style score/readout
- more than five tone controls
- explanatory helper panel

---

# `A2_03` — Generated AI Letter + Letter Insights

## Purpose

Present the AI-only letter as a clean typed document and make the machine interpretation visible alongside it.

This is the final Console 2 screen before shared reflection.

## Overall layout

The reference is asymmetrical: large document slightly left-of-center with a narrow insight rail on the right.

Recommended result grid:

```text
container x: 210
container y: 235
container width: 1090
columns: 780px 240px
gap: 70px
```

Do not center the combined result group by making both columns equal.

## Letter document

Main sheet:

```text
width: 760px
height: ~520px
```

Layered-sheet offsets behind it establish depth.

Letter content starts with a casual neutral salutation fixture such as:

```text
hey kristian,
```

The reference's sample copy is fixture content, not a locked final message. Store all letter copy in fixtures/config.

Typography:

- 17–18px
- regular
- line-height 1.42
- left aligned
- near-black

No visible editor controls.
No textarea chrome.
No handwriting/personal decoration in first build.

## Letter insights rail

Heading:

```text
letter insights
```

Exactly four cards in order:

1. sentiment
2. emotion
3. romance
4. tone profile

### Sentiment fixture

```text
sentiment
positive
confidence: 82%
```

### Emotion fixture

Example:

```text
emotion
affection / longing
confidence: 79%
```

### Romance fixture

```text
romance
high
confidence: 78%
```

### Tone profile

```text
tone profile
warm, intimate,
sincere
```

Important: emotion must be present even though the original montage right rail showed fewer categories.

Accent blue is used for the key value (`positive`, `high`, tone labels) and icon; labels/confidence remain neutral.

## Navigation

Bottom navigation has all three canonical actions:

```text
left:   ← back
center: ↻ regenerate
right:  continue →
```

### Back

Returns to `A2_02` with current tone controls intact.

### Regenerate

Stay on `A2_03`.
Preserve:

- inherited context
- short prompt
- analysis
- current tone-control values

Cycle to the next deterministic letter fixture and its matching insights.

### Continue

Enter shared reflection/comparison flow.

Guard that both Human + AI and AI-only results exist.

## No standalone completion screen

Do not add:

- `AI letter complete`
- `thank you`
- `ready to compare?`

unless later explicitly designed.

---

# Cross-screen layout rules

## Persistent identity

`AiOnlyIdentity` must not move between screens.

## Bottom navigation

Use same vertical baseline on screens 2–4.

## Text measure

Avoid very wide body paragraphs. Most body/helper text should remain under ~60–70 characters per line where practical.

## Whitespace

If implementing a missing copy state creates open space, preserve the open space. Do not fill it with UI.

## Content overflow

If future copy is longer:

1. keep shell/frame/identity/navigation fixed,
2. keep type role within ±2px where possible,
3. allow internal content wrapping,
4. only request design review if the canonical bounding box cannot fit at readable size.

Do not shrink headings dramatically to accommodate verbose copy.

# Static fixture transition map

```text
A2_00
  BEGIN -> A2_01

A2_01
  BACK -> A2_00
  CONTINUE(valid prompt) -> A2_02

A2_02
  BACK -> A2_01
  tone edits -> remain A2_02
  CONTINUE -> A2_03

A2_03
  BACK -> A2_02
  REGENERATE -> A2_03 (new fixture variant)
  CONTINUE -> shared reflection first screen
```

# Screen approval gates

Do not call a screen complete until:

- 1440×1080 screenshot exists
- identity anchor matches all other Console 2 screens
- stage/frame colors match shared tokens
- type hierarchy matches reference
- navigation baseline matches
- there is no Console 1 visual chrome
- there are no unapproved UI elements
- the route/state behaviour matches this document.