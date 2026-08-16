# 38 — MUSE Reflection Experience — Source of Truth

**Status:** Current product-flow authority for all `R_*` Reflection screens. Read together with later numbered Reflection files. **File `46-reflection-five-screen-merged-letter-choice.md` is the latest flow override and wins wherever older Reflection files conflict.**

Reflection begins only after both console experiences are complete and both final letters exist.

It is a third experience layer, visually separate from Arcade Console 1 and Arcade Console 2.

## Non-negotiable separation

Reflection must use its own `ReflectionShell`.

Do not use Console 1:

- navy pixel grid;
- MuseWindow;
- purple/lavender desktop chrome;
- pixel sprites/type;
- magenta CTA;
- visible arcade hardware strip.

Do not use Console 2:

- `MUSE / AI ONLY / ARCADE CONSOLE 2` identity;
- signal-red system motif as persistent Reflection language;
- grey control deck;
- visible arcade BACK/NEXT controls;
- visible intensity dial;
- machine-status chrome.

Physical controls may map to Reflection semantic actions without rendering their hardware graphics on screen.

## Entry guard

Reflection may begin only when:

```ts
arcade1.completed === true
arcade1.finalLetter exists
arcade2.completed === true
arcade2.activeGeneratedLetter exists
```

## Canonical five-screen flow

```text
Console 1 complete
→ Console 2 complete
→ R_01 Read both letters side by side
→ R_02 Compare normalized analysis + experience tags
→ R_03 Choose the letter that feels most like you and that you would actually send — dial-driven
→ R_04 Choose future authorship / agency approach
→ R_05 Confirm that choice + matching coin + bowl + postcard exit
→ session complete
```

All progress labels use:

```text
REFLECTION NN / 05
```

Do not use `/06` in current Reflection implementation.

---

# R_01 — Read both letters

Heading:

```text
Read both letters side by side.
```

Supporting line:

```text
Take a moment with each one before comparing how they feel.
```

Show both complete final letters with equal visual weight:

```text
LETTER A — HUMAN + AI
LETTER B — AI ONLY
```

No analysis, tags, selection, or source bias.

`CONTINUE → R_02`.

---

# R_02 — Analysis + experience tags

Show one normalized comparison of both final letters using exactly:

1. emotional warmth
2. personal specificity
3. vocabulary complexity
4. affectionate language

Do not place raw Console 1 and Console 2 analysis components beside each other.

Heading:

```text
Two letters. Two ways of getting there.
```

Supporting line:

```text
Before choosing between them, look at what each one carries.
```

Question:

```text
How did the two experiences feel?
```

Helper:

```text
choose up to 3
```

Allow `1–3` tags from the approved fixture.

Store:

```ts
reflection.experienceTags
```

`CONTINUE → R_03`.

---

# R_03 — Merged voice + send choice

The former standalone `Which letter sounds more like you?` and `Which letter would you actually send?` screens are superseded and merged.

Preferred merged question:

```text
Which letter feels most like you — and is the one you'd actually send?
```

Supporting line:

```text
Choose the one that feels closest to your voice and that you'd put your name behind.
```

Use the approved three-object dial-driven composition:

```text
[ HUMAN + AI LETTER ]  [ CENTRAL QUESTION PIVOT CARD ]  [ AI ONLY LETTER ]
```

The choice is binary:

```text
human-ai
ai-only
```

The old `Parts of both` and `Neither` options are no longer part of the current merged question.

Dial left/right previews a candidate. Knob press confirms and advances.

Store one committed letter choice:

```ts
reflection.sendChoice = 'human-ai' | 'ai-only' | null;
```

A separate durable `reflection.voiceChoice` is no longer required.

`DIAL_CONFIRM → R_04` when a candidate exists.

---

# R_04 — Future authorship / agency approach

Question:

```text
Next time you want to say something that matters,
how would you rather write it?
```

Use exactly three visually equal choices:

```text
I write first. AI helps refine.
AI drafts first. I choose what stays.
I write without AI.
```

States:

```ts
'human-led-ai-refine'
'ai-led-draft'
'human-only'
```

Store:

```ts
reflection.futureApproach
```

No default and no privileged styling.

`CONTINUE → R_05`.

---

# R_05 — Confirm choice + physical exit

The final screen must first tell the visitor which future-writing approach they selected, then translate that same choice into the physical installation ritual.

Recommended heading pattern:

```text
You chose:
[SELECTED APPROACH LABEL]
```

Then instruct:

```text
01  Pick up the coin that matches your choice.
02  Drop that coin into the bowl.
03  Collect your printed postcard on the way out.
```

Use `coin`, not `token`.
Use `bowl`, not `box`.

Physical mapping:

```text
human-led-ai-refine -> HUMAN FIRST + AI REFINE
ai-led-draft       -> AI DRAFTS FIRST
human-only         -> HUMAN ONLY
```

The printed postcard is based on the letter committed in `reflection.sendChoice` on R_03.

Use printer stub only in the current build.

No confetti, score, winner language, moralized feedback, or additional survey question.

---

# Current Reflection state

Preferred current contract:

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

R_03 may use a transient `sendChoiceCandidate` before confirmation.

The old separate `voiceChoice` product answer is superseded by the merged R_03 question.

## Neutrality

Reflection reveals the visitor's own position. Never use winner/recommended labels, moralized red/green states, or unequal treatment of the two letters or three future approaches.

## Latest implementation authority

Read:

```text
docs/implementation/46-reflection-five-screen-merged-letter-choice.md
```

for the latest migration, route, state, dial-interaction, final-coin/bowl, and testing details.
