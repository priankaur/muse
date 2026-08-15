# 36 — Arcade Console 2 / AI Only — A2_03 Generated Letter + Post-Generation Analysis Plan

**Status:** Next implementation authority after the approved A2_02 tone-only calibration in file `35`.

Read this together with:

- `34-ai-only-post-generation-analysis-flow.md` — product-flow/state authority;
- `35-ai-only-a2-02-visual-calibration.md` — locked A2_02 baseline;
- `19-ai-only-visual-system.md` — Console 2 visual system;
- `20-ai-only-component-architecture.md` — component boundaries.

Where this file conflicts with older A2_03 analysis timing in files `18`–`24`, files `34` and `36` win.

## Purpose

`A2_03` is the final AI-only screen before shared comparison/reflection.

It must present:

1. the AI-only generated love letter as the dominant object;
2. post-generation analysis of that exact generated result;
3. a restrained regenerate action;
4. the persistent Console 2 physical control deck.

The visitor must visually understand that the analysis describes **what AI actually wrote**, not what it predicted before writing.

## Primary hierarchy

The screen must read in this order:

```text
GENERATED LETTER
↓
LETTER ANALYSIS
↓
REGENERATE
↓
CONTROL DECK
```

The letter is always the visual hero.

The analysis rail is secondary.

Do not make the analysis wider, darker, more colorful or more visually dominant than the letter document.

## Shared shell

Preserve without redesign:

- 1440 × 1080 fixed stage;
- warm off-white main field;
- persistent top-left `MUSE / AI ONLY / ARCADE CONSOLE 2` identity;
- light-grey lower control deck;
- strong horizontal deck separator;
- outlined BACK/NEXT controls;
- right-side intensity dial;
- black / grey / off-white / restrained signal-red palette.

No giant A2_00 `MUSE` hero title on this screen.
No Console 1 chrome.
No blue-dominant UI.

## Recommended composition

Starting geometry at 1440 × 1080:

```text
main result region:
  x: 180–205
  y: 155–185
  width: 1090–1110
  height: <= 650

columns:
  letter: 730–770px
  gap: 65–80px
  analysis rail: 235–270px
```

Keep the whole result comfortably above the control deck.

Do not vertically center the result so low that it approaches the deck separator.

## Generated letter document

Create/reuse a dedicated `AiLetterDocument` component.

Starting size:

```text
width: 740–770px
height: 500–525px
```

Visual treatment:

- warm off-white/light paper surface slightly distinguishable from stage;
- 1px neutral/near-black outline;
- 1–2 offset outline/sheet layers behind the main sheet to suggest a generated document stack;
- no glossy shadow;
- no colored paper;
- no handwriting/stamps/doodles yet;
- square or extremely low-radius corners;
- no modern card elevation.

The sheet-stack effect should remain restrained and technical.

### Letter typography

Use the neutral content face, not system mono for full body.

Starting rules:

```text
font-size: 16–18px
line-height: 1.4–1.5
color: near-black
alignment: left
```

Preserve greeting, paragraphs and sign-off as actual text structure.

Do not center the body.
Do not make the letter look handwritten in this phase.

## Optional small output label

If a label is needed above the document, use only a compact system label such as:

```text
AI GENERATED LETTER
```

or

```text
OUTPUT // AI ONLY
```

This is optional, not mandatory.

If used:

- small mono/system typography;
- near-black or muted grey;
- optional tiny signal-red square;
- no large headline.

Do not invent a decorative title that competes with the letter.

## Post-generation analysis rail

Use a dedicated `LetterAnalysisRail` / existing `LetterInsights` component.

Preferred rail heading:

```text
letter analysis
```

Optional structure:

```text
[red square] letter analysis
```

The heading may use a tiny red signal marker, but the analysis values themselves remain monochrome.

### Required categories

Exactly four:

1. sentiment
2. emotion
3. romance
4. tone profile

These must correspond to the active generated variant.

### Recommended analysis block treatment

Prefer compact technical groups separated by thin lines rather than colorful dashboard cards.

Each group may contain:

```text
LABEL
primary value
secondary summary/confidence
```

Example structure:

```text
sentiment
positive
confidence: 82%
```

```text
emotion
love / longing / hope
```

```text
romance
high romantic intent
confidence: 78%
```

```text
tone profile
warm / intimate / reflective
```

