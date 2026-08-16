# 41 — MUSE Reflection Experience — Codex Build Playbook

Use this plan to build reflection as a separate third visual system without contaminating either console.

## Read order

Before any reflection implementation, read:

1. `AGENTS.md`
2. `docs/implementation/38-reflection-source-of-truth.md`
3. `docs/implementation/39-reflection-visual-system.md`
4. `docs/implementation/40-reflection-screen-specifications.md`
5. `docs/implementation/10-reflection-choice-exit-screens.md` only as legacy context where non-conflicting

Do not implement reflection from Console 1 or Console 2 screen specs.

## Phase A — Audit

Inspect:

- current route/state machine;
- current A2_03 NEXT behavior;
- existing reflection routes/components;
- whether reflection currently mounts `ArcadeOneShell`, `MuseWindow`, `AiOnlyShell`, or `AiControlDeck`;
- current state fields for letter choice/stance;
- current printer stub;
- existing comparison data/analysis fixtures.

Report what will be removed, reused, and created.

Critical audit condition:

If reflection currently renders inside either console shell, identify and remove that coupling before styling screens.

## Phase B — Reflection foundation only

Create/refactor:

- `ReflectionShell`
- `reflection.tokens.css`
- `ReflectionProgress`
- `ReflectionNavigation`
- `ReflectionLetterCard`
- `ReflectionTag`
- `ReflectionChoiceCard`
- `ReflectionComparisonGrid`

Shared infrastructure may reuse:

- 1440×1080 stage scaler;
- session store;
- semantic navigation/actions;
- test utilities.

Do NOT reuse visual shell/chrome components from either console.

Render an empty/calibration reflection shell and stop for review.

Foundation acceptance:

- warm-white background;
- no pixel UI;
- no AI-only control deck;
- no hardware graphics;
- no console branding lockup;
- neutral grotesk typography;
- black/grey only outside letter paper tint;
- simple sequence progress allowed;
- stage exactly 1440×1080.

## Phase C — R_01 only

Implement side-by-side shared analysis comparison + experience tags.

Use exactly the shared comparison schema from file `38`/`40`.

Do not simply render the separate Arcade 1 and Arcade 2 analysis UIs next to each other.

That would visually and semantically merge incompatible analysis models.

Create normalized reflection comparison data.

Implement 1–3 tag multi-select.

Capture screenshot and stop.

## Phase D — R_02 only

Implement the two letter cards and voice choice.

Preserve identical letter order and geometry.

Allow:

- Human + AI
- AI Only
- parts of both
- neither

Capture screenshot and stop.

## Phase E — R_03 only

Reuse the same letter comparison geometry.

Change only the question/responsibility to send choice.

Do not carry `voiceChoice` selection state visually into this screen.

Capture screenshot and stop.

## Phase F — R_04 only

Implement the three future-authorship choice cards.

Use exact current copy from file `40` unless the product owner changes it.

All cards equal size and hierarchy.

Capture screenshot and stop.

## Phase G — R_05 only

Implement final physical handoff instruction screen.

Use printer stub only.

No real hardware integration.

No confetti/score/winner state.

Capture screenshot and stop.

## Phase H — Integration

Wire:

```text
A2_03 NEXT -> R_01
R_01 -> R_02 -> R_03 -> R_04 -> R_05
```

Reflection entry guard requires both console outputs.

Do not route A2_03 NEXT into any Arcade 1-styled legacy reflection shell.

## Testing

Add tests asserting:

- reflection cannot begin until both final letters exist;
- no `MuseWindow` mounts on R_* routes;
- no `AiOnlyShell`/`AiControlDeck` mounts on R_* routes;
- R_01 uses a shared normalized comparison schema;
- R_01 tags are multi-select with configured max;
- `voiceChoice` and `sendChoice` are separate;
- R_02 and R_03 letter order is identical;
- R_04 exposes exactly 3 equal stance choices;
- R_05 print payload uses `sendChoice`;
- Console 1 and Console 2 regressions remain unchanged.

## Visual regression

Capture all five screens at exactly `1440 × 1080`.

Reflection screenshot baselines must not include:

- browser chrome;
- console hardware deck;
- console identity lockups;
- dev overlay;
- toast UI.

## Stop gates

Stop after every screen for review.

Do not build all five screens in one uncontrolled pass.

Recommended order:

```text
foundation
R_01
R_02
R_03
R_04
R_05
integration
full regression
```

## Non-negotiable anti-drift rule

If a reflection screen begins to look recognizably like Arcade 1 or Arcade 2, stop and correct the shell/components before continuing.

Reflection must read as a distinct third chapter of the exhibition.
