# 41 — MUSE Reflection Experience — Codex Build Playbook

Use this plan to build Reflection as a separate third visual system without contaminating either console.

## Read order

Before any Reflection implementation, read:

1. `AGENTS.md`
2. `docs/implementation/38-reflection-source-of-truth.md`
3. `docs/implementation/39-reflection-visual-system.md`
4. `docs/implementation/40-reflection-screen-specifications.md`
5. `docs/implementation/42-reflection-foundation-visual-calibration.md`
6. `docs/implementation/43-reflection-r01-visual-calibration.md` — applies to the analysis/tag composition now indexed as R_02
7. `docs/implementation/44-reflection-r04-send-choice-dial-interaction.md`
8. `docs/implementation/45-reflection-consolidated-current-directive.md`

`docs/implementation/10-reflection-choice-exit-screens.md` is superseded legacy context only.

Do not implement Reflection from Console 1 or Console 2 screen specs.

## Phase A — Audit

Inspect:

- current route/state machine;
- current `A2_03 NEXT` behavior;
- existing Reflection routes/components;
- whether Reflection currently mounts `ArcadeOneShell`, `MuseWindow`, `AiOnlyShell`, or `AiControlDeck`;
- current state fields for tags/voice/send/future approach;
- current printer stub;
- existing normalized comparison data/fixtures;
- current semantic rotary/dial input abstraction;
- current Reflection progress count and route numbering.

Report what is already present, what must be preserved, what must be renumbered, and what remains to be built.

Critical audit condition:

If Reflection currently renders inside either console shell, identify and remove that coupling before continuing.

## Phase B — Foundation

Foundation is already visually approved in file `42`.

Preserve:

- `ReflectionShell`;
- `reflection.tokens.css`;
- warm-white `#FAF9F6` field;
- neutral grotesk type;
- top-left Reflection progress;
- bottom text navigation anchors;
- no console chrome;
- no hardware deck;
- no persistent MUSE identity;
- no footer separator/deck.

Do not redesign the approved shell while adding screens.

## Phase C — Current R_02 preservation + six-screen migration

The analysis/tag composition already exists and was visually reviewed.

Before adding new screens:

1. preserve its approved composition;
2. change its progress label to `REFLECTION 02 / 06`;
3. preserve normalized comparison dimensions;
4. preserve selected tag treatment (black fill / warm-white text);
5. ensure `choose up to 3` helper is present unless explicitly removed later;
6. keep max 3 selections;
7. keep CONTINUE disabled at zero and enabled at 1–3;
8. if practical, refine tag wrapping toward a balanced centered layout without redesigning the component.

Do not rebuild R_02 from scratch.

## Phase D — R_01 read-both-letters screen

Insert a new screen before R_02.

Progress:

```text
REFLECTION 01 / 06
```

Copy:

```text
Read both letters side by side.
Take a moment with each one before comparing how they feel.
```

Show two equal full letter cards:

```text
LETTER A — HUMAN + AI
LETTER B — AI ONLY
```

No analysis.
No tags.
No selection.

Capture screenshot and stop for review if the user requests stage-by-stage approval.

## Phase E — R_03 voice choice

Progress:

```text
REFLECTION 03 / 06
```

Question:

```text
Which letter sounds more like you?
```

Supporting line:

```text
Not which one is better — which one feels closer to your voice.
```

Display both complete letters side by side with identical visual weight.

Choices:

- Human + AI
- AI Only
- Parts of both
- Neither

Store only in `reflection.voiceChoice`.

No default.

CONTINUE enabled after selection.

Capture empty + selected state screenshots.

## Phase F — R_04 dial-driven send choice

Read file `44` before implementation.

Progress:

```text
REFLECTION 04 / 06
```

Use:

```text
[ HUMAN + AI LETTER ] [ CENTRAL QUESTION PIVOT CARD ] [ AI ONLY LETTER ]
```

Dial left previews Human + AI.
Dial right previews AI Only.
The center card leans subtly toward the candidate.
The candidate letter receives a restrained stronger border.

Knob press commits `reflection.sendChoice` and advances directly to R_05.

Do not preselect from `voiceChoice`.

Do not render an on-screen hardware deck or dial graphic.

Do not show an active Continue action that bypasses the dial-confirm behavior.

Capture neutral, left-candidate and right-candidate screenshots.

## Phase G — R_05 future authorship / agency choice

Progress:

```text
REFLECTION 05 / 06
```

Question:

```text
Next time you want to say something that matters,
how would you rather write it?
```

Use exactly three equal choice cards:

1. `I write first. AI helps refine.`
2. `AI drafts first. I choose what stays.`
3. `I write without AI.`

Store `reflection.futureApproach` independently.

No recommendation or preferred styling.

Capture empty + selected screenshots.

## Phase H — R_06 physical handoff

Progress:

```text
REFLECTION 06 / 06
```

Headline:

```text
One last choice — make it physical.
```

Instructions:

```text
01  Pick up the token that matches your choice.
02  Drop it into the corresponding box.
03  Collect your printed postcard on the way out.
```

Use printer stub only.

Postcard payload must use `reflection.sendChoice`.

No confetti/score/winner state.

## Phase I — Integration

Wire the canonical sequence:

```text
A2_03 NEXT -> R_01
R_01 CONTINUE -> R_02
R_02 CONTINUE -> R_03
R_03 CONTINUE -> R_04
R_04 DIAL_CONFIRM -> R_05
R_05 CONTINUE -> R_06
R_06 -> physical exit/session complete
```

Back routes:

```text
R_02 BACK -> R_01
R_03 BACK -> R_02
R_04 BACK -> R_03
R_05 BACK -> R_04
```

R_01 BACK remains product-guarded.

Reflection entry guard requires both console outputs.

Do not route into any Arcade 1-styled legacy reflection shell.

## Testing

Add/update tests asserting:

- Reflection cannot begin until both final letters exist;
- no `MuseWindow` mounts on R_* routes;
- no `AiOnlyShell`/`AiControlDeck` mounts on R_* routes;
- every Reflection progress label uses `/06`;
- R_01 shows both letters and no analysis/selection;
- R_02 uses normalized shared comparison data;
- R_02 tags are 1–3 multi-select with no fourth selection;
- `voiceChoice` and `sendChoice` are separate;
- R_03 allows exactly the current four voice options;
- R_04 dial left/right updates candidate correctly;
- R_04 knob confirm commits and routes only when candidate exists;
- `voiceChoice` does not preselect R_04;
- R_05 exposes exactly 3 equal future-approach choices;
- R_06 print payload uses `sendChoice`;
- Console 1 and Console 2 regressions remain unchanged.

## Visual regression

Capture all six screens at exactly `1440 × 1080`.

Include state screenshots defined in file `45`.

Reflection screenshot baselines must not include:

- browser chrome;
- console hardware deck;
- console identity lockups;
- dev overlay;
- toast UI.

## Stop gates

Stop after every new screen for review unless the user explicitly authorizes a broader pass.

Current recommended order from the latest implementation state:

```text
preserve/refine existing R_02
insert R_01
R_03
R_04
R_05
R_06
integration
full regression
```

## Non-negotiable anti-drift rule

If a Reflection screen begins to look recognizably like Arcade 1 or Arcade 2, stop and correct the shell/components before continuing.

Reflection must read as a distinct third chapter of the exhibition.
