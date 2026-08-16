# 46 — MUSE Reflection Experience — Five-Screen Flow + Merged Letter Choice

**Status:** Latest product-flow authority for Reflection. This file supersedes the six-screen sequence in files `38`, `40`, `41`, `44`, and `45` wherever they conflict.

## Core change

Reflection is now exactly **five screens**.

The previous separate questions:

- `Which letter sounds more like you?`
- `Which letter would you actually send?`

are merged into **one binary letter-choice screen** using the approved dial-driven pivot-card interaction.

The final screen now confirms the visitor's future-writing choice and gives physical exit instructions using a **matching coin + bowl + postcard**.

## Canonical flow

```text
A2_03 NEXT
→ R_01 Read both letters
→ R_02 Analysis + experience-feeling tags
→ R_03 Which letter feels most like you — and is the one you'd actually send? (dial-driven)
→ R_04 Future authorship / agency choice
→ R_05 Confirm choice + matching coin + bowl + postcard exit
→ session complete
```

All Reflection progress labels must use:

```text
REFLECTION NN / 05
```

Do not use `/06` anywhere in the current Reflection implementation.

---

# R_01 — Read both letters

Unchanged responsibility.

Progress:

```text
REFLECTION 01 / 05
```

Heading:

```text
Read both letters side by side.
```

Supporting line:

```text
Take a moment with each one before comparing how they feel.
```

Show both final letters with equal visual weight.

No analysis, tags, selection, or source bias.

`CONTINUE → R_02`.

---

# R_02 — Analysis + experience-feeling tags

This is the currently approved normalized comparison/tag screen.

Progress:

```text
REFLECTION 02 / 05
```

Keep the approved composition and selected-tag treatment.

Heading:

```text
Two letters. Two ways of getting there.
```

Supporting line:

```text
Before choosing between them, look at what each one carries.
```

Comparison dimensions remain exactly:

1. emotional warmth
2. personal specificity
3. vocabulary complexity
4. affectionate language

Question:

```text
How did the two experiences feel?
```

Helper:

```text
choose up to 3
```

Allow `1–3` selected tags; no fourth selection.

Selected screenshot examples such as `personal`, `thoughtful`, and `too polished` are demonstration states only and must not be preselected by default.

`CONTINUE → R_03`.

---

# R_03 — Merged letter choice

## Purpose

Ask one combined question that captures both:

- which letter feels closest to the visitor's voice;
- which letter they would actually choose to send.

Do not ask these as separate screens anymore.

## Progress

```text
REFLECTION 03 / 05
```

## Approved merged question

Preferred headline / pivot-card copy:

```text
Which letter feels most like you — and is the one you'd actually send?
```

Supporting line:

```text
Choose the one that feels closest to your voice and that you'd put your name behind.
```

Keep copy configurable.

## Choice model

This is now a binary choice between the two completed letters:

```text
HUMAN + AI
AI ONLY
```

Remove the previous separate voice-choice options:

- Parts of both
- Neither

Those belonged to the superseded standalone voice question and no longer apply to the merged dial interaction.

## State

Use one durable committed letter choice:

```ts
reflection.sendChoice: 'human-ai' | 'ai-only' | null;
```

The old durable `reflection.voiceChoice` field is no longer required for the current product flow.

If it exists in the current code, migrate/remove it safely rather than keeping two contradictory answers.

A transient candidate may still be used before knob confirmation:

```ts
sendChoiceCandidate: 'human-ai' | 'ai-only' | null;
```

## Visual composition

Retain the approved dial/pivot interaction concept from file `44`, but apply it to `R_03`:

```text
[ HUMAN + AI LETTER ]    [ CENTRAL QUESTION PIVOT CARD ]    [ AI ONLY LETTER ]
```

Both letter cards remain identical in:

- size
- paper tint
- border
- typography
- elevation
- horizontal prominence

No source-specific color coding.

The center card is smaller and uses the merged question.

## Dial behavior

Initial:

```text
candidate = null
pivotRotation = 0deg
```

Turn left:

```text
candidate = 'human-ai'
pivot ≈ -5deg to -7deg
translateX ≈ -6px to -12px
```

Turn right:

```text
candidate = 'ai-only'
pivot ≈ +5deg to +7deg
translateX ≈ +6px to +12px
```

Candidate letter:

```text
2px near-black border
```

Other letter:

```text
1px neutral border
```

Do not change paper tint or add winner styling.

## Knob confirmation

Dial movement previews only.

Knob press / `DIAL_CONFIRM` commits the selected letter and advances directly to `R_04`.

```ts
if (candidate === null) {
  // remain on R_03
}

if (candidate) {
  reflection.sendChoice = candidate;
  routeTo('R_04');
}
```

Do not require an additional visible Continue click.

Do not show an active `CONTINUE →` that bypasses the dial interaction.

BACK routes to `R_02`.

Mouse/touch fallback may set the candidate; Enter/Space may dispatch the same confirm action. Fallback interaction must not alter the visible Reflection design.

## Motion

Keep the approved subtle editorial motion:

- `140–190ms`;
- transform origin around `50% 65%`;
- no bounce, spring, wobble, arcade stepping, large rotation, or continuous spin;
- respect `prefers-reduced-motion`.

---

