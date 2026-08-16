# 40 — MUSE Reflection Experience — Screen Specifications

**Status:** Current five-screen screen-spec authority. Read with files `38`, `39`, `41`, and latest overrides `42`–`46`. **File `46` wins for the merged R_03 flow.**

All screens use the shared fixed `1440 × 1080` stage and `ReflectionShell`.

## Shared shell

Background:

```text
#FAF9F6
```

Progress:

```text
REFLECTION NN / 05
```

Top-left anchor approximately `x:72`, `y:58–64`.

Bottom-left where applicable:

```text
← BACK
```

Bottom-right where applicable:

```text
CONTINUE →
```

No console chrome, visible hardware deck, MUSE console identity, pixel UI, or persistent system accent.

---

# R_01 — Read both letters

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

Show two equal `ReflectionLetterCard`s:

```text
LETTER A
HUMAN + AI
```

```text
LETTER B
AI ONLY
```

Both use identical dimensions, tint, border, typography and prominence.

No analysis, tags or selection.

`CONTINUE → R_02`.

---

# R_02 — Normalized analysis + experience tags

Progress:

```text
REFLECTION 02 / 05
```

Heading:

```text
Two letters. Two ways of getting there.
```

Supporting line:

```text
Before choosing between them, look at what each one carries.
```

Use one normalized comparison model with exactly:

1. emotional warmth
2. personal specificity
3. vocabulary complexity
4. affectionate language

Do not render the console-specific analysis UIs side by side.

Question:

```text
How did the two experiences feel?
```

Helper:

```text
choose up to 3
```

Current tags:

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

Allow `1–3` selected tags.

Selected = near-black fill + warm-white text.

The latest screenshot showing `personal`, `thoughtful`, and `too polished` selected is a visual-state example only. Initial state remains zero selected.

`CONTINUE → R_03` after at least one valid selection.

---

# R_03 — Merged letter choice, dial-driven

**Latest detailed authority:** file `46`. File `44` remains the detailed pivot/dial interaction reference but its old R_04 numbering is superseded.

Progress:

```text
REFLECTION 03 / 05
```

Merged question:

```text
Which letter feels most like you — and is the one you'd actually send?
```

Supporting line:

```text
Choose the one that feels closest to your voice and that you'd put your name behind.
```

Use the three-object composition:

```text
[ HUMAN + AI LETTER ]    [ CENTRAL QUESTION PIVOT CARD ]    [ AI ONLY LETTER ]
```

Letters remain identical in size, paper tint, border, typography and visual weight.

This is a binary choice only:

```text
human-ai
ai-only
```

No separate `Parts of both` or `Neither` controls on the current merged screen.

Transient candidate:

```ts
sendChoiceCandidate: 'human-ai' | 'ai-only' | null;
```

Initial:

```text
candidate = null
pivot = 0deg
```

Dial left:

```text
candidate = human-ai
pivot ≈ -5deg to -7deg
translateX ≈ -6px to -12px
```

Dial right:

```text
candidate = ai-only
pivot ≈ +5deg to +7deg
translateX ≈ +6px to +12px
```

Candidate letter gets a restrained `2px` near-black border; other letter remains `1px` neutral.

Knob press / `DIAL_CONFIRM` commits:

```ts
reflection.sendChoice = sendChoiceCandidate;
```

and advances directly to `R_04`.

If candidate is null, confirm does not advance.

Do not show an active Continue action that bypasses dial confirmation.

BACK routes to `R_02`.

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

Use exactly three equal `ReflectionChoiceCard`s.

## A

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

## B

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

## C

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

All three have identical dimensions/hierarchy and neutral selection treatment.

No default, recommendation, or privileged styling.

Store in `reflection.futureApproach`.

`CONTINUE → R_05` after selection.

---

# R_05 — Confirm choice + coin + bowl + postcard exit

Progress:

```text
REFLECTION 05 / 05
```

Purpose: confirm the future-writing choice from R_04, then make that same choice physical.

Dynamic heading pattern:

```text
You chose:
[SELECTED APPROACH LABEL]
```

The selected visible label is one of:

```text
I write first. AI helps refine.
AI drafts first. I choose what stays.
I write without AI.
```

Optional quiet supporting line:

```text
Carry that choice into the final step.
```

Physical coin mapping:

```text
human-led-ai-refine -> HUMAN FIRST + AI REFINE
ai-led-draft       -> AI DRAFTS FIRST
human-only         -> HUMAN ONLY
```

Instructions:

```text
01  Pick up the coin that matches your choice.
02  Drop that coin into the bowl.
03  Collect your printed postcard on the way out.
```

Use `coin`, not `token`.
Use `bowl`, not `box`.

The postcard uses `reflection.sendChoice` from R_03 to determine the selected letter content.

Use printer stub only.

No confetti, score, winner language, recommendation, or another survey question.

---

# Current Reflection state

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

R_03 may keep `sendChoiceCandidate` transient/local until knob confirmation.

The old separate `voiceChoice` answer is superseded and should not remain a required product state.

# Transition map

```text
A2_03 NEXT -> R_01
R_01 CONTINUE -> R_02
R_02 CONTINUE -> R_03
R_03 DIAL_CONFIRM -> R_04
R_04 CONTINUE -> R_05
R_05 -> physical exit/session complete
```

Back:

```text
R_02 -> R_01
R_03 -> R_02
R_04 -> R_03
```

R_01 BACK remains product-guarded.

# Cross-screen invariants

- same `ReflectionShell` across all five screens;
- progress always `/05`;
- no Arcade 1 or Arcade 2 visual chrome;
- same warm-white background;
- same subtle letter-paper tint for both letters;
- stable left/right ordering: Human + AI left, AI Only right;
- no winner/score/recommendation language;
- no moralized color coding;
- physical inputs may dispatch semantic actions without visible console hardware graphics.
