# 34 — Arcade Console 2 / AI Only — Post-Generation Analysis Flow Override

**Status:** Latest product-flow authority for `A2_02` and `A2_03`.

This file records an explicit product change after review of the current `A2_02` screenshot.

Where this file conflicts with files `18`, `21`, `22`, `23`, or `24`, **this file wins** for the ordering, timing, state and presentation of Console 2 analysis.

## Product decision

The visitor must **not see sentiment / emotion / romance analysis before AI generates the AI-only letter**.

The analysis shown in the reviewed `A2_02` screenshot is therefore in the wrong place in the experience.

The new logic is:

```text
A2_00  welcome / inherited context
  ↓
A2_01  short contextual prompt
  ↓
A2_02  AI-proposed tone controls only
  ↓
      AI generates letter
  ↓
A2_03  generated AI-only letter + post-generation analysis
  ↓
shared comparison / reflection
```

No extra fifth Console 2 screen is added.

## Why

The visitor should first decide how the AI should write, then see what AI actually produces, and only then see the machine's analysis of its own generated result.

This keeps the experience sequence legible:

```text
context + short direction
→
AI proposes generation parameters
→
visitor adjusts parameters
→
AI generates
→
result is analyzed
→
visitor continues to comparison
```

Do not expose the analytical readout early as though the AI has already analyzed a letter that does not yet exist.

---

# A2_02 — Tone Controls Only

## Responsibility

`A2_02` now has **one visible responsibility only**:

> allow the visitor to review and adjust AI-proposed tone/intensity parameters before generation.

Remove from A2_02:

- sentiment analysis card;
- emotion detection card;
- romance detection card;
- analysis heading;
- analysis scores;
- analysis summaries;
- analysis icons/markers associated with those outputs.

Do not leave empty placeholder cards where analysis used to be.

## AI-proposed values remain

The five editable values remain exactly:

1. warmth
2. intimacy
3. emotional depth
4. playfulness
5. nostalgia

Starting deterministic fixture values may remain:

```text
warmth             72%
intimacy           68%
emotional depth    70%
playfulness        40%
nostalgia          55%
```

These values may still be **proposed internally from inherited Arcade 1 context + recipient/relationship context + the visitor's A2_01 prompt**.

Important distinction:

- AI may interpret context internally to propose the tone values;
- the visitor does **not** see sentiment/emotion/romance analysis at this stage.

## Recommended A2_02 copy

Replace the old heading:

```text
here’s what I understand.
```

because that heading implies visible interpretation/analysis.

Preferred default:

```text
here’s how AI will shape it.
```

Supporting line:

```text
adjust the tone before it writes.
```

Keep copy configurable in the content layer.

The voice remains neutral/computational.

## Recommended A2_02 composition

Do not preserve the old two-column `analysis | tone controls` dashboard after removing analysis.

Recompose the five tone rows as the sole main interaction.

Preferred structure at 1440×1080:

```text
persistent identity

           here’s how AI will shape it.
           adjust the tone before it writes.

           [ tone controls block ]

           warmth             slider      72%
           intimacy           slider      68%
           emotional depth    slider      70%
           playfulness        slider      40%
           nostalgia          slider      55%

------------------------------------------------ control deck
BACK     NEXT                                      INTENSITY DIAL
```

Geometry guidance:

- keep title centered in the main content region;
- center the tone-control block as one deliberate system module;
- target block width approximately `620–760px`;
- preserve generous vertical spacing between rows;
- no card container is required around the whole group;
- use restrained horizontal alignment/rules only when they help structure the rows;
- do not fill the newly available space with analytics, icons or decoration.

The screen should feel **simpler** than the reviewed screenshot, not emptier by accident.

## Dial behavior

A2_02 remains the only current Console 2 screen where the `INTENSITY DIAL` actively adjusts values.

Rules remain:

- dial changes only `activeToneControlId`;
- no active tone row -> dial changes nothing;
- dial never edits sentiment/emotion/romance;
- there is no sixth global intensity value.

## Navigation

```text
BACK -> A2_01
NEXT -> generate/select A2_03 result
```

`NEXT` commits the current tone controls to generation.

Static prototype may synchronously select deterministic result fixture data; do not add a standalone loading screen.

---

# A2_03 — Generated Letter + Post-Generation Analysis

## Responsibility

`A2_03` is now the **first place the visitor sees machine analysis in Console 2**.

The generated letter remains the visual hero.

The analysis is secondary evidence about the result AI actually produced.

