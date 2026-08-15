# 21 — Arcade Console 2 / AI Only — Data, State and Interaction Model

This document defines the static-prototype state contract for Console 2 and the integration seams for later AI/hardware work.

## 1. Core principle

Console 2 should feel continuous with the visitor's existing session without repeating setup.

The implementation must separate:

- inherited session context,
- Console 2 user input,
- machine interpretation,
- AI-proposed tone controls,
- visitor-adjusted tone controls,
- active tone-control focus/selection,
- generated letter variants,
- result insights,
- semantic control-deck actions.

Do not collapse these into one arbitrary screen object.

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
    activeToneControlId: ToneControlId | null;
    generatedVariants: AiLetterVariant[];
    activeVariantIndex: number;
    completed: boolean;
  };
};
```

`activeToneControlId` exists only to identify which tone parameter the visible intensity dial may adjust. It is **not** a sixth tone value.

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

The Human + AI result remains stored for later comparison. Do not make Console 2 depend on copying the entire Console 1 generated letter unless a future product decision explicitly requires it.

## 4. Read-only analysis model

```ts
type AiOnlyAnalysis = {
  sentiment: {
    label: string;
    score?: number;
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

Recommended static step:

```ts
const TONE_STEP = 1;
```

## 6. AI proposal + visitor edit distinction

Store both:

- `proposedToneControls`
- `toneControls`

Workflow:

1. machine interpretation fixture returns a proposal,
2. copy proposal into editable `toneControls` on first entry,
3. visitor adjusts `toneControls`,
4. navigating back/forward preserves visitor values,
5. do not overwrite edits by reapplying the proposal unless the short prompt/context changes and the product logic intentionally recomputes interpretation.

This distinction matters later when comparing what AI suggested versus what the visitor controlled.

## 7. Canonical fixture values

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

Validation:

- empty prompt: NEXT disabled
- whitespace-only: invalid
- no artificial minimum beyond non-empty trimmed content
- max 120 characters enforced

Preserve prompt when navigating back/forward.

## 9. Analysis trigger

Static build:

- NEXT from `A2_01` assigns deterministic analysis fixture + proposal if required
- no fake delay
- no standalone loading page

Future production AI may introduce local pending state, but not a new full-screen composition without design approval.

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

Current locked behaviour:

```text
A2_03
  regenerate
    -> keep inherited context
    -> keep prompt
    -> keep analysis
    -> keep current tone values
    -> increment activeVariantIndex cyclically
    -> update letter + matching insights
    -> remain A2_03
```

Static implementation:

```ts
nextIndex = (currentIndex + 1) % generatedVariants.length;
```

Do not reset controls.
Do not navigate to `A2_02`.
Do not clear prompt.

## 12. Continue behaviour from result

Guard:

- active AI-only letter exists
- Arcade 1 comparison result exists

Then route to the first shared reflection screen.

Do not append extra Console 2 completion screens.

## 13. Semantic actions

Console 2 now has a visible physical-control deck, but UI actions must still be modeled semantically so future real hardware can dispatch the same actions.

Recommended action names:

```ts
type SemanticAction =
  | 'BACK'
  | 'NEXT'
  | 'BEGIN'
  | 'CONTINUE'
  | 'REGENERATE'
  | 'FOCUS_PREVIOUS'
  | 'FOCUS_NEXT'
  | 'DECREMENT'
  | 'INCREMENT'
  | 'CONFIRM';
```

Recommended mapping:

```text
visible BACK deck button -> BACK
visible NEXT deck button -> BEGIN on A2_00, CONTINUE on A2_01/A2_02/A2_03
visible intensity dial -> DECREMENT / INCREMENT for active tone control on A2_02
software regenerate action -> REGENERATE on A2_03
```

Do not couple the visual button component directly to route names.

## 14. Persistent control-deck state model

The deck remains mounted on every `A2_*` screen.

Suggested derived configuration:

```ts
type AiDeckState = {
  backEnabled: boolean;
  nextEnabled: boolean;
  dialEnabled: boolean;
  activeToneControlId: ToneControlId | null;
};
```

Screen derivation:

```text
A2_00: back false, next true,  dial false
A2_01: back true,  next prompt-valid, dial false
A2_02: back true,  next true,  dial active only when tone row selected/focused
A2_03: back true,  next true,  dial false
```

Do not remove unavailable hardware from the layout; change its enabled state only.

## 15. Dial-to-tone interaction contract

The dial is a **controller for the active tone row**, not an independent model value.

Rules:

1. `activeToneControlId === null` -> dial changes nothing.
2. Focusing/selecting a tone control sets `activeToneControlId`.
3. Dial increment/decrement changes only `toneControls[activeToneControlId]`.
4. Clamp value to 0–100.
5. Respect `TONE_STEP`.
6. Dial indicator may mirror that active value visually.
7. Moving to another tone row changes which value the dial controls.
8. Leaving `A2_02` may clear `activeToneControlId` without altering tone values.

Example:

```ts
function adjustActiveTone(delta: number) {
  if (!activeToneControlId) return;
  const current = toneControls[activeToneControlId];
  toneControls[activeToneControlId] = clamp(current + delta, 0, 100);
}
```

Do not let the dial change sentiment/emotion/romance analysis.

## 16. Keyboard development mapping

Suggested development-only mapping:

- `ArrowUp` / `ArrowDown` = move tone focus on `A2_02`
- `ArrowLeft` / `ArrowRight` = decrement/increment active tone value when appropriate
- `Enter` = NEXT/confirm when valid
- `Escape` or guarded `Backspace` = BACK
- `R` on `A2_03` may trigger regenerate if focus is not inside text input

Keyboard shortcuts are implementation conveniences, not extra visible UI copy.

## 17. Prompt-change invalidation

If visitor changes short prompt after analysis/result state exists:

```ts
onShortPromptChanged() {
  analysis = null;
  proposedToneControls = null;
  generatedVariants = [];
  activeVariantIndex = 0;
  activeToneControlId = null;
  completed = false;
}
```

Do not clear inherited Arcade 1 context.

## 18. Tone edit invalidation

Changing tone controls after returning from result makes the previous result stale.

On NEXT from `A2_02`, static build may reselect/generate deterministic fixtures from current controls and set active variant to 0.

Do not silently show an old result as if it came from new values.

## 19. No persistence/network requirement in static phase

Use local in-memory/session fixture state.

Do not add:

- API keys
- OpenAI calls
- database schema
- authentication
- new persistence unless existing project architecture already requires it

## 20. Real hardware integration is deferred

Current scope includes the **on-screen visual representation and semantic behavior** of BACK/NEXT/dial.

Do not add:

- serial port access
- MIDI wiring
- Arduino libraries
- WebSerial permissions
- hardware polling loops

Later hardware should dispatch the same semantic actions defined here.

## 21. Testable invariants

Tests must assert:

- Console 2 opens with inherited first name
- no recipient/relationship form exists
- empty prompt cannot NEXT
- analysis has exactly sentiment/emotion/romance read-only blocks
- tone controls have exactly five editable values in canonical order
- tone edits survive navigation
- deck remains mounted with stable geometry
- dial changes only active tone row
- dial is inert when no tone row is active
- regenerate preserves prompt + tone controls
- regenerate changes active result fixture
- result insight rail includes emotion
- NEXT from result enters shared reflection
- no Console 1 visual-shell component mounts on any `A2_*` route.