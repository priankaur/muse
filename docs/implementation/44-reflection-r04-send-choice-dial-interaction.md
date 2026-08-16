# 44 — MUSE Reflection Experience — Dial-Driven Letter Choice Interaction

**Status:** Detailed dial/pivot interaction reference. **Current screen numbering and merged-question authority are in file `46`.** The interaction previously lived on R_04; it now applies to **R_03 / 05**.

## Current role

The old separate questions:

```text
Which letter sounds more like you?
```

and:

```text
Which letter would you actually send?
```

are now merged into one binary letter choice.

Current question:

```text
Which letter feels most like you — and is the one you'd actually send?
```

Supporting line:

```text
Choose the one that feels closest to your voice and that you'd put your name behind.
```

Progress:

```text
REFLECTION 03 / 05
```

## Composition

At `1440 × 1080`:

```text
[ HUMAN + AI LETTER ]    [ CENTRAL QUESTION PIVOT CARD ]    [ AI ONLY LETTER ]
```

Both letters use identical dimensions, paper tint, typography, border treatment and prominence.

Recommended starting geometry:

```text
left letter:
  x: 125–155
  y: 245–285
  width: 420–460
  height: 500–540

center question card:
  center x: 720
  center y: 500–520
  width: 300–340
  height: 230–270

right letter:
  x: 825–855
  y: 245–285
  width: 420–460
  height: 500–540
```

Do not heavily overlap the pivot card over the letter text.

## Visual treatment

Letter paper:

```css
background: var(--reflection-letter-paper); /* ~#F1EEE8 */
border: 1px solid var(--reflection-line);
border-radius: 0–2px;
```

Pivot card:

- warm-white / barely separated neutral surface;
- 1px neutral or near-black border;
- 0–2px radius;
- no colored outline;
- no hearts/patterns;
- no playful styling from the interaction reference;
- centered question text.

Optional quiet helper:

```text
turn the dial to choose
press to confirm
```

## Candidate state

```ts
type SendChoiceCandidate = 'human-ai' | 'ai-only' | null;
```

Initial:

```text
candidate = null
rotation = 0deg
```

Turn left:

```text
candidate = 'human-ai'
rotation = -5deg to -7deg
translateX = -6px to -12px
```

Turn right:

```text
candidate = 'ai-only'
rotation = +5deg to +7deg
translateX = +6px to +12px
```

Do not accumulate unlimited rotation.

## Motion

Recommended:

```text
140–190ms
transform-origin: 50% 65%
cubic-bezier(0.22, 1, 0.36, 1)
```

No spring, bounce, wobble, continuous spinning, perspective flip, large tilt, or Arcade 1 stepped motion.

Respect `prefers-reduced-motion`.

## Candidate feedback

Candidate letter:

```text
2px #111111 border
```

Other letter:

```text
1px neutral border
```

Optional slight source-label weight increase.

Do not alter paper tint, add winner states, color-code, or heavily dim the other letter.

## Confirmation

Dial movement previews only.

Knob press / `DIAL_CONFIRM` commits the current candidate and advances to **R_04**.

```ts
if (sendChoiceCandidate === null) {
  // remain on R_03
}

if (sendChoiceCandidate) {
  reflection.sendChoice = sendChoiceCandidate;
  routeTo('R_04');
}
```

Do not require a second Continue click.

On this screen, do not show an active `CONTINUE →` that bypasses dial confirmation.

BACK routes to `R_02`.

## Fallback

Clicking either letter may set its candidate but must not auto-submit.

Enter/Space may dispatch `DIAL_CONFIRM`.

Do not change visible design for fallback behavior.

## State simplification

The old separate durable `reflection.voiceChoice` answer is superseded.

Current committed letter answer is only:

```ts
reflection.sendChoice: 'human-ai' | 'ai-only' | null;
```

The previous `Parts of both` / `Neither` standalone voice options are not part of current R_03.

## Tests

Verify:

- initial candidate null;
- left/right dial selection;
- pivot rotation direction;
- candidate border feedback;
- null confirm does not advance;
- Human + AI confirm stores `sendChoice = 'human-ai'` and routes to R_04;
- AI Only confirm stores `sendChoice = 'ai-only'` and routes to R_04;
- mouse fallback selects but does not auto-submit;
- reduced-motion preserves semantics;
- no separate `voiceChoice` answer is required.

## Latest authority

For complete five-screen routing/state/final exit behavior read:

```text
docs/implementation/46-reflection-five-screen-merged-letter-choice.md
```
