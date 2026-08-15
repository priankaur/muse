# 21 — Arcade Console 2 / AI Only — Data, State and Interaction Model

This document defines the static-prototype state contract for Console 2 and the integration seams for later AI/hardware work.

## 1. Core principle

Console 2 should feel continuous with the visitor's existing session without repeating setup.

The implementation must separate:

- inherited session context,
- Console 2 user input,
- machine interpretation,
- user-adjustable tone controls,
- generated letter variants,
- result insights.

Do not collapse all of these into one arbitrary screen object.

## 2. Recommended session shape

Adapt to existing project conventions, but preserve these conceptual fields:

```ts
type MuseSession = {
  visitor: {
    id: string;
    firstName: string;
  };

  recipient: {
    name: string;
    relationship: string;
  };

  arcade1: {
    completed: boolean;
    humanSourceContext?: string;
    humanAiLetter?: string;
    contextForArcade2?: string;
  };

  arcade2: {
    started: boolean;
    shortPrompt: string;
    analysis: AiOnlyAnalysis | null;
    proposedToneControls: ToneControlValues | null;
    toneControls: ToneControlValues;
    generatedVariants: AiLetterVariant[];
    activeVariantIndex: number;
    completed: boolean;
  };
};
```

## 3. Context passed into Console 2

Define an explicit selector rather than passing the entire session object into future AI services.

```ts
type AiOnlyContextInput = {
  visitorFirstName: string;
  recipientName: string;
  relationship: string;
  arcade1Context: string;
  shortPrompt: string;
};
```

Current analysis/generation uses all five fields.

### Arcade 1 context recommendation

Use a curated `contextForArcade2` field derived from visitor-originated material/context from the first experience rather than blindly serializing every Arcade 1 UI value.

The Human + AI result itself remains stored for later comparison. Do not make the implementation depend on copying the entire generated Console 1 letter into Console 2 unless a future product decision explicitly requires that.

## 4. Read-only analysis model

```ts
type AiOnlyAnalysis = {
  sentiment: {
    label: string;
    score?: number;      // 0..100, fixture only if displayed
    summary: string;
  };
  emotion: {
    label: string;
    score?: number;
    summary: string;
    dominant?: string[];
  };
  romance: {
    label: string;
    score?: number;
    summary: string;
  };
};
```

These metrics are **not controls**.

Do not provide sliders/toggles/edit states for sentiment, emotion or romance.

## 5. Tone-control model

```ts
type ToneControlId =
  | 'warmth'
  | 'intimacy'
  | 'emotionalDepth'
  | 'playfulness'
  | 'nostalgia';

type ToneControlValues = Record<ToneControlId, number>;
```

Values are normalized 0–100.

Recommended default step for static mouse/keyboard controls:

```ts
const TONE_STEP = 1;
```

For future physical dial integration, the semantic input layer may map one detent to 1 or 5 percentage points without changing component geometry.

## 6. AI proposal + user edit distinction

Store both:

- `proposedToneControls`
- `toneControls`

Workflow:

1. machine interpretation fixture returns a proposal,
2. copy proposal into editable tone controls on first entry,
3. visitor adjusts `toneControls`,
4. navigating back/forward preserves visitor values,
5. do not overwrite visitor edits by reapplying proposal unless the short prompt/context actually changes and product logic explicitly recomputes analysis.

This distinction will matter later when comparing what AI suggested versus what the visitor controlled.

## 7. Canonical fixture values

For the first static reference-aligned fixture, use values close to the canonical montage:

```ts
const DEFAULT_ANALYSIS: AiOnlyAnalysis = {
  sentiment: {
    label: 'positive',
    score: 62,
    summary: 'overall sentiment is positive with moments of vulnerability.'
  },
  emotion: {
    label: 'love, longing, and hope',
    score: 71,
    summary: 'love, longing, and hope are the dominant emotions.',
    dominant: ['love', 'longing', 'hope']
  },
  romance: {
    label: 'clear romantic intent',
    score: 68,
    summary: 'clear romantic intent with a desire for closeness and reassurance.'
  }
};

const DEFAULT_TONE_CONTROLS: ToneControlValues = {
  warmth: 72,
  intimacy: 68,
  emotionalDepth: 70,
  playfulness: 40,
  nostalgia: 55
};
```

