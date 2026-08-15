# 28 — Arcade Console 1 / Human + AI — Motion, Click Feedback and Sound

This file activates motion and sound for **Arcade Console 1 only**. It supersedes the earlier blanket statement that animation/sound are deferred, but only for the specific interactions defined here.

Console 2 remains static unless its own plan explicitly changes later.

## 1. Core principle

Motion and sound must make Arcade 1 feel tactile and arcade-like **without changing the locked visual design**.

The approved shell, colors, window geometry, sprites, CTA design and hardware visuals remain unchanged.

Motion should feel:

- stepped;
- tactile;
- quick;
- low-frame / pixel-like;
- mechanical enough to feel arcade-native;
- playful but not noisy.

It must NOT feel like:

- modern app spring physics;
- smooth luxury-product easing;
- glass UI;
- long cinematic transitions;
- constant decorative motion;
- motion for every hover.

## 2. Technology constraints

Use CSS transitions/keyframes plus a small event-driven interaction layer.

Do not add Framer Motion or another animation framework.

Recommended architecture:

```text
ArcadeOneMotionProvider / motion utilities
ArcadeOneAudioManager
semantic interaction events
shared pressed/transition state helpers
```

Do not trigger audio or animation from arbitrary component re-renders.

## 3. Semantic interaction events

Define explicit events such as:

```ts
type ArcadeOneFeedbackEvent =
  | 'CTA_PRESS'
  | 'ARCADE_BUTTON_PRESS'
  | 'DIAL_TICK'
  | 'DIAL_CONFIRM'
  | 'PAGE_TRANSITION_OUT'
  | 'PAGE_TRANSITION_IN'
  | 'TEXT_COMMIT'
  | 'CAPTURE'
  | 'PROCESS_START'
  | 'RESULT_REVEAL';
```

The visual and audio feedback systems subscribe to semantic events rather than page-specific DOM selectors.

## 4. CTA press animation

Applies to magenta primary CTAs.

Interaction sequence:

1. pointer/keyboard activation begins;
2. button face visually compresses/depresses;
3. CTA sound plays once;
4. activation is committed;
5. button returns or page transition begins.

Starting timing:

```text
press-down: 70–90ms
hold/confirmation: 20–40ms
release: 80–100ms
```

Visual behavior:

- translate face down by approximately 3–4px in the 1440×1080 coordinate system;
- reduce visible stepped lower bevel/extrusion during press;
- optional 1–2% scale reduction maximum;
- no blur;
- no glow;
- no smooth elastic bounce;
- use `steps()` or very short linear timing where appropriate.

Keyboard Enter/Space must trigger the same pressed state as pointer interaction.

## 5. Red arcade button press animation

Applies to the persistent red 3D arcade buttons.

Visual behavior:

- top cap moves downward approximately 3px;
- lower dark ring appears compressed;
- tiny highlight shifts/reduces;
- full component does not slide around the footer;
- release returns to canonical asset geometry.

Timing:

```text
press: 60–80ms
release: 80–100ms
```

The button must remain recognizable as the same approved component.

Do not replace the current art with generic CSS circles.

## 6. Gold dial animation

The gold center control is a rotary encoder/dial, not a slider.

Use discrete visual increments.

Recommended:

```text
one logical detent = 10–15 degrees visual rotation
```

Each increment/decrement:

- rotates the top/pointer state by one discrete step;
- emits one dial tick sound;
- updates the active value once;
- uses no inertial spin;
- does not continuously rotate while idle.

Starting animation duration per detent:

```text
45–70ms
```

Pressing the dial, where confirm/select is supported, may use a 2px vertical depression plus `DIAL_CONFIRM` sound.

## 7. Page/screen change animation

The outer Arcade 1 world and persistent hardware strip should feel stable. The main change happens in the **content/window interior**, not by moving the entire composition offscreen.

Recommended transition:

### Outgoing

- content snaps/dims out in 2–4 stepped frames;
- optional 1–2px horizontal pixel offset/glitch step;
- duration approximately 90–120ms.

### Incoming

- new content appears in 3–5 stepped frames;
- duration approximately 120–160ms;
- no long fade.

Total transition target:

```text
180–260ms maximum
```

Do not animate the sharp window frame itself on every screen change.

Do not animate top-left branding or console label on every transition.

The window chrome and hardware strip remain spatially stable.

## 8. Processing/result reveal

`A1_09` can now use a restrained pixel-processing animation instead of a fully static state.

Allowed:

- discrete progress blocks;
- stepped meter increments;
- short terminal/pixel text updates;
- 2–5 deterministic progress stages.

