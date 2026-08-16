# 40 — MUSE Reflection Experience — Screen Specifications

**Status:** Current screen authority for the five-screen reflection flow.

Read together with:

- `38-reflection-source-of-truth.md`
- `39-reflection-visual-system.md`

All screens render in the shared fixed `1440 × 1080` stage but use `ReflectionShell`, not either console shell.

---

# Shared shell

## Stage

```text
1440 × 1080
```

Background:

```text
#FAF9F6
```

No console hardware deck.
No console identity lockup.
No pixel window.
No system status chrome.

## Shared top area

Small progress text:

```text
REFLECTION 01 / 05
```

Recommended anchor:

```text
x: 72
y: 58
```

Use muted grey, small tracked grotesk.

## Shared navigation

Bottom-left:

```text
← BACK
```

Bottom-right:

```text
CONTINUE →
```

Use neutral text controls.

Do not render on-screen arcade buttons or dial graphics.

---

# R_01 — Side-by-side analysis + experience tags

## Purpose

Let the visitor see how the two final letters differ, then reflect on the experience itself.

## Heading

Preferred:

```text
Two letters. Two ways of getting there.
```

Supporting line:

```text
Before choosing between them, look at what each one carries.
```

Then show a shared comparison table.

## Analysis comparison

Use one normalized shared schema for both letters:

1. emotional warmth
2. personal specificity
3. vocabulary complexity
4. affectionate language

Recommended table width:

```text
980–1080px
```

Recommended centered placement:

```text
x: 180–230
y: 260–500
```

Column structure:

```text
METRIC | LETTER A | LETTER B
```

Labels above columns:

```text
LETTER A
HUMAN + AI
```

```text
LETTER B
AI ONLY
```

Use text descriptors and optional thin monochrome readouts.

Do not visually mark a winner.

## Experience question

Place below comparison:

```text
How did the two experiences feel?
```

Use multi-select tags.

Recommended tags:

- personal
- easy
- surprising
- thoughtful
- too polished
- distant
- expressive
- awkward
- familiar
- made me think

Allow max 3 selections initially.

CONTINUE enabled after at least one tag is selected.

Store in `reflection.experienceTags`.

---

# R_02 — Which letter sounds like you?

## Heading

```text
Which letter sounds more like you?
```

Supporting line:

```text
Not which one is better — which one feels closer to your voice.
```

## Two-letter layout

Display both complete letter documents using the reusable `ReflectionLetterCard`.

Recommended:

```text
container x: 150–170
container y: 220–760
letter width: 520px
letter height: 500px
column gap: 70–80px
```

Both surfaces use identical subtle paper tint.

Do not use source-specific background colors.

## Choice controls

Selection may happen directly by clicking the letter card.

Also provide small neutral options beneath if needed:

- parts of both
- neither

No default selection.

CONTINUE enabled after selection.

Store `reflection.voiceChoice` separately.

---

# R_03 — Which letter would you send?

## Heading

```text
Which letter would you actually send?
```

Supporting line:

```text
Choose the one you would put your name behind.
```

Reuse the exact same two-letter geometry from R_02.

Do not reorder the letters between screens.

Do not automatically select the letter chosen in R_02.

Selection should be independent.

Primary options:

- Human + AI
- AI Only

Optional `neither` only if approved in content config.

Store in `reflection.sendChoice`.

CONTINUE enabled after choice.

---

# R_04 — Future authorship stance

## Heading

Preferred:

```text
Next time you want to say something that matters,
how would you rather write it?
```

Use three equal-width choice cards.

## Choice A

Label:

```text
I write first. AI helps refine.
```

Explanation:

```text
Start with my own words, then use AI to improve or clarify them.
```

State:

```text
human-led-ai-refine
```

## Choice B

Label:

```text
AI drafts first. I choose what stays.
```

Explanation:

```text
Begin with an AI-written draft, then edit or keep what feels right.
```

State:

```text
ai-led-draft
```

## Choice C

Label:

```text
I write without AI.
```

Explanation:

```text
Keep meaningful writing entirely in my own words.
```

State:

```text
human-only
```

All cards are visually equal.

No recommendation.
No preferred default.
No different icon/color per card.

CONTINUE enabled after one is selected.

---

# R_05 — Token + postcard exit

## Heading

Preferred:

```text
One last choice — make it physical.
```

Alternative approved tone if needed:

```text
Take your choice with you.
```

## Instruction stack

Use three large but restrained numbered lines:

```text
01  Pick up the token that matches your choice.
02  Drop it into the corresponding box.
03  Collect your printed postcard on the way out.
```

Do not add more survey questions.

Optional small confirmation:

```text
POSTCARD READY
```

if printer service has been invoked/stubbed successfully.

## Physical mapping

Future stance → physical label:

```text
human-led-ai-refine -> HUMAN FIRST + AI REFINE
ai-led-draft       -> AI DRAFTS FIRST
human-only         -> HUMAN ONLY
```

## Print payload

Prepare the letter selected in `reflection.sendChoice`.

Recommended payload:

```ts
{
  selectedLetterType,
  selectedLetterText,
  visitorName,
  recipientName,
  futureApproach,
  timestamp
}
```

Current static implementation may call a printer stub only.

No real printer dependency required yet.

## Completion

Entering/confirming this state may mark:

```ts
reflection.completed = true
session.completed = true
```

Do not route back into either console visual shell after completion.

---

# Cross-screen invariants

- same `ReflectionShell` across all five screens;
- no Arcade 1 visual chrome;
- no Arcade 2 visual chrome;
- same background across all reflection screens;
- same letter paper tint for both letters;
- same Letter A / Letter B ordering across R_01–R_03;
- voice choice and send choice stored independently;
- all philosophical options have equal visual weight;
- no winner, score or recommendation language;
- no color-coded morality;
- progress is sequence-only, never points.

# Reflection transition map

```text
A2_03 NEXT
  -> R_01

R_01 CONTINUE
  -> R_02

R_02 CONTINUE
  -> R_03

R_03 CONTINUE
  -> R_04

R_04 CONTINUE
  -> R_05

R_05
  -> physical exit/session complete
```

Back routes:

```text
R_02 BACK -> R_01
R_03 BACK -> R_02
R_04 BACK -> R_03
```

R_01 BACK behavior should be guarded/product-reviewed because returning into A2_03 may be undesirable once reflection begins. Default prototype may allow it for testing, but do not expose unless explicitly approved.