These are static design fixtures, not scientific claims.

## 8. Prompt model

Current cap:

```ts
const AI_ONLY_PROMPT_MAX = 120;
```

Recommended validation:

- empty prompt: continue disabled
- whitespace-only prompt: invalid
- minimum meaningful content: no artificial word minimum beyond non-empty trimmed string unless research later requires it
- max 120 characters enforced by input

Preserve prompt when navigating back/forward.

## 9. Analysis trigger

Static build:

- on continue from `A2_01`, assign deterministic analysis fixture + proposal if not already present
- no fake delay required
- no standalone loading page

Later production build:

- same transition may enter a local pending state
- pending state should not become a new full-screen composition without design approval

## 10. Result variant model

```ts
type AiLetterVariant = {
  id: string;
  body: string;
  insights: {
    sentiment: InsightMetric;
    emotion: InsightMetric;
    romance: InsightMetric;
    toneProfile: string[];
  };
};
```

Provide at least 3 deterministic fixture variants for regenerate testing.

## 11. Regenerate behaviour

Current locked recommendation:

```text
A2_03
  regenerate
    -> keep prompt
    -> keep analysis
    -> keep current tone values
    -> increment activeVariantIndex cyclically
    -> update letter + insights
    -> remain A2_03
```

Static implementation:

```ts
nextIndex = (currentIndex + 1) % generatedVariants.length;
```

Do not reset controls.
Do not navigate to `A2_02`.
Do not clear prompt.

Back from result goes to `A2_02`, where current editable values remain.

## 12. Continue behaviour from result

Guard:

- active AI-only letter exists
- Arcade 1 comparison result exists

Then:

```text
A2_03 -> R_01
```

or the current first route in the shared reflection registry.

Do not append extra Console 2 completion screens.

## 13. Semantic actions

Keep visible text navigation decoupled from future hardware input.

Recommended action names:

```ts
type SemanticAction =
  | 'BACK'
  | 'CONTINUE'
  | 'BEGIN'
  | 'REGENERATE'
  | 'FOCUS_PREVIOUS'
  | 'FOCUS_NEXT'
  | 'DECREMENT'
  | 'INCREMENT'
  | 'CONFIRM';
```

For current build, mouse/keyboard can dispatch these actions.

Do not render the physical control legend on Console 2.

## 14. Keyboard development mapping

Suggested development-only mapping:

- `ArrowLeft` = context-sensitive decrement/previous
- `ArrowRight` = increment/next
- `ArrowUp` / `ArrowDown` = move between tone controls
- `Enter` = confirm/continue when valid
- `Escape` or `Backspace` with appropriate guard = back
- `R` on result screen may trigger regenerate in development if it does not interfere with text input

Keyboard shortcuts are implementation conveniences, not visible UI copy.

## 15. Analysis recomputation rule

If visitor goes back and changes the short prompt:

- static build may deterministically reset analysis/proposed controls to the fixture set appropriate to the prompt fixture strategy
- preserve architecture so production AI can recompute
- if prompt changes, current generated variants should be considered stale and reset

Recommended invalidation:

```ts
onShortPromptChanged() {
  analysis = null;
  proposedToneControls = null;
  generatedVariants = [];
  activeVariantIndex = 0;
  completed = false;
}
```

Do not clear inherited Arcade 1 context.

## 16. Tone edit invalidation

Changing tone controls after returning from the result means the previous generated result is stale.

On continue from `A2_02`, static build may reselect/generate fixtures based on current controls and set active variant to 0.

Do not silently show the old result as if generated from new values.

## 17. No persistence/network requirement in static phase

Use local in-memory/session fixture state.

Do not add:

- API keys
- OpenAI calls
- localStorage persistence unless existing project architecture already requires it
- database schema
- authentication

## 18. Testable invariants

Tests must assert:

- Console 2 opens with inherited first name
- no recipient/relationship form exists in Console 2
- empty short prompt cannot continue
- analysis has exactly sentiment/emotion/romance read-only cards
- tone controls have exactly five editable values in canonical order
- tone edits survive navigation to result and back
- regenerate preserves prompt + tone controls
- regenerate changes active fixture variant
- result insight rail includes emotion
- continue from result enters shared reflection
- no Console 1 visual-shell component mounts on any `A2_*` route.