Avoid fake long waiting. For the prototype, total deterministic processing duration should usually remain under ~1.5 seconds unless exhibition pacing later requires more.

`A1_10` result reveal may use a short stepped reveal (150–250ms), not a dramatic cinematic animation.

## 9. Decorative sprite motion

The earlier planned gentle floating stationery motion is now allowed for Arcade 1 after core interaction feedback is implemented.

Rules:

- only existing approved sprites move;
- no new decorative sprites;
- gentle vertical bob 3–8px;
- stepped or low-frame cadence;
- varied periods so everything does not move in sync;
- no rotation storms;
- no motion behind dense text fields if it harms focus.

This is lower priority than CTA/button/dial/page feedback.

## 10. Audio architecture

Create one `ArcadeOneAudioManager` or equivalent semantic audio service.

Requirements:

- audio unlock happens only after the first valid user gesture;
- no autoplay errors;
- no audio triggered during render;
- support global mute and volume setting in code/config;
- prevent accidental duplicate playback from pointer + semantic action firing twice;
- allow future replacement of generated placeholder sounds with production WAV/OGG assets without changing screen components.

## 11. Sound palette

Use short, dry, arcade/system sounds.

Recommended semantic cues:

### CTA_PRESS

- short confirm chirp;
- approximately 70–120ms;
- mid/high frequency;
- one clean hit, no melody.

### ARCADE_BUTTON_PRESS

- lower tactile click/clack;
- approximately 50–100ms.

### DIAL_TICK

- tiny dry tick;
- approximately 20–50ms;
- should tolerate repeated detents without becoming harsh.

### DIAL_CONFIRM

- slightly stronger click than dial tick.

### PAGE_TRANSITION_OUT / IN

Use one restrained paired cue or one compact transition blip.
Do not play two loud sounds for every page.

### PROCESS_START

- short computational/pixel sequence;
- restrained volume.

### RESULT_REVEAL

- concise completion cue;
- avoid celebratory fanfare.

## 12. Sound implementation strategy

For the first implementation, either:

1. use tiny local audio assets stored under `public/assets/audio/arcade1/`, or
2. generate simple placeholder tones through Web Audio API behind the semantic `AudioManager` interface.

Preferred for robustness during development: Web Audio or locally generated tiny WAV files with **no runtime network dependency**.

Do not fetch sounds from external URLs.

Production sound assets can replace placeholders later.

## 13. Volume discipline

The installation may have two physical consoles nearby, so Arcade 1 audio must not be loud or continuous.

Starting relative volumes:

```text
CTA confirm:      0.35
arcade button:    0.32
dial tick:        0.18
page transition:  0.22
processing:       0.20
result reveal:    0.28
```

Treat these as normalized defaults, not final venue calibration.

No background music in this task.

## 14. Reduced-motion and accessibility

Respect `prefers-reduced-motion: reduce`.

Reduced mode:

- remove sprite bobbing;
- remove stepped page movement;
- keep a near-instant opacity/state swap;
- retain essential pressed-state feedback at minimal displacement.

Sound is independent from reduced motion.

Interactive elements must remain usable with keyboard.

## 15. Transition locking / double activation

During the short page transition:

- prevent duplicate route commits;
- ignore repeated confirm presses until transition completes;
- do not permanently disable controls if a transition is interrupted.

Use a small transition state such as:

```ts
'isIdle' | 'exiting' | 'entering'
```

Do not scatter `setTimeout` calls independently across screens.

## 16. Testing

Add tests for:

- CTA pressed class/state on pointer and keyboard;
- arcade button pressed state;
- one dial tick updates one discrete value;
- one semantic action triggers one sound event;
- page transition commits route exactly once;
- reduced-motion branch disables nonessential motion;
- visual screenshot after transitions settles remains identical to approved static baseline.

Visual regression screenshots should be captured **after animation settles**.

## 17. Non-negotiable anti-drift rules

Motion/sound work must not:

- change locked component geometry;
- change colors;
- add labels beneath hardware;
- round the main window;
- animate the whole window around the stage;
- introduce modern spring/ease-out-bounce behavior;
- introduce background music;
- alter Console 2.

## 18. Implementation order

Implement in this order:

1. semantic feedback event layer;
2. CTA press animation;
3. red arcade button press animation;
4. dial discrete rotation/tick;
5. page transition state;
6. sound manager + placeholder cues;
7. processing/result reveal;
8. optional sprite bobbing last.

Stop for visual/audio review after steps 1–6 before adding decorative motion.