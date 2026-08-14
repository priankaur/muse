# 06 — Navigation and Input Model

## Purpose

The final installation uses physical arcade controls, but the first build uses keyboard/mouse simulation. The UI must not be coupled to either input source.

## Interaction abstraction

Screen components should consume semantic actions:

```ts
type MuseAction =
  | { type: 'NEXT' }
  | { type: 'BACK' }
  | { type: 'CONFIRM' }
  | { type: 'MOVE_PREV' }
  | { type: 'MOVE_NEXT' }
  | { type: 'ADJUST'; delta: -1 | 1 }
  | { type: 'TEXT_COMMIT' };
```

The physical adapter and keyboard adapter both emit these actions later.

## Temporary development keyboard mapping

Recommended:

- `ArrowLeft` → previous/focus previous/back depending on screen contract.
- `ArrowRight` → next/focus next.
- `ArrowUp` / `ArrowDown` → adjust dial value or move among option rows.
- `Enter` → confirm / commit.
- `Escape` → development back/reset only when debug mode is on.
- normal typing → active text field.

The exact production mapping can change when hardware is connected; components should not contain key codes.

## Mouse support

Mouse/touch clicks can be enabled for development and testing even though the final physical interaction is arcade-led.

Do not visually redesign controls to look like web buttons just because they are clickable.

## Focus model

The app maintains one logical focused control at a time.

For each screen define an ordered focus list:

```ts
['recipientName', 'relationship.partner', ..., 'relationship.otherText', 'continue']
```

The visual focus state should be explicit and visible from standing distance.

## Text entry mode

When a text field is active:

- normal typing affects the field,
- hardware/dial movement should later be ignored or mapped according to the final keyboard/hardware design,
- Enter commits the field and returns to screen navigation.

The legacy experience used this rule and it remains a good interaction contract.

## Back navigation

Do not assume every screen supports back.

The screen registry should include:

```ts
canGoBack: boolean
```

Examples:

- welcome/recipient screens can generally go back,
- a final capture after the third photo may block retake/back,
- generating/result transition states may be forward-only in production.

For the static prototype, keep deterministic rules documented per screen.

## Screen state machine

Avoid ad-hoc `setScreen(screen + 1)` logic.

The state machine decides next screen based on:

- current screen ID,
- required session state,
- selections,
- attempt count,
- console phase.

This is important for the `Other` relationship field and camera retry branch.

## Console transition

Arcade 2 begins with the existing session. It must not clear recipient or visitor data.

For development, `A2_00` deep-link should seed representative Arcade 1 fixture state automatically.

## Reset

Provide a development-only and operator-safe reset action that restores the session to a known initial fixture/default state.

Production auto-reset timing is deferred until exhibition operation is defined.
