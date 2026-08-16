# 44 — MUSE Reflection Experience — R_04 Dial-Driven Send Choice

**Status:** Latest interaction and visual authority for the Reflection screen asking which letter the visitor would actually send.

This screen is now `R_04` in the six-screen Reflection flow.

Read together with:

- `39-reflection-visual-system.md`
- `42-reflection-foundation-visual-calibration.md`
- `40-reflection-screen-specifications.md`

Where this file conflicts with older `R_03` send-choice behavior in file `40`, **this file wins**.

## Intent

Use the physical rotary dial as the primary selection mechanism while keeping the Reflection interface visually minimal and modern.

The interaction is inspired by the provided reference where a central card visually leans toward the left or right option, but the Reflection screen must NOT inherit that reference's bright colors, hearts, decorative graphics, playful framing, or website chrome.

Reflection remains a calm editorial/gallery experience.

## Screen role

Prompt:

```text
Which letter would you actually send?
```

Supporting line:

```text
Choose the one you would put your name behind.
```

This is an independent decision from `voiceChoice` on the previous screen.

Do not carry the previous voice selection into this screen as a default.

## Composition

At `1440 × 1080`, use a three-object horizontal composition in the main field:

```text
[ HUMAN + AI LETTER ]    [ CENTRAL QUESTION CARD ]    [ AI ONLY LETTER ]
```

The two letters remain the primary choice objects.

The central question card is the interactive selector/needle metaphor.

### Left letter

Label:

```text
LETTER A
HUMAN + AI
```

### Right letter

Label:

```text
LETTER B
AI ONLY
```

Both letter cards must use:

- identical dimensions;
- identical paper tint;
- identical typography;
- identical border treatment;
- identical elevation;
- equal horizontal distance from center.

No color coding by source.

## Recommended geometry

Starting values at 1440×1080:

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

Keep enough visual separation so the center card is clearly distinct but still spatially relates to both letters.

Do not overlap the center card heavily over the letter text.

## Letter appearance

Use the approved Reflection letter treatment:

```css
background: var(--reflection-letter-paper); /* ~#F1EEE8 */
border: 1px solid var(--reflection-line);
border-radius: 0–2px;
box-shadow: none or extremely restrained neutral shadow;
```

The same paper tint is mandatory for both choices.

Letter text should remain readable but may use controlled clipping if necessary for the canonical composition. Prefer enough card height to show the complete fixture.

## Central question card

Create a dedicated component, e.g.:

```text
ReflectionChoicePivotCard
```

It is visually simpler than the two letter documents.

Recommended treatment:

- background: `#FAF9F6` or a barely separated warm neutral such as `#F6F4EF`;
- 1px near-black or neutral border;
- 0–2px radius;
- no colored outline;
- no decorative hearts;
- no shadow spectacle;
- centered text;
- enough whitespace around the question.

Card copy:

```text
Which letter would you actually send?
```

Optional small supporting line inside/below card:

```text
turn the dial to choose
press to confirm
```

If included, keep this instruction extremely quiet:

- 12–14px;
- muted grey;
- no icon;
- no button illustration.

The instruction may also live just beneath the pivot card rather than inside it.

## Dial interaction model

Use the existing shared semantic rotary input abstraction.

Do NOT render a physical dial graphic on the Reflection screen.

The real/keyboard-emulated dial controls `sendChoiceCandidate`.

State:

```ts
type SendChoiceCandidate = 'human-ai' | 'ai-only' | null;
```

Initial state:

```text
sendChoiceCandidate = null
pivotRotation = 0deg
```

### Turn left

One or more left detents set:

```text
sendChoiceCandidate = 'human-ai'
```

Visual response:

```text
center card rotation: -5deg to -7deg
center card x shift: -6px to -12px maximum
```

The motion should read as the question card leaning toward Letter A.

### Turn right

One or more right detents set:

```text
sendChoiceCandidate = 'ai-only'
```

Visual response:

```text
center card rotation: +5deg to +7deg
center card x shift: +6px to +12px maximum
```

The motion should read as the question card leaning toward Letter B.

### Neutral

If the interaction abstraction supports returning to neutral before submission:

```text
sendChoiceCandidate = null
rotation = 0deg
```

However, a dedicated neutral detent is not required. A left/right two-choice model is acceptable.

## Motion character

The pivot motion must stay subtle and editorial.

Recommended:

```text
transition duration: 140–190ms
transform-origin: 50% 65%
```

