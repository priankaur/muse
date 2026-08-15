# 29 — Arcade Console 1 / Human + AI — Human Letter Analysis

This file adds a structured analysis step to Arcade 1 after the visitor accepts the captured handwritten letter and before they provide optional notes/tuning.

The purpose is to make visible what the machine has recognized from the visitor's **human-originated letter** before AI enhancement begins.

## 1. Product intent

Arcade 1 demonstrates Human + AI collaboration. The machine should first acknowledge/interrogate the material the visitor created themselves.

The analysis is not the final letter result and must not dominate the experience. It is a transparent readback of what the system detected before enhancement.

The four required outputs are:

1. sentiment analysis;
2. emotions recognized;
3. character count;
4. visual meaning.

## 2. Recommended flow placement

Insert one new responsibility after `A1_06 — Photo review` is accepted and before `A1_07 — Notes for AI`.

Use a non-disruptive screen ID so existing downstream IDs do not need renumbering:

```text
A1_06A — Human Letter Analysis
```

Flow becomes:

```text
A1_05 capture
-> A1_06 review
-> A1_06A human-letter analysis
-> A1_07 notes for AI
-> A1_08 tune enhancement
-> A1_09 processing
-> A1_10 result
```

If the screen registry does not support alphanumeric IDs cleanly, use an internal stable enum/key while preserving existing public IDs. Do not renumber A1_07–A1_11 merely for convenience.

## 3. Visual design

Use the **locked Arcade 1 visual system** only.

Do not copy Console 2 analysis cards.

The analysis must look like it belongs inside the pale-lavender MuseWindow:

- pixel typography;
- dark navy/purple ink;
- magenta/purple/yellow accents only from the existing Arcade 1 palette;
- stepped pixel outlines;
- no modern SaaS cards;
- no blue/grey Console 2 analytics language;
- no charts unless explicitly approved later.

Recommended layout inside the main window:

```text
TITLE / INTRO

[ sentiment ]       [ emotions recognized ]
[ character count ] [ visual meaning      ]

CONTINUE CTA
```

Use four compact pixel panels or two stacked rows. Keep the window spacious.

## 4. Screen title / copy direction

Keep copy collaborative and transparent.

Recommended configurable title:

```text
HERE'S WHAT THE MACHINE PICKED UP
```

Supporting line:

```text
A quick read of your letter before AI adds anything to it.
```

This is recommended fixture copy, not a permanent immutable sentence. Store in content config.

Avoid:

- `AI knows how you feel`;
- `we understand your emotions`;
- diagnostic/clinical claims;
- language implying the analysis is objectively correct.

## 5. Analysis data model

Add a structured model similar to:

```ts
type HumanLetterAnalysis = {
  sentiment: {
    label: string;
    score?: number;      // 0..100 only if displayed
    summary?: string;
  };

  emotions: Array<{
    label: string;
    confidence?: number; // optional fixture/prod value
  }>;

  characterCount: {
    characters: number;
    charactersWithoutSpaces?: number;
  };

  visualMeaning: {
    summary: string;
    cues?: Array<{
      type: 'symbol' | 'doodle' | 'color' | 'layout' | 'mark' | 'other';
      label: string;
      interpretation?: string;
      confidence?: number;
    }>;
  };
};
```

Store this under Arcade 1 session state, for example:

```ts
arcade1.humanLetterAnalysis
```

Do not reuse the Console 2 `AiOnlyAnalysis` type because the analysis source and visual meaning field are different.

## 6. Source material

Production analysis will eventually derive from:

- OCR/handwriting extraction from the selected capture;
- visible symbols/doodles/layout/color cues from the selected image;
- recipient/relationship context where appropriate.

Current prototype must use deterministic fixture data.

Do not make production AI/vision calls in this task unless separately approved.

## 7. Sentiment analysis

Display a concise label plus optional numeric score/summary.

Example fixture:

```text
SENTIMENT
warm + reflective
72 / 100
```

or, if numeric scores feel too clinical in visual review:

```text
SENTIMENT
warm + reflective
```

The data model may still retain a score even if the UI does not show it.

Do not semantic-color positive/negative sentiment using traffic-light colors.

Use existing Arcade 1 visual accents.

## 8. Emotions recognized

Recognize a small set, not an exhaustive taxonomy.

Recommended visible maximum:

```text
3 emotions
```

Example fixture:

```text
EMOTIONS RECOGNIZED
love
nostalgia
longing
```

Use pixel tags, compact stacked labels or a simple text list consistent with Arcade 1.

Do not show 10–20 emotion labels.

