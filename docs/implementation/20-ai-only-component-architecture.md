# 20 — Arcade Console 2 / AI Only — Component Architecture

Console 2 must be implemented as a distinct visual system. Reuse application logic where sensible, but do not theme Console 1 components to imitate this design.

## 1. Folder recommendation

```text
src/
  app/
    stage/
      FixedStage.tsx
      FixedStage.module.css
    session/
      MuseSessionContext.tsx
      museSession.types.ts
    navigation/
      screenRegistry.ts
      useExperienceNavigation.ts
      semanticActions.ts

  console1/
    ... existing Human + AI components

  console2/
    AiOnlyShell.tsx
    AiOnlyShell.module.css

    components/
      AiOnlyIdentity.tsx
      AiOnlyIdentity.module.css
      AiPromptField.tsx
      AiPromptField.module.css
      AiNavigation.tsx
      AiNavigation.module.css
      AnalysisCard.tsx
      AnalysisCard.module.css
      AnalysisStack.tsx
      ToneControl.tsx
      ToneControl.module.css
      ToneControls.tsx
      ContextSignal.tsx
      ContextSignal.module.css
      AiLetterDocument.tsx
      AiLetterDocument.module.css
      LetterInsights.tsx
      LetterInsights.module.css
      InsightCard.tsx
      InsightCard.module.css

    screens/
      AiWelcomeScreen.tsx
      AiPromptScreen.tsx
      AiInterpretationScreen.tsx
      AiLetterResultScreen.tsx

    content/
      aiOnlyCopy.ts
      aiOnlyFixtures.ts
      toneControls.ts

    styles/
      aiOnly.tokens.css
      aiOnly.global.css

  reflection/
    ... shared post-console flow
```

Names may follow existing repo conventions, but architectural boundaries should remain.

## 2. What may be shared across consoles

Safe shared implementation:

- fixed 1440×1080 stage scaler
- viewport centering
- session state/types
- screen registry/state machine
- semantic input abstraction
- fixture utilities
- Playwright helpers
- route guards

Do not duplicate those purely for visual separation.

## 3. What must NOT be shared visually

Do not render Console 2 using:

- `MuseWindow`
- `ArcadeBackground`
- `OuterHud`
- `FloatingSpriteLayer`
- `HardwareControlStrip`
- `PrimaryCta`
- `PixelTextField`
- `ChoiceTag`
- Console 1 typography primitives

Do not add `variant="aiOnly"` to a pixel component just to avoid making the correct Console 2 component.

## 4. `AiOnlyShell`

Responsibilities:

- own warm off-white background
- render subtle inset perimeter frame
- render persistent `AiOnlyIdentity`
- expose a deterministic content coordinate system
- render screen body via `children`
- render navigation slots if screen configuration requests them

Suggested interface:

```ts
type AiOnlyShellProps = {
  children: React.ReactNode;
  nav?: {
    back?: () => void;
    continue?: () => void;
    regenerate?: () => void;
    continueDisabled?: boolean;
  };
};
```

The shell should not know screen-specific copy.

## 5. Layout primitives

Prefer a small set of structural classes/primitives rather than arbitrary screen CSS.

Recommended:

- `.aiStageContent`
- `.aiCenteredHero`
- `.aiScreenTitle`
- `.aiSectionLabel`
- `.aiTwoColumn`
- `.aiResultGrid`
- `.aiBottomNav`

Do not create a generic 12-column SaaS grid. The reference uses bespoke editorial alignment.

## 6. `AiOnlyIdentity`

Content is fixed by system identity, not screen copy:

```text
MUSE
AI ONLY
ARCADE CONSOLE 2
```

No screen number prop.
No console icon prop.
No badge variant.

## 7. `AiNavigation`

Single component renders the three canonical actions in fixed locations:

- back — left
- regenerate — center
- continue — right

Screens pass only actions/visibility/disabled state.

Avoid individual screens manually positioning links.

Keyboard-accessible buttons are preferable semantically, styled to look like text links.

Example:

```tsx
<button className={styles.textAction} onClick={onContinue}>
  continue <span aria-hidden>→</span>
</button>
```

Do not use anchors for application state changes.

## 8. `AiPromptField`

Responsibilities:

- controlled textarea
- 120-character max by current config
- display example/placeholder
- character count
- expose value + change
- keyboard focus state
- no domain logic

Suggested props:

