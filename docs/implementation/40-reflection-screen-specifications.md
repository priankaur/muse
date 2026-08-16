# 40 — MUSE Reflection Experience — Screen Specifications

**Status:** Current screen authority for the six-screen Reflection flow.

Read together with:

- `38-reflection-source-of-truth.md`
- `39-reflection-visual-system.md`
- `41-reflection-codex-build-playbook.md`
- latest numbered Reflection overrides, especially `42`, `43`, and `44`.

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
No system-status chrome.

## Shared top area

Small progress text:

```text
REFLECTION NN / 06
```

Canonical anchor approximately:

```text
x: 72
y: 58–64
```

Use muted grey, small tracked grotesk.

## Shared navigation

Bottom-left:

```text
← BACK
```

Bottom-right where applicable:

```text
CONTINUE →
```

Use neutral text controls.

Do not render arcade hardware graphics.

Physical hardware may still dispatch the same semantic actions invisibly where a specific Reflection screen explicitly maps them.

---

# R_01 — Read both letters

## Purpose

Give the visitor a quiet reading moment before analysis or judgment.

## Heading

```text
Read both letters side by side.
```

Supporting line:

```text
Take a moment with each one before comparing how they feel.
```

## Layout

Display both complete letters using equal `ReflectionLetterCard` components.

Left:

```text
LETTER A
HUMAN + AI
```

Right:

```text
LETTER B
AI ONLY
```

Both cards must have identical dimensions, tint, border, typography and prominence.

This screen is read-only.

No analysis.
No tags.
No selection.

`CONTINUE` routes to `R_02`.

---

# R_02 — Side-by-side analysis + experience tags

This is the screen previously implemented as Reflection 01 and is now `REFLECTION 02 / 06`.

Latest visual calibration: `43-reflection-r01-visual-calibration.md` applies to this composition even though the screen index has shifted.

## Heading

```text
Two letters. Two ways of getting there.
```

Supporting line:

```text
Before choosing between them, look at what each one carries.
```

## Normalized comparison

Use exactly four shared dimensions:

1. emotional warmth
2. personal specificity
3. vocabulary complexity
4. affectionate language

Do not place the raw Console 1 and Console 2 analysis UIs beside each other.

Use one normalized Reflection model.

Column labels:

```text
LETTER A
HUMAN + AI
```

```text
LETTER B
AI ONLY
```

## Experience question

```text
How did the two experiences feel?
```

Helper:

```text
choose up to 3
```

Tags:

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

Allow 1–3 selections.

Store:

```text
reflection.experienceTags
```

`CONTINUE` routes to `R_03`.

---

# R_03 — Which letter sounds like you?

## Purpose

Voice identity, not send preference.

## Heading

```text
Which letter sounds more like you?
```

Supporting line:

```text
Not which one is better — which one feels closer to your voice.
```

Display both letters side by side with identical visual weight.

Selection options:

- Human + AI
- AI Only
- Parts of both
- Neither

Store independently:

```text
reflection.voiceChoice
```

No default selection.

`CONTINUE` routes to `R_04`.

---

# R_04 — Which letter would you send?

**Latest interaction authority:** `44-reflection-r04-send-choice-dial-interaction.md`.

## Purpose

A physical dial-driven choice between the two completed letters.

This choice is independent from `reflection.voiceChoice`.

## Prompt

```text
Which letter would you actually send?
```

Supporting line:

```text
Choose the one you would put your name behind.
```

## Three-object composition

Use:

```text
[ HUMAN + AI LETTER ]    [ QUESTION PIVOT CARD ]    [ AI ONLY LETTER ]
```

The two full letter cards remain equal in size, tint and prominence.

The central question card acts as the visual selector and rotates subtly toward the current dial candidate.

## Dial semantics

Initial:

```text
sendChoiceCandidate = null
pivot = 0deg
```

Turn left:

```text
sendChoiceCandidate = human-ai
pivot ≈ -5deg to -7deg
```

Turn right:

```text
sendChoiceCandidate = ai-only
pivot ≈ +5deg to +7deg
```

Candidate letter receives restrained 2px near-black border feedback.

Do not change letter paper colors.

## Confirm

Pressing the rotary knob commits the candidate:

```text
reflection.sendChoice = sendChoiceCandidate
```

and advances directly to `R_05`.

Do not require an additional visible Continue click after knob confirmation.

If no candidate is selected, knob press does not advance.

Mouse/keyboard fallback may set the same semantic candidate/confirm actions without changing the visible design.

Do not show a Reflection hardware deck or dial graphic.

---

# R_05 — Future authorship stance

## Heading

```text
Next time you want to say something that matters,
how would you rather write it?
```

Use three visually equal choice cards.

### A

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

### B

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

### C

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

No option receives privileged styling.

Store the selected future approach.

`CONTINUE` routes to `R_06`.

---

# R_06 — Token + postcard exit

## Heading

```text
One last choice — make it physical.
```

Instructions:

```text
01  Pick up the token that matches your choice.
02  Drop it into the corresponding box.
03  Collect your printed postcard on the way out.
```

Physical mapping:

```text
human-led-ai-refine -> HUMAN FIRST + AI REFINE
ai-led-draft       -> AI DRAFTS FIRST
human-only         -> HUMAN ONLY
```

Prepare the postcard from `reflection.sendChoice` using the printer stub only in the current build.

No confetti.
No score.
No winner screen.
No additional survey question.

---

# Cross-screen invariants

- same `ReflectionShell` across all six screens;
- no Arcade 1 visual chrome;
- no Arcade 2 visual chrome;
- same warm-white background;
- same letter-paper tint for Human + AI and AI Only;
- same left/right Letter A / Letter B ordering on all letter comparison screens;
- `voiceChoice` and `sendChoice` remain independent;
- no winner, score or recommendation language;
- progress is sequence-only, never points;
- physical inputs may be mapped semantically without rendering either console's hardware graphics inside Reflection.

# Transition map

```text
A2_03 NEXT
  -> R_01

R_01 CONTINUE
  -> R_02

R_02 CONTINUE
  -> R_03

R_03 CONTINUE
  -> R_04

R_04 DIAL_CONFIRM
  -> R_05

R_05 CONTINUE
  -> R_06

R_06
  -> physical exit/session complete
```

Back routes:

```text
R_02 BACK -> R_01
R_03 BACK -> R_02
R_04 BACK -> R_03
R_05 BACK -> R_04
```

R_01 BACK behavior should remain product-guarded because returning into A2_03 may be undesirable once Reflection begins.
