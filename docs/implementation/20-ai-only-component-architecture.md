# 20 — Arcade Console 2 / AI Only — Component Architecture

Console 2 is a distinct visual system. Reuse application logic where sensible, but do not theme Console 1 components to imitate this design.

The latest system refinement adds a monochrome lower physical-control deck, red signal markers, strong rules/separators and heavier editorial typography. These are Console 2-specific components, not reused Console 1 hardware.

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
      AiDisplayTitle.tsx
      SystemStatusLine.tsx
      SignalMarker.tsx
      SystemRule.tsx

      AiControlDeck.tsx
      AiControlDeck.module.css
      AiArcadeButton.tsx
      AiArcadeButton.module.css
      AiRotaryDial.tsx
      AiRotaryDial.module.css
      AiRegenerateAction.tsx

      AiPromptField.tsx
      AiPromptField.module.css
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

Names may follow existing repository conventions, but these architectural boundaries should remain.

## 2. What may be shared across consoles

Safe shared implementation:

- fixed 1440×1080 stage scaler
- viewport centering
- session state/types
- screen registry/state machine
- semantic action abstraction
- fixture utilities
- Playwright helpers
- route guards

Do not duplicate these purely for visual separation.

## 3. What must NOT be shared visually

Do not render Console 2 using:

- `MuseWindow`
- `ArcadeBackground`
- `OuterHud`
- `FloatingSpriteLayer`
- Console 1 `HardwareControlStrip`
- Console 1 `ArcadeButton3D`
- Console 1 `RotaryDial3D`
- `PrimaryCta`
- `PixelTextField`
- `ChoiceTag`
- Console 1 typography primitives

Do not add `variant="aiOnly"` to a pixel component merely to avoid creating the correct Console 2 component.

## 4. `AiOnlyShell`

Responsibilities:

- own warm off-white main background
- render optional subtle perimeter hairline if retained after calibration
- render persistent `AiOnlyIdentity`
- expose deterministic content coordinates
- render screen body via `children`
- render the strong shared horizontal rule above the lower control deck
- render the persistent `AiControlDeck`

Suggested interface:

```ts
type AiOnlyShellProps = {
  children: React.ReactNode;
  controls: {
    back?: {
      enabled: boolean;
      onPress?: () => void;
    };
    next?: {
      enabled: boolean;
      onPress?: () => void;
      label?: string;
    };
    dial?: {
      enabled: boolean;
      value?: number;
      min?: number;
      max?: number;
      onChange?: (value: number) => void;
      label?: string;
    };
  };
};
```

The shell must not know screen-specific copy.

## 5. Vertical structure

Console 2 uses a fixed two-region structure:

```text
Main content: y 0–888
Control deck: y 888–1080
```

The deck position and height are shared tokens. Individual screens must not move or resize it.

## 6. Layout primitives

Prefer a small set of structural classes/primitives:

- `.aiStageContent`
- `.aiCenteredHero`
- `.aiDisplayTitle`
- `.aiScreenTitle`
- `.aiSystemLabel`
- `.aiTwoColumn`
- `.aiResultGrid`
- `.aiControlDeck`

Do not create a generic 12-column SaaS grid.

## 7. `AiOnlyIdentity`

Fixed content:

```text
MUSE
AI ONLY
ARCADE CONSOLE 2
```

Rules:

- `MUSE` line uses heavy condensed display character
- top-left only
- no screen number prop
- no icon prop
- no badge variant
- no bottom-center duplicate

## 8. `AiDisplayTitle`

Use for large title roles where the screen spec requests strong editorial display hierarchy.

Props:

```ts
type AiDisplayTitleProps = {
  children: React.ReactNode;
  size?: 'xl' | 'lg' | 'screen';
  align?: 'left' | 'center';
};
```

It consumes the heavy condensed typography tokens from `19-ai-only-visual-system.md`.

Do not hardcode the phrase `DIGITAL LOVE LETTER`; that phrase belongs only to the visual reference.

## 9. `SignalMarker`

Tiny red square used as a micro-accent anchor.

Props:

```ts
type SignalMarkerProps = {
  size?: 'micro' | 'small';
  decorative?: boolean;
};
```

Default visual size ~8px.

Do not let each screen create arbitrary red squares with one-off sizes.

## 10. `SystemRule`

Shared line primitive for strong and hairline separators.

```ts
type SystemRuleProps = {
  tone?: 'strong' | 'neutral';
  orientation?: 'horizontal' | 'vertical';
};
```

The shell's deck divider uses `strong` and is full-width.

## 11. `AiControlDeck`

Persistent lower Console 2 control region.

Contains:

- `AiArcadeButton` BACK
- `AiArcadeButton` NEXT
- `AiRotaryDial` INTENSITY DIAL

It must not render a centered MUSE wordmark.

Responsibilities:

- fixed geometry
- map semantic actions to visible physical controls
- display disabled states without removing hardware
- maintain identical geometry across screens

