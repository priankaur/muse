# 41 — MUSE Reflection Experience — Codex Build Playbook

Use this plan to build Reflection as a separate third visual system.

## Read order

Before Reflection work, read:

1. `AGENTS.md`
2. `docs/implementation/38-reflection-source-of-truth.md`
3. `docs/implementation/39-reflection-visual-system.md`
4. `docs/implementation/40-reflection-screen-specifications.md`
5. `docs/implementation/42-reflection-foundation-visual-calibration.md`
6. `docs/implementation/43-reflection-r01-visual-calibration.md` — applies to the analysis/tag composition now indexed as R_02
7. `docs/implementation/44-reflection-r04-send-choice-dial-interaction.md` — interaction reference, now migrated to current R_03 by file 46
8. `docs/implementation/45-reflection-consolidated-current-directive.md` — historical six-screen consolidation
9. `docs/implementation/46-reflection-five-screen-merged-letter-choice.md` — **latest authority; wins on current flow/state/numbering**

## Phase A — Audit

Inspect:

- current Reflection routes/components;
- current progress count;
- whether old `/06` assumptions remain;
- whether a standalone voice-choice route/state still exists;
- current analysis/tag screen implementation;
- whether R_01 reading screen exists;
- current semantic dial/knob input abstraction;
- current future-approach state;
- current printer stub;
- any `token`/`box` copy that must become `coin`/`bowl`.

Do not redesign already approved Reflection components during migration.

## Phase B — Preserve approved shell

Preserve file `42` baseline:

- `1440 × 1080`;
- background `#FAF9F6`;
- top-left progress;
- bottom text navigation where applicable;
- no console chrome;
- no visible hardware deck;
- no MUSE console identity;
- neutral grotesk type;
- generous whitespace.

## Phase C — Preserve R_02 and migrate progress

The normalized analysis + tag screen already exists and is visually approved.

Preserve its composition.

Update:

```text
REFLECTION 02 / 05
```

Keep:

- normalized four-dimension comparison;
- `How did the two experiences feel?`;
- `choose up to 3`;
- 1–3 selection logic;
- zero initial tag selection;
- black selected tags / outlined idle tags;
- balanced wrap refinement if still needed.

## Phase D — R_01 reading screen

Progress:

```text
REFLECTION 01 / 05
```

Show both completed letters equally.

No analysis, tags or choice.

`CONTINUE → R_02`.

## Phase E — R_03 merged dial-driven letter choice

The old standalone voice-choice screen and old send-choice screen are merged.

Progress:

```text
REFLECTION 03 / 05
```

Question:

```text
Which letter feels most like you — and is the one you'd actually send?
```

Supporting line:

```text
Choose the one that feels closest to your voice and that you'd put your name behind.
```

Use the approved pivot composition:

```text
[ HUMAN + AI LETTER ] [ CENTRAL QUESTION PIVOT CARD ] [ AI ONLY LETTER ]
```

Dial left/right previews a candidate.

Candidate border feedback remains restrained.

Knob press commits:

```ts
reflection.sendChoice
```

and routes to `R_04`.

Remove the old product requirement for:

```ts
reflection.voiceChoice
```

and remove the old standalone voice options `Parts of both` / `Neither` from the current flow.

Do not show active Continue that bypasses knob confirmation.

Capture neutral, left-candidate, right-candidate states.

## Phase F — R_04 future authorship choice

Progress:

```text
REFLECTION 04 / 05
```

Question:

```text
Next time you want to say something that matters,
how would you rather write it?
```

Use exactly three equal choices:

1. `I write first. AI helps refine.`
2. `AI drafts first. I choose what stays.`
3. `I write without AI.`

Store `reflection.futureApproach`.

No default/recommendation.

`CONTINUE → R_05`.

## Phase G — R_05 confirmation + physical exit

Progress:

```text
REFLECTION 05 / 05
```

First show the visitor the selected future-writing approach from R_04.

Recommended dynamic heading:

```text
You chose:
[SELECTED APPROACH LABEL]
```

Then show physical instructions:

```text
01  Pick up the coin that matches your choice.
02  Drop that coin into the bowl.
03  Collect your printed postcard on the way out.
```

Use `coin`, not `token`.
Use `bowl`, not `box`.

Physical coin mapping:

```text
human-led-ai-refine -> HUMAN FIRST + AI REFINE
ai-led-draft       -> AI DRAFTS FIRST
human-only         -> HUMAN ONLY
```

Postcard content comes from `reflection.sendChoice` committed on R_03.

Printer stub only.

## Integration

Wire:

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

R_01 BACK remains guarded.

## Testing

Assert:

- Reflection starts only after both final letters exist;
- no console shell/chrome mounts on `R_*`;
- every progress label uses `/05`;
- no `R_06` route is required;
- no standalone voice-choice route is required;
- old `voiceChoice` is not a required current answer;
- R_01 shows both letters and no analysis/selection;
- R_02 uses normalized comparison + 1–3 tags;
- R_03 dial left/right selects candidate;
- R_03 knob confirm with null does not advance;
- R_03 knob confirm commits `sendChoice` and routes to R_04;
- R_04 has exactly three equal future-approach choices;
- R_05 displays the selected future approach;
- R_05 uses matching coin/bowl language;
- postcard payload uses `sendChoice`;
- Console 1 and Console 2 do not regress.

## Visual regression

Capture all five screens at exactly `1440 × 1080`, including interaction states listed in file `46`.

## Current recommended migration order

```text
1. audit old six-screen assumptions
2. preserve/renumber current analysis/tag screen as R_02 / 05
3. ensure R_01 / 05 exists
4. merge old voice/send responsibilities into current R_03 / 05
5. move future-approach choice to R_04 / 05
6. convert exit to R_05 / 05 with dynamic choice confirmation + coin + bowl + postcard
7. full routing/state/test migration
8. visual regression
```

If Reflection starts to look like either console, stop and correct the visual-shell coupling before continuing.