Use a simple restrained ease such as:

```css
cubic-bezier(0.22, 1, 0.36, 1)
```

Do not use:

- spring bounce;
- elastic overshoot;
- continuous spinning;
- large 15–30° tilts;
- perspective flips;
- arcade/pixel stepped motion;
- wobbling idle animation.

This is the one Reflection interaction allowed to have a clearly perceptible rotational gesture because the physical dial meaningfully maps to it.

Respect `prefers-reduced-motion`:

- selection must still work;
- reduce rotation/translation or make state update nearly instant.

## Selected-letter feedback

The center-card lean alone is not sufficient for accessibility.

Also give the candidate letter a restrained selected state.

Preferred:

```text
selected letter border: 2px #111111
unselected letter border: 1px neutral grey
```

Optional secondary cue:

- slightly stronger source label weight; or
- one small black circular/square selection marker in the label area.

Do not:

- change paper color;
- scale the chosen letter dramatically;
- dim the unchosen letter below readable contrast;
- add green checks;
- use red/blue accents;
- label it `winner` or `recommended`.

## Knob press / submission

Dial rotation only previews the candidate.

The choice is committed ONLY when the rotary knob is pressed.

Semantic action:

```text
DIAL_CONFIRM
```

Rules:

```ts
if (sendChoiceCandidate === null) {
  // ignore confirm / do not advance
}

if (sendChoiceCandidate) {
  reflection.sendChoice = sendChoiceCandidate;
  route -> R_05;
}
```

The press must both:

1. store the selected letter;
2. submit/advance to the next reflection screen.

Do not require a second on-screen CONTINUE click after knob confirmation.

## Navigation chrome on R_04

Keep the shared Reflection bottom navigation anchors for consistency.

BACK remains available and routes to `R_03`.

For the primary forward action, the physical knob press is the intended interaction.

Recommended visible treatment:

- either hide/disable `CONTINUE →` on this specific screen while using dial confirmation;
- or keep a muted helper `PRESS KNOB TO CONFIRM` near the center selector instead.

Do NOT present a simultaneously active `CONTINUE →` that bypasses the dial interaction unless required for accessibility/testing fallback.

If keyboard accessibility is needed, map Enter/Space to the same `DIAL_CONFIRM` semantic action and expose an accessible button target without changing the visible design.

## Mouse/touch fallback

For development/accessibility, the letter cards may be clickable.

Clicking Letter A should set:

```text
sendChoiceCandidate = 'human-ai'
```

Clicking Letter B should set:

```text
sendChoiceCandidate = 'ai-only'
```

But clicking a letter should NOT immediately advance.

The user still confirms with the same semantic confirm action.

## State separation

Keep:

```text
reflection.voiceChoice
```

and:

```text
reflection.sendChoice
```

separate.

Add transient state if useful:

```text
reflection.sendChoiceCandidate
```

or keep candidate state local to R_04 until confirmation.

Do not preselect from `voiceChoice`.

## Progress

This screen is now:

```text
REFLECTION 04 / 06
```

The current six-screen order is:

```text
R_01 read both letters
R_02 analysis + feeling tags
R_03 which sounds like you
R_04 which would you send
R_05 future authorship/agency choice
R_06 token + postcard exit
```

## Tests

Add tests for:

- initial candidate is null;
- left dial detent selects Human + AI candidate;
- right dial detent selects AI Only candidate;
- pivot card rotates left/right accordingly;
- candidate border feedback follows the selected side;
- dial confirm with null does not advance;
- dial confirm with Human + AI stores `reflection.sendChoice = 'human-ai'` and routes to R_05;
- dial confirm with AI Only stores `reflection.sendChoice = 'ai-only'` and routes to R_05;
- mouse fallback sets candidate but does not auto-submit;
- `voiceChoice` does not preselect `sendChoiceCandidate`;
- reduced-motion mode preserves selection semantics;
- R_01–R_03 visual regressions remain unchanged.

## Visual acceptance

At 1440×1080 the screen should read as:

```text
quiet Reflection shell

[full letter]     [small question card]     [full letter]
                        ↙ / ↘
                   dial chooses side

BACK
```

The interaction should feel physical and memorable without making Reflection look like a game.

## Stop gate

Implement `R_04` only after `R_01–R_03` are stable.

Capture:

1. neutral/no-candidate state;
2. Human + AI candidate state;
3. AI Only candidate state.

Also verify knob confirmation routing.

STOP for visual review before implementing/finalizing R_05.