Rules:

- label: small system/neutral semibold;
- primary value: near-black;
- confidence/explanation: muted grey/mono where appropriate;
- use 1px neutral rules between groups;
- low/zero radius if outlined blocks are used;
- no shadows;
- no semantic green/pink/blue;
- no chart library;
- no pie/radar/ring visualizations;
- no oversized scores.

Signal red may appear as a tiny heading/status marker only.

## Analysis provenance

Each result fixture owns its matching analysis.

Recommended shape:

```ts
type AiLetterVariant = {
  id: string;
  body: string;
  analysis: {
    sentiment: InsightMetric;
    emotion: InsightMetric;
    romance: InsightMetric;
    toneProfile: string[];
  };
};
```

If the implementation already uses `insights` rather than `analysis`, that property name may remain.

Do not read analysis from stale pre-generation A2_02 state.

## Deterministic fixtures

Provide at least 3 result variants.

Each variant must differ in:

- letter wording;
- at least one post-generation analysis value/summary;
- tone profile when appropriate.

The fixtures should use the same inherited context, prompt and active tone-control model, but represent different deterministic outputs for regeneration testing.

## Regenerate action

There is no approved fourth hardware control.

Keep `REGENERATE` as software/system text action.

Preferred placement:

- centered under the result region and above the deck separator; or
- aligned beneath the letter document if that produces better balance.

Visual treatment:

```text
[optional red square] REGENERATE
```

- small mono/system text;
- near-black;
- no filled CTA;
- no pill;
- no large icon button;
- no blue.

On activation:

```text
preserve prompt
preserve inherited context
preserve current 5 tone values
cycle active generated variant
update body + analysis together
remain on A2_03
```

Do not send visitor back to A2_02.

## Deck state

```text
BACK = enabled -> A2_02
NEXT = enabled -> shared comparison/reflection
INTENSITY DIAL = visible but inactive
```

The dial pointer can remain as the standard physical visual, but it must not modify any result-analysis value.

Do not make the dial control regeneration.

## Back / stale result behavior

If visitor returns:

```text
A2_03 -> BACK -> A2_02
```

preserve:

- short prompt;
- current five tone-control values.

If any tone value changes, the previous result is stale.

On NEXT from A2_02, reset/select a fresh active result fixture and matching analysis.

Do not silently display the old result under new controls.

## NEXT / reflection handoff

`NEXT` from A2_03 enters the existing shared comparison/reflection flow.

Guard that both comparison artifacts exist:

- Console 1 Human + AI result;
- active Console 2 AI-only result.

Do not add another AI-only completion screen.

## Whitespace and density

A2_03 is naturally the densest Console 2 screen, but it must still preserve the system's restraint.

Do not solve density by:

- shrinking the letter into a small card;
- making analysis text tiny;
- adding scrollable mini-panels if avoidable;
- turning the analysis into a dashboard;
- packing every margin with labels.

Prefer:

- one strong document;
- one narrow analysis rail;
- one small regenerate action;
- generous margins around both.

## No animation/sound in current Console 2 phase

Do not add:

- typing animation;
- analysis reveal animation;
- paper motion;
- regeneration spinner spectacle;
- page transitions;
- sound.

Static state swaps are sufficient.

## Testing requirements

Add/update tests asserting:

- A2_03 contains generated letter body;
- A2_03 contains exactly 4 analysis categories;
- sentiment/emotion/romance are absent on A2_02 and present on A2_03;
- analysis corresponds to active result variant;
- regenerate changes body + matching analysis together;
- regenerate preserves prompt + tone values;
- BACK preserves prompt + tone values;
- retuning invalidates previous result;
- NEXT routes to shared reflection only when both console outputs exist;
- dial is inactive on A2_03;
- A2_00, A2_01 and A2_02 visual regressions remain unchanged.

## First implementation gate

Codex should implement `A2_03` only.

At completion:

1. render initial result at exactly 1440×1080;
2. capture stage-only screenshot;
3. trigger regenerate and capture variant 2 screenshot;
4. report which fixture body + analysis pair is active in each capture;
5. run typecheck/tests;
6. rerun A2_00/A2_01/A2_02 regressions;
7. STOP for visual review before wiring/finalizing the shared reflection handoff.

Do not redesign the already approved A2_00–A2_02 screens while implementing this result screen.