Do not imply diagnosis.

## 9. Character count

This count refers to the **recognized/extracted human letter content**, not the optional 120-character machine note.

Display:

```text
CHARACTERS RECOGNIZED
384
```

or equivalent concise wording.

If OCR extraction is unavailable in the static prototype, use a deterministic fixture count associated with the fixture capture.

Keep the existing A1_07 note character counter separately; these are two different concepts.

## 10. Visual meaning

`VISUAL MEANING` means the machine's interpretation of visible non-text cues in the human-created letter.

It is not objective truth.

Examples of cues:

- heart doodles;
- underlined words;
- repeated symbols;
- handwritten emphasis;
- color use;
- collage/cutout presence;
- page density/spacing;
- crossed-out/revised text;
- arrows or connecting marks.

Recommended fixture:

```text
VISUAL MEANING
heart doodles + highlighted phrases suggest emphasis on affection and closeness.
```

Better internal wording in the component can use a qualifier such as:

```text
AI interpretation of visible cues
```

Do not infer highly specific psychological meaning from color/doodles without uncertainty language.

## 11. Confidence / uncertainty

For production-readiness, the structured model may include confidence values, but the first visual build does not need confidence percentages everywhere.

Prefer readable, non-clinical output.

If a cue is uncertain, phrase it as:

- `may suggest`;
- `appears to emphasize`;
- `visible cues include`.

## 12. CTA / navigation

Primary CTA:

```text
CONTINUE
```

or current approved Arcade 1 forward action copy.

Back should return to photo review if supported by the existing semantic navigation model.

Do not allow editing of the analysis itself in this first version.

The next screen (`A1_07`) is where the visitor can add a short note/correction for the machine.

This creates a useful interaction logic:

```text
machine shows what it recognized
-> visitor gets a chance to add/correct context
-> visitor tunes AI enhancement
```

## 13. Fixture strategy

Create deterministic fixture analysis tied to the fixture letter image.

Example:

```ts
const HUMAN_LETTER_ANALYSIS_FIXTURE = {
  sentiment: {
    label: 'warm + reflective',
    score: 72,
    summary: 'The letter reads as affectionate with reflective moments.'
  },
  emotions: [
    { label: 'love', confidence: 0.88 },
    { label: 'nostalgia', confidence: 0.76 },
    { label: 'longing', confidence: 0.69 }
  ],
  characterCount: {
    characters: 384,
    charactersWithoutSpaces: 322
  },
  visualMeaning: {
    summary: 'Heart doodles and emphasized phrases appear to reinforce affection and closeness.',
    cues: [
      { type: 'doodle', label: 'heart doodles', interpretation: 'affection emphasis', confidence: 0.81 },
      { type: 'mark', label: 'underlined phrases', interpretation: 'intentional emphasis', confidence: 0.84 }
    ]
  }
};
```

These values are design/test fixtures only.

## 14. Processing state

Because real vision/OCR is deferred, do not add a long fake loading screen.

When production analysis is added later, the same screen may support:

```text
idle -> analyzing -> success -> recoverable error
```

For the current fixture build, navigation may enter `A1_06A` already populated or use a very short deterministic scan state if the motion plan is being implemented.

## 15. Testing

Add tests for:

- accepting photo review routes to `A1_06A`;
- analysis renders exactly four required categories;
- emotions visible count does not exceed configured maximum;
- character count is taken from human-letter analysis fixture, not note-field length;
- visual meaning renders from structured config;
- continue routes to `A1_07`;
- back returns to review where supported;
- no Console 2 component classes/shell are used.

## 16. Visual regression

Capture a 1440×1080 stage-only screenshot for `A1_06A`.

Review for:

- locked MuseWindow unchanged;
- no generic dashboard/card feel;
- four outputs readable without crowding;
- CTA/hardware strip unchanged;
- analysis feels like part of the arcade system.

## 17. Future AI/vision integration seam

Create an interface such as:

```ts
interface HumanLetterAnalysisService {
  analyze(input: HumanLetterAnalysisInput): Promise<HumanLetterAnalysis>;
}
```

Current implementation uses a fixture service.

Future service may use OCR/vision/model APIs without changing the screen component contract.

Do not put provider-specific response parsing directly in `A1_06A`.

## 18. Anti-drift rules

Do not:

- turn Arcade 1 into the Console 2 analytics UI;
- use clinical dashboards;
- add charts/radar graphs;
- add modern progress rings;
- semantic-color emotions;
- remove the visitor's correction/notes opportunity;
- treat visual meaning as objective fact;
- renumber all downstream screens unnecessarily.