## Analysis source

Analysis must correspond to the **active generated AI-only letter variant**, not merely the original prompt.

Each deterministic generated variant should own its matching analysis/insights.

Required read-only categories:

1. sentiment
2. emotion
3. romance / romantic intent
4. tone profile

The first three are the analysis responsibilities removed from A2_02.

`tone profile` summarizes the generated output and/or effective generation controls.

## Result data shape

Prefer the result to own analysis:

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

If the existing implementation uses `insights` instead of `analysis`, that name may remain, but conceptually the values are **post-generation analysis of the active result**.

Do not maintain a stale pre-generation `analysis` object and show it as though it describes every regenerated letter.

## Regenerate

On `REGENERATE`:

Preserve:

- inherited Arcade 1 context;
- recipient/relationship context;
- A2_01 prompt;
- visitor-adjusted five tone controls.

Change together:

- generated letter body;
- sentiment analysis;
- emotion analysis;
- romance analysis;
- tone profile.

All result analysis must switch to the matching active variant.

Remain on `A2_03`.

## Visual hierarchy

A2_03 should read in this order:

1. generated letter/document;
2. post-generation analysis rail;
3. regenerate action;
4. physical control deck.

The analysis must not overpower the letter.

Preferred right-side rail heading:

```text
letter analysis
```

or the currently configured equivalent.

Do not call it `analysis` in a way that visually competes with the main document.

Use the existing Console 2 black/grey/off-white/red language:

- black labels;
- muted grey explanation/confidence;
- signal red only as small marker/state accent;
- no semantic green/pink/blue coding;
- no chart library;
- no large progress rings.

## Back behavior

```text
A2_03 BACK -> A2_02
```

Returning to A2_02 allows the visitor to retune values.

Changing tone values makes the current result stale. NEXT from A2_02 generates/selects a new result and matching post-generation analysis.

---

# State-model override

The previous model treated `arcade2.analysis` as a pre-generation interpretation populated when leaving A2_01.

That behavior is now superseded.

Recommended state:

```ts
arcade2: {
  shortPrompt: string;
  proposedToneControls: ToneControlValues | null;
  toneControls: ToneControlValues;
  activeToneControlId: ToneControlId | null;
  generatedVariants: AiLetterVariant[];
  activeVariantIndex: number;
  completed: boolean;
}
```

Analysis should live with each generated result variant.

If an `analysis` field must remain temporarily for migration compatibility, it must be `null` before A2_03 and must never render on A2_02.

## A2_01 -> A2_02 trigger

When leaving A2_01:

- validate prompt;
- derive/load `proposedToneControls` fixture;
- copy proposal to editable `toneControls` if needed;
- do **not** populate visible result analysis;
- route to A2_02.

## A2_02 -> A2_03 trigger

When leaving A2_02:

- use inherited context + short prompt + current tone values;
- generate/select deterministic letter variant;
- load that variant's matching post-generation analysis;
- set active result;
- route to A2_03.

---

# Testing override

Update tests to assert:

- A2_02 renders **zero** sentiment/emotion/romance analysis cards;
- A2_02 renders exactly five editable tone controls;
- A2_02 dial edits only the active tone control;
- no letter-analysis state is visible before generation;
- A2_03 renders the generated letter;
- A2_03 renders sentiment, emotion, romance and tone profile;
- each regenerate variant changes both letter body and matching analysis;
- returning A2_03 -> A2_02 preserves prompt/tone controls;
- retuning and continuing produces a fresh result state;
- A2_00 and A2_01 regressions remain unchanged.

---

# Immediate correction for the reviewed screenshot

The current screenshot showing:

```text
analysis                 tone controls
[sentiment]
[emotion]
[romance]
```

is **not the approved final A2_02 layout**.

Codex must remove the entire left analysis column and recompose A2_02 around the five tone controls before this screen is approved.

Do not proceed to A2_03 implementation until the revised tone-only A2_02 screenshot is reviewed.

---

# Authority

For analysis timing and screen responsibility, use this precedence:

1. `34-ai-only-post-generation-analysis-flow.md`
2. later explicit user-approved overrides
3. `18-ai-only-source-of-truth.md`
4. `21-ai-only-data-state-interactions.md`
5. `22-ai-only-screen-specifications.md`
6. `23-ai-only-testing-acceptance.md`
7. `24-ai-only-codex-build-playbook.md`

Files `18`–`24` remain useful for all non-conflicting design/system details.
