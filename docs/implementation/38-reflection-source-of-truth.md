# 38 — MUSE Reflection Experience — Source of Truth

**Status:** Current product-flow authority for all `R_*` reflection screens.

The reflection experience begins **only after both console experiences are complete and both final letters exist**.

It is not part of Arcade Console 1 and it is not part of Arcade Console 2.

It is a third, intentionally separate experience layer that compares the two completed artifacts and asks the visitor to reflect on authorship, agency and personal voice.

Where this file conflicts with the older `10-reflection-choice-exit-screens.md`, this file wins.

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
- outlined BACK/NEXT arcade controls;
- intensity dial;
- technical system-status typography;
- Console 2 shell geometry.

Reflection gets its own `ReflectionShell` and component system.

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

## Canonical flow

```text
Console 1 complete
→ Console 2 complete
→ R_01 Compare analysis + experience tags
→ R_02 Which letter sounds like you?
→ R_03 Which letter would you send?
→ R_04 What would you choose next time?
→ R_05 Physical token + postcard handoff
→ session complete
```

There are five reflection responsibilities.

Do not restore the older eight-question survey flow unless explicitly requested later.

---

# R_01 — Compare the two letters + reflect on the experience

## Purpose

Show a normalized side-by-side analysis of both completed letters, then ask the visitor how the overall experience felt.

The analysis is descriptive, not a scorecard and not a winner declaration.

## Comparison requirement

Both letters must be compared using the **same shared dimensions**.

Do not place Console 1-only metrics such as visual meaning beside unrelated Console 2-only metrics and imply direct equivalence.

Recommended shared comparison dimensions:

1. emotional warmth;
2. personal specificity;
3. vocabulary complexity;
4. affectionate / romantic language.

These dimensions are chosen because they allow both final letter texts to be compared consistently and support the exhibition question around human voice versus AI polish.

Values can be deterministic fixtures in the prototype.

Prefer restrained textual descriptors or subtle linear readouts rather than charts.

Examples:

```text
EMOTIONAL WARMTH        high        moderate
PERSONAL SPECIFICITY    high        medium
VOCABULARY COMPLEXITY   medium      high
AFFECTIONATE LANGUAGE   high        restrained
```

Do not label either column `better`, `winner`, or `recommended`.

## Experience question

Preferred prompt:

```text
How did the two experiences feel?
```

Use multi-select tags.

Recommended initial tag set:

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

Allow approximately 1–3 selections.

All tags must have equal visual legitimacy.

Selected state may invert black/white; do not color-code emotional meaning.

---

# R_02 — Which letter sounds like you?

## Purpose

Show both completed letters side by side and ask the visitor which one best reflects their own voice.

Prompt:

```text
Which letter sounds more like you?
```

Options:

- Letter A — Human + AI
- Letter B — AI Only
- parts of both
- neither

If the experience should force a binary choice later, that can be changed in content config; default should preserve `parts of both` and `neither` because voice can be mixed.

Store separately from send choice:

```ts
reflection.voiceChoice = 'human-ai' | 'ai-only' | 'both' | 'neither'
```

Do not default-select based on analysis.

---

# R_03 — Which letter would you send?

## Purpose

Show the same two letter artifacts again and ask for the practical choice.

Prompt:

```text
Which letter would you actually send?
```

Primary options:

- Human + AI letter
- AI Only letter

Optional third option only if later approved:

- neither

The two letter surfaces must remain exactly equal in size and visual prominence.

Store:

```ts
reflection.sendChoice = 'human-ai' | 'ai-only' | 'neither'
```

Do not infer this from `voiceChoice`.

A visitor may think one sounds like them but still choose to send the other.

---

# R_04 — Future authorship / agency stance

## Purpose

After the visitor has decided which letter they would send, ask how they would prefer to approach meaningful writing in the future.

Do not use loaded language such as `give up control` in the visible option text.

The conceptual difference can remain in research/implementation notes, but the visitor-facing choices should be neutral and equally legitimate.

Preferred question:

```text
Next time you want to say something that matters, how would you rather write it?
```

Preferred three choices:

### Choice A — Human-led + AI refinement

```text
Start with my own words,
then use AI to refine them.
```

Short label:

```text
I write first. AI helps refine.
```

Meaning: visitor retains initial authorship and uses AI as a tool.

### Choice B — AI-led drafting

```text
Start with an AI draft,
then decide what to keep.
```

Short label:

```text
AI drafts first. I choose what stays.
```

Meaning: AI takes the first authorship step and the visitor works from the machine draft.

### Choice C — Fully human writing

```text
Write it entirely myself,
without AI.
```

Short label:

```text
I write without AI.
```

Meaning: visitor opts out of AI for this type of meaningful communication.

All three must use identical card size, typography and selection treatment.

Do not visually privilege Choice A even if it aligns most closely with the exhibit thesis.

Store:

```ts
reflection.futureApproach =
  | 'human-led-ai-refine'
  | 'ai-led-draft'
  | 'human-only'
```

---

# R_05 — Physical handoff / exit ritual

## Purpose

Move from digital reflection to the physical installation exit.

Preferred headline:

```text
One last choice — make it physical.
```

Preferred instruction sequence:

```text
Pick up the token that matches your choice.
Drop it into the corresponding box.
Collect your printed postcard on the way out.
```

Alternative softer headline:

```text
Take your choice with you.
```

The screen should be extremely simple.

No further survey questions.

No confetti.
No winner state.
No gamified score.

## Token mapping

Physical token/box labels should map exactly to the three `futureApproach` options:

- HUMAN FIRST + AI REFINE
- AI DRAFTS FIRST
- HUMAN ONLY

Exact physical labels can be shortened for fabrication, but software state and physical signage must map one-to-one.

## Postcard

The printed postcard should use `reflection.sendChoice` to determine which selected letter is prepared for takeaway, unless a later printing rule explicitly changes this.

Static prototype may show `POSTCARD READY` / equivalent state and invoke only a printer service stub.

---

# Shared reflection state

Recommended state:

```ts
type ReflectionState = {
  experienceTags: string[];
  voiceChoice: 'human-ai' | 'ai-only' | 'both' | 'neither' | null;
  sendChoice: 'human-ai' | 'ai-only' | 'neither' | null;
  futureApproach:
    | 'human-led-ai-refine'
    | 'ai-led-draft'
    | 'human-only'
    | null;
  completed: boolean;
};
```

Keep these fields distinct.

Do not collapse `voiceChoice` and `sendChoice`.

## Neutrality rule

Reflection should reveal the visitor's own position, not tell them which position is correct.

Never use:

- winner badges;
- recommended labels;
- moralized red/green states;
- celebratory treatment for one choice only;
- negative language for AI-led drafting;
- shame language for no-AI choice.

## Interaction rule

Reflection can reuse shared semantic navigation/state infrastructure, but it must not render either console's visual controls.

If real physical controls are later mapped to reflection actions, handle that below the visual layer.

The on-screen reflection UI remains its own system.