Static prototype controls are mouse/keyboard accessible.

Future physical hardware integration should dispatch the same semantic actions without redesigning the deck.

## 12. `AiArcadeButton`

This is not the Console 1 3D button.

Visual construction:

- circular off-white face
- thick black outer ring
- black inner ring
- optional subtle grey inner contour
- no glossy fill
- no red body
- no pixel shading

Suggested props:

```ts
type AiArcadeButtonProps = {
  label: 'BACK' | 'NEXT';
  enabled: boolean;
  onPress?: () => void;
  ariaLabel: string;
};
```

Disabled hardware stays visible but uses muted grey/black state.

## 13. `AiRotaryDial`

Distinct Console 2 rotary representation.

Visual construction:

- off-white circular face
- black outer ring
- grey inner contour
- red pointer/tick
- no gold
- no pixel-art extrusion

Suggested props:

```ts
type AiRotaryDialProps = {
  label?: string;
  value?: number;
  min?: number;
  max?: number;
  enabled: boolean;
  onChange?: (value: number) => void;
};
```

Default label:

```text
INTENSITY DIAL
```

For the static build, it may mirror/drive the currently focused tone control only when the interaction model has an active adjustable control. It must not create hidden product behavior outside the screen plan.

## 14. Regenerate action

`A2_03` still needs `regenerate`, but the current reference deck has only BACK/NEXT/dial hardware.

Therefore use `AiRegenerateAction` as a restrained software/system text action placed just above the deck or within the result content action row.

It must not be styled as a large button.

Do not invent a fourth hardware control.

## 15. `AiPromptField`

Responsibilities:

- controlled textarea
- 120-character max
- example/placeholder
- character count
- keyboard focus

Suggested props remain:

```ts
type AiPromptFieldProps = {
  value: string;
  onChange: (value: string) => void;
  maxLength: number;
  placeholder: string;
  ariaLabel: string;
};
```

Use refined black/grey/red focus language, not blue.

## 16. `AnalysisCard`

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

Use thin editorial rules and optional shared `SignalMarker`, not blue cards/icons.

## 17. `ToneControl`

Editable parameter component.

```ts
type ToneControlProps = {
  id: ToneControlId;
  label: string;
  value: number;
  min?: number;
  max?: number;
  step?: number;
  onChange: (value: number) => void;
};
```

Use native `<input type="range">` when possible. Fully style the track/thumb using refined monochrome/red tokens.

## 18. `ToneControls`

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

## 19. `ContextSignal`

Welcome screen can retain the restrained transferred-context signal from the original four-screen reference.

Update its visual language:

- monochrome neutral dots/lines
- tiny red center/marker instead of blue
- approximately 160–190px diameter
- no animation
- no glow
- no scientific labels

It remains a contextual acknowledgement, not a data visualization.

## 20. `AiLetterDocument`

Responsibilities:

- typed letter display
- optional layered outline sheets
- no editing
- no personal decoration in current phase

Props:

```ts
type AiLetterDocumentProps = {
  letter: string;
  recipientName?: string;
  variantIndex?: number;
};
```

Normalize generated content to safe plain paragraphs.

## 21. `LetterInsights`

Contains exactly four insight sections:

1. sentiment
2. emotion
3. romance
4. tone profile

All read-only.

Use black/grey typography with tiny red signal accents only where needed.

## 22. Screen responsibilities

### `AiWelcomeScreen`

Owns:

- personalized welcome copy
- inherited-context sentence
- `ContextSignal`
- optional system-status line/microcopy

Primary begin action is mapped to the deck `NEXT` button.

### `AiPromptScreen`

Owns:

- title
- subtitle
- prompt field

Navigation maps to deck:

- BACK -> previous
- NEXT -> continue when valid

### `AiInterpretationScreen`

Owns:

- screen title
- left read-only analysis column
- right tone-control column

Deck:

- BACK -> prompt
- NEXT -> result
- dial enabled for intensity/tone adjustment according to current focus/selection model

### `AiLetterResultScreen`

Owns:

- letter document
- insight rail
- `AiRegenerateAction`

Deck:

- BACK -> interpretation
- NEXT -> reflection
- dial may remain visible but neutral/inactive unless a later approved interaction uses it

## 23. State isolation

Components are deterministic from props/session state. Avoid local duplicate copies of global session values.

## 24. Error/empty state strategy

Do not design visible error banners now.

Development guards may render plain developer-only fallbacks outside canonical screenshot tests.

## 25. No motion architecture dependency

Do not install an animation library.
Do not wrap components in motion primitives.
Do not create timers solely for visual effects.

## 26. Component completion rule

A component is complete only when:

- it matches the current canonical references,
- it consumes shared Console 2 tokens,
- it has no Console 1 visual dependency,
- hardware/deck geometry remains stable,
- it is keyboard accessible where interactive,
- it passes screenshot regression in actual screen composition.