```ts
type AiPromptFieldProps = {
  value: string;
  onChange: (value: string) => void;
  maxLength: number;
  placeholder: string;
  ariaLabel: string;
};
```

## 9. `AnalysisCard`

Read-only presentation only.

```ts
type AnalysisKind = 'sentiment' | 'emotion' | 'romance';

type AnalysisCardProps = {
  kind: AnalysisKind;
  label: string;
  score?: number;
  summary: string;
};
```

The production AI may later provide confidence/score data. Static fixture values are allowed now.

Do not make the card editable.
Do not convert it into a selectable control.

## 10. `ToneControl`

Editable parameter component.

```ts
type ToneControlProps = {
  id: ToneControlId;
  label: string;
  value: number;        // 0..100
  min?: number;         // default 0
  max?: number;         // default 100
  step?: number;        // recommended 1 or 5
  onChange: (value: number) => void;
};
```

Use a native `<input type="range">` where possible for robustness/accessibility, fully visually styled to match reference.

The visual thumb/track should not rely on browser defaults.

## 11. `ToneControls`

Container owns order, not individual screens.

Canonical order:

```ts
[
  'warmth',
  'intimacy',
  'emotionalDepth',
  'playfulness',
  'nostalgia'
]
```

Do not reorder based on values.

## 12. `ContextSignal`

Welcome screen reference includes a restrained central dotted/radial context-loaded signal.

Current static implementation can create this with CSS/SVG only.

Rules:

- monochrome neutral dots/lines
- tiny blue center accent
- approximately 160–190px diameter
- no animation
- no glowing particles
- no data labels
- no scientific chart semantics

It is a visual acknowledgement of context transfer, not an analytical visualization.

## 13. `AiLetterDocument`

Responsibilities:

- typed letter display
- optional layered outline sheets behind main page
- scroll handling only if absolutely necessary
- no editing in current result screen
- no decorative personalisation in first build

Props:

```ts
type AiLetterDocumentProps = {
  letter: string;
  recipientName?: string;
  variantIndex?: number;
};
```

Do not render markdown styling from arbitrary generated output. Convert/normalize output to safe plain paragraphs.

## 14. `LetterInsights`

Contains exactly four insight sections in current build:

1. sentiment
2. emotion
3. romance
4. tone profile

Suggested data:

```ts
type LetterInsightsData = {
  sentiment: InsightMetric;
  emotion: InsightMetric;
  romance: InsightMetric;
  toneProfile: {
    labels: string[];
  };
};
```

All values are read-only.

## 15. Icon strategy

Create four tiny purpose-built SVG/CSS icons:

- sentiment: simple heart outline
- emotion: simple face/circle expression glyph
- romance: simple sparkle/star glyph
- tone profile: simple waveform/equalizer glyph

Use `currentColor`.
No icon package.
No filled emoji.
No multicolor icons.

## 16. Screen responsibilities

### `AiWelcomeScreen`

Owns only:

- personalized welcome copy
- inherited-context sentence
- `ContextSignal`
- begin action

### `AiPromptScreen`

Owns:

- title
- subtitle
- prompt field
- back/continue

### `AiInterpretationScreen`

Owns:

- screen title
- left analysis column
- right tone-control column
- back/continue

Analysis and tuning intentionally coexist on the same screen in the canonical reference.

### `AiLetterResultScreen`

Owns:

- letter document
- insight rail
- back/regenerate/continue

No additional title is required unless a later reference explicitly adds one.

## 17. State isolation

Components must be deterministic from props/session state. Avoid local duplicate copies of global session values.

`AiPromptScreen` may use controlled draft state, but commit to session on every change or on continue according to existing architecture.

`AiInterpretationScreen` writes tone controls to `session.arcade2.toneControls`.

`AiLetterResultScreen` reads the active fixture/result by index.

## 18. Error/empty state strategy for static build

Do not design visible error banners now.

Development guards may render a plain developer-only fallback outside screenshot tests if required.

Production-facing error treatment should be designed later with AI integration.

## 19. No motion architecture dependency

Do not install an animation library.
Do not wrap components in motion primitives.
Do not create timers solely for visual effects.

Keep component APIs motion-agnostic so animation can be layered later.

## 20. Component completion rule

A component is not complete merely because it is reusable. It is complete only when:

- it visually matches the canonical reference,
- it consumes shared tokens,
- it has no Console 1 styling dependency,
- it is keyboard accessible where interactive,
- it passes screenshot regression in its actual screen composition.