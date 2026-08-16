# 38 — MUSE Reflection Experience — Source of Truth

**Status:** Current product-flow authority for all `R_*` reflection screens. Read together with the latest numbered Reflection overrides, especially files `42`–`45`.

The reflection experience begins **only after both console experiences are complete and both final letters exist**.

It is not part of Arcade Console 1 and it is not part of Arcade Console 2.

It is a third, intentionally separate experience layer that compares the two completed artifacts and asks the visitor to reflect on authorship, agency and personal voice.

Where this file conflicts with the older `10-reflection-choice-exit-screens.md`, this file wins. Where a later Reflection calibration/override conflicts with this file, the later numbered file wins.

## Non-negotiable separation

Reflection must NOT inherit the visual shell of either console.

Do not use Console 1:

- navy pixel grid;
- MuseWindow;
- purple title bar;
- pixel sprites;
- magenta CTA;
- pixel typography;
- red/gold/red hardware strip.

Do not use Console 2:

- persistent `MUSE / AI ONLY / ARCADE CONSOLE 2` identity;
- red-square system language as a dominant motif;
- grey hardware deck;
- outlined on-screen BACK/NEXT arcade controls;
- on-screen intensity dial;
- technical system-status typography;
- Console 2 shell geometry.

Reflection gets its own `ReflectionShell` and component system.

Physical inputs may be mapped to Reflection semantic actions without rendering either console's hardware graphics.

## Entry guard

Reflection can begin only when all of the following are available:

```ts
arcade1.completed === true
arcade1.finalLetter exists
arcade2.completed === true
arcade2.activeGeneratedLetter exists
```

Do not enter reflection immediately after Console 1.
Do not enter reflection before the AI-only result exists.

## Canonical six-screen flow

```text
Console 1 complete
→ Console 2 complete
→ R_01 Read both letters side by side
→ R_02 Compare normalized analysis + experience tags
→ R_03 Which letter sounds like you?
→ R_04 Which letter would you actually send? — dial-driven choice
→ R_05 What writing approach would you choose next time?
→ R_06 Physical token + postcard handoff
→ session complete
```

All progress labels must use:

```text
REFLECTION NN / 06
```

Do not restore the older five-screen or eight-question reflection sequence unless explicitly requested later.

---

# R_01 — Read both letters first

## Purpose

Give the visitor a quiet reading moment before analysis, judgment or choice.

Heading:

```text
Read both letters side by side.
```

Supporting line:

```text
Take a moment with each one before comparing how they feel.
```

Display both complete final letters with equal visual weight:

```text
LETTER A — HUMAN + AI
LETTER B — AI ONLY
```

Both letter cards must use identical dimensions, paper tint, border, typography and prominence.

No analysis.
No tags.
No selection.

R_01 CONTINUE routes to R_02.

---

# R_02 — Compare the two letters + reflect on the experience

## Purpose

Show a normalized side-by-side analysis of both completed letters, then ask the visitor how the overall experience felt.

The analysis is descriptive, not a scorecard and not a winner declaration.

## Comparison requirement

Both letters must be compared using the same shared dimensions:

1. emotional warmth;
2. personal specificity;
3. vocabulary complexity;
4. affectionate language.

Do not place raw Console 1 analysis components beside raw Console 2 analysis components.

Use one normalized Reflection comparison model.

Preferred deterministic prototype fixture may resolve to:

```text
EMOTIONAL WARMTH        high        moderate
PERSONAL SPECIFICITY    high        medium
VOCABULARY COMPLEXITY   medium      high
AFFECTIONATE LANGUAGE   high        restrained
```

Do not label either column `better`, `winner`, or `recommended`.

## Experience question

```text
How did the two experiences feel?
```

Helper:

```text
choose up to 3
```

Current tag set:

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

Selected state may invert black/white; do not color-code emotional meaning.

Store in:

```ts
reflection.experienceTags
```

---

# R_03 — Which letter sounds like you?

## Purpose

Voice identity, not send preference.

Prompt:

```text
Which letter sounds more like you?
```

Supporting line:

```text
Not which one is better — which one feels closer to your voice.
```

Show both complete letters side by side with equal visual treatment.

Current options:

- Human + AI
- AI Only
- Parts of both
- Neither

Store independently:

```ts
reflection.voiceChoice =
  | 'human-ai'
  | 'ai-only'
  | 'parts-of-both'
  | 'neither'
  | null;
```

No default selection.

---

# R_04 — Which letter would you actually send?

Detailed current interaction authority: `44-reflection-r04-send-choice-dial-interaction.md`.

## Purpose

Ask for the practical send choice using the physical rotary dial as the primary selector.

Prompt:

```text
Which letter would you actually send?
```

Supporting line:

```text
Choose the one you would put your name behind.
```

Use a three-object composition:

```text
[ HUMAN + AI LETTER ]    [ CENTRAL QUESTION PIVOT CARD ]    [ AI ONLY LETTER ]
```

Both letters remain equal in size, tint and prominence.

Dial left previews Human + AI.
Dial right previews AI Only.
The central question card leans subtly toward the candidate.
The candidate letter receives a restrained stronger border.

Knob press confirms and advances.

Store:

```ts
reflection.sendChoice = 'human-ai' | 'ai-only' | null;
```

Do not infer or preselect this from `voiceChoice`.

The interaction reference changes the interaction metaphor only; do not copy its colorful/playful styling into Reflection.

---

# R_05 — Future authorship / agency stance

## Purpose

After the visitor has decided which letter they would send, ask how they would prefer to approach meaningful writing in the future.

Do not use loaded language such as `give up control` in visible copy.

Preferred question:

```text
Next time you want to say something that matters,
how would you rather write it?
```

Preferred three choices:

### Choice A

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

### Choice B

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

### Choice C

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

All three must use identical card size, typography and selection treatment.

Store:

```ts
reflection.futureApproach =
  | 'human-led-ai-refine'
  | 'ai-led-draft'
  | 'human-only'
  | null;
```

---

# R_06 — Physical handoff / exit ritual

## Purpose

Move from digital reflection to the physical installation exit.

Preferred headline:

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

The printed postcard should use `reflection.sendChoice` to determine which selected letter is prepared for takeaway.

Current prototype may invoke only a printer-service stub.

No confetti.
No winner state.
No gamified score.
No further survey question.

---

# Shared reflection state

Recommended:

```ts
type ReflectionState = {
  experienceTags: string[];

  voiceChoice:
    | 'human-ai'
    | 'ai-only'
    | 'parts-of-both'
    | 'neither'
    | null;

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

R_04 may keep a transient/local `sendChoiceCandidate` before confirmation.

Keep `voiceChoice`, `sendChoice`, and `futureApproach` distinct.

## Neutrality rule

Reflection should reveal the visitor's own position, not tell them which position is correct.

Never use:

- winner badges;
- recommended labels;
- moralized red/green states;
- celebratory treatment for one choice only;
- negative language for AI-led drafting;
- shame language for no-AI choice.

## Current consolidated directive

For the fastest up-to-date implementation summary, read:

```text
docs/implementation/45-reflection-consolidated-current-directive.md
```

That file captures the latest reviewed R_02 state, the inserted R_01 reading screen, the R_03 voice-choice specification, the R_04 dial interaction, and the current six-screen implementation order.
