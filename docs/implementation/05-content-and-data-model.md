# 05 — Content and Data Model

## Principle

The copy will continue to evolve. The interface should not need structural edits every time wording changes.

Store content separately from visual components and store visitor/session data separately from content.

## Content architecture

Suggested files:

```text
src/content/
├── screenCopy.ts
├── relationshipOptions.ts
├── tuningControls.ts
├── reflectionQuestions.ts
└── fixtures.ts
```

A screen component should receive content through typed objects.

Example:

```ts
interface NarrativeScreenContent {
  heading?: string;
  greeting?: string;
  paragraphs: RichTextBlock[];
  cta: string;
}
```

Do not hard-code copy inside reusable window, CTA, tag or typography components.

## Rich-text emphasis

Narrative copy may contain highlighted phrases. Represent them structurally rather than embedding HTML strings.

Example:

```ts
type RichTextSpan = {
  text: string;
  emphasis?: 'pink-box' | 'purple-box';
};
```

This prevents screen copy from reaching into CSS classes directly.

## Session model

Use a single in-memory `MuseSession` during the static phase.

Suggested shape:

```ts
interface MuseSession {
  visitor: {
    id: string;
    firstName: string;
    age?: number;
    sex?: string;
  };

  recipient?: {
    name: string;
    relationship: RelationshipValue;
    relationshipOther?: string;
  };

  arcade1: {
    handwrittenLetterImage?: DemoImageRef;
    photoAttempt?: 1 | 2 | 3;
    machineNotes?: string;
    tuning?: Record<string, number>;
    enhancedLetter?: string;
  };

  arcade2: {
    shortPrompt?: string;
    analysis?: {
      sentiment?: string;
      emotions?: string[];
      romanceIntent?: string;
    };
    intensities?: Record<string, number>;
    generatedLetter?: string;
  };

  reflection: {
    answers: Record<string, string | string[]>;
    chosenLetter?: 'human-ai' | 'ai-only';
    stance?: 'convenience' | 'control' | 'more-human';
  };
}
```

## Registration data

Current early registration material indicates first-name-centric visitor identity plus age/sex context. Registration requirements have changed during exploration; keep the model permissive and do not let the main arcade screens depend on fields that are not required for their copy.

For the static phase, seed registration fixtures so Arcade 1 can render `HELLO, [USER NAME]`.

## Recipient data

Arcade 1 owns:

- recipient name,
- relationship category,
- free-text relationship when `Other` is selected.

Arcade 2 inherits these values and must not ask for them again.

## Relationship options

Current screen options:

- Partner
- Crush
- Girlfriend / Boyfriend
- Sibling
- Parent
- Son
- Daughter
- Other

Keep these in content configuration. Do not encode them as separate components.

When `Other` is selected, show the associated text field. For the static prototype it may remain visible in the layout but disabled/visually inactive until selected if that better matches the approved design.

## Fixture AI outputs

Use deterministic fixture strings for:

- Human + AI enhanced letter.
- AI-only generated letter.
- sentiment analysis.
- detected emotions.
- romantic-intent classification.

The fixtures should be believable enough to exercise long and short text layouts but must be clearly located in `fixtures.ts` so they cannot be mistaken for real model output.

## Required-data guards

Before entering Arcade 2, the state machine should verify:

- visitor first name exists,
- recipient name exists,
- relationship exists,
- Arcade 1 result exists or a fixture has been created.

If required state is missing, route to a recoverable development/session-error state rather than showing blank placeholders.

## Content token interpolation

Use a small controlled interpolation layer for dynamic copy:

- `[User Name]`
- `[Recipient Name]`

Prefer typed functions over generic template evaluation.

Example:

```ts
const greeting = getGreeting(session.visitor.firstName);
```

Do not evaluate arbitrary strings as code.