# R_04 — Future authorship / agency choice

Progress:

```text
REFLECTION 04 / 05
```

Question:

```text
Next time you want to say something that matters,
how would you rather write it?
```

Use exactly three equal Reflection choice cards.

## Choice A

```text
I write first. AI helps refine.
```

```text
Start with my own words, then use AI to improve or clarify them.
```

State:

```text
human-led-ai-refine
```

## Choice B

```text
AI drafts first. I choose what stays.
```

```text
Begin with an AI-written draft, then edit or keep what feels right.
```

State:

```text
ai-led-draft
```

## Choice C

```text
I write without AI.
```

```text
Keep meaningful writing entirely in my own words.
```

State:

```text
human-only
```

All three choices remain visually equal and neutral.

Store:

```ts
reflection.futureApproach =
  | 'human-led-ai-refine'
  | 'ai-led-draft'
  | 'human-only'
  | null;
```

No default selection.

`CONTINUE → R_05` once one choice is selected.

---

# R_05 — Choice confirmation + coin + bowl + postcard exit

## Purpose

The last digital screen should first **tell the visitor what future-writing approach they chose**, then translate that same choice into the physical exit ritual.

Progress:

```text
REFLECTION 05 / 05
```

## Dynamic confirmation

Show the selected `reflection.futureApproach` prominently.

Recommended heading pattern:

```text
You chose:
[SELECTED APPROACH LABEL]
```

Where the visible selected label is exactly one of:

```text
I write first. AI helps refine.
AI drafts first. I choose what stays.
I write without AI.
```

Optional supporting line:

```text
Carry that choice into the final step.
```

Do not congratulate, score, or moralize the selection.

## Physical coin mapping

Map the selected future approach one-to-one to a physical coin label:

```text
human-led-ai-refine -> HUMAN FIRST + AI REFINE
ai-led-draft       -> AI DRAFTS FIRST
human-only         -> HUMAN ONLY
```

## Exit instructions

Use `coin`, not `token`.
Use `bowl`, not `box`.

Preferred instruction sequence:

```text
01  Pick up the coin that matches your choice.
02  Drop that coin into the bowl.
03  Collect your printed postcard on the way out.
```

A slightly more direct dynamic version is also valid:

```text
Pick up the [MATCHING COIN LABEL] coin.
Drop it into the bowl.
Collect your printed postcard on the way out.
```

Keep the screen visually quiet and poster-like.

## Postcard

The postcard is based on the letter committed on `R_03` via:

```ts
reflection.sendChoice
```

Use the current printer stub only.

No real printer dependency yet.

The final screen may show a very small neutral status such as:

```text
POSTCARD READY
```

only if the printer stub/state supports it.

Do not add:

- confetti
- winner language
- score
- recommendation
- extra survey question
- console chrome

Entering/completing R_05 may mark:

```ts
reflection.completed = true
session.completed = true
```

---

# Current Reflection state contract

Preferred current state:

```ts
type ReflectionState = {
  experienceTags: string[];

  sendChoice:
    | 'human-ai'
    | 'ai-only'
    | null;

  futureApproach:
    | 'human-led-ai-refine'
    | 'ai-led-draft'
    | 'human-only'
    | null;

  completed: boolean;
};
```

`voiceChoice` is superseded by the merged R_03 question and should not remain as a separate required product answer.

---

# Route map

```text
A2_03 NEXT -> R_01
R_01 CONTINUE -> R_02
R_02 CONTINUE -> R_03
R_03 DIAL_CONFIRM -> R_04
R_04 CONTINUE -> R_05
R_05 -> physical exit / session complete
```

Back routes:

```text
R_02 BACK -> R_01
R_03 BACK -> R_02
R_04 BACK -> R_03
```

R_01 BACK remains product-guarded.

---

# Migration requirements

Codex must audit and remove old six-screen assumptions safely.

Specifically search for and update:

- `/06` progress labels;
- `R_06` route/component references;
- old standalone `R_03` voice-choice route;
- old `R_04` send-choice route numbering;
- `voiceChoice` required state/tests;
- `Parts of both` / `Neither` voice options;
- old `R_05` agency numbering;
- old `R_06` exit numbering;
- `token` wording;
- `box` wording;
- printer payload assumptions tied to old route numbering.

Do not delete reusable visual components merely because screen numbering changes.

The dial-driven pivot-card component should migrate from old R_04 to current R_03.

---

# Required visual regressions

Capture stage-only `1440 × 1080` screenshots for:

- R_01 read-both-letters;
- R_02 zero tags;
- R_02 one tag;
- R_02 three tags;
- R_03 neutral candidate;
- R_03 Human + AI candidate;
- R_03 AI Only candidate;
- R_04 no future approach selected;
- R_04 one future approach selected;
- R_05 confirmation/exit for each of the three future approaches if fixture coverage permits.

Also verify Console 1 and Console 2 do not visually regress.

---

# Non-negotiable emotional sequence

```text
READ
→ COMPARE + REFLECT
→ CHOOSE THE LETTER THAT FEELS LIKE ME AND I WOULD SEND
→ CHOOSE HOW I WANT TO WRITE NEXT TIME
→ SEE MY CHOICE + MAKE IT PHYSICAL
```

This five-step sequence is now canonical.
