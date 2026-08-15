# 30 — Arcade Console 1 / Human + AI — Enhancement Build Playbook

This playbook governs the new Arcade 1 work requested after the static visual system was established.

The work has two separate tracks:

1. interaction feedback: motion + sound;
2. human-letter analysis: sentiment, emotions, character count, visual meaning.

Do not implement both in one uncontrolled pass.

## Global read order

Before any of these tasks, read:

1. `AGENTS.md`
2. `docs/implementation/03-design-system-implementation.md`
3. `docs/implementation/08-arcade-1-human-ai-screens.md`
4. `docs/implementation/28-arcade1-motion-audio-interactions.md`
5. `docs/implementation/29-arcade1-human-letter-analysis.md`
6. this file
7. current approved Arcade 1 screenshots/references

The locked Arcade 1 design system remains authoritative for geometry and styling.

---

# Task A — Audit current Arcade 1 implementation

Before coding, inspect and report:

- existing CTA component implementation;
- hardware button/dial components;
- semantic action/input architecture;
- current screen-transition implementation;
- current audio utilities, if any;
- existing `prefers-reduced-motion` handling;
- session state around `A1_05`–`A1_08`;
- current character counter in `A1_07`;
- current route/screen registry constraints;
- whether `A1_06A` can be added safely without renumbering downstream screens.

Do not change code until this audit is summarized.

---

# Task B — Add motion feedback only

Implement:

- CTA press/depth-collapse animation;
- red arcade-button press animation;
- gold dial discrete rotation/tick visual;
- short content/page transition state.

Do NOT add sound yet.
Do NOT add analysis screen yet.
Do NOT animate decorative sprites yet.

Acceptance:

- locked visual geometry unchanged at rest;
- keyboard activation gets same feedback as pointer;
- route transitions commit once;
- reduced-motion branch exists;
- 1440×1080 screenshots after settle match approved static baselines.

STOP for review.

---

# Task C — Add semantic sound system

Implement one Arcade 1 audio manager and semantic sound events.

Required first sounds:

- CTA confirm;
- arcade-button press;
- dial tick;
- dial confirm where used;
- page transition cue.

Optional after review:

- processing cue;
- result reveal cue.

Requirements:

- no background music;
- no external network audio;
- first-user-gesture unlock;
- no duplicate sound on one action;
- configurable volume;
- local/WebAudio placeholder sounds replaceable later.

STOP for audio review before decorative sound expansion.

---

# Task D — Add A1_06A human-letter analysis state/model

Implement data/state/service seams only first:

- `HumanLetterAnalysis` type;
- fixture analysis;
- fixture service/interface;
- `arcade1.humanLetterAnalysis` session field;
- route `A1_06 -> A1_06A -> A1_07`;
- no production vision/OCR API.

Tests:

- accept photo -> A1_06A;
- continue -> A1_07;
- fixture persists correctly.

Do not change visuals outside the new screen.

---

# Task E — Implement A1_06A visual screen

Build the new screen using the locked Arcade 1 shell.

Show exactly four primary categories:

1. sentiment analysis;
2. emotions recognized;
3. character count;
4. visual meaning.

Use Arcade 1 pixel panels/components, not Console 2 analytics styling.

Recommended title fixture:

```text
HERE'S WHAT THE MACHINE PICKED UP
```

Recommended helper:

```text
A quick read of your letter before AI adds anything to it.
```

CTA:

```text
CONTINUE
```

Capture a clean 1440×1080 screenshot.

STOP for visual review.

---

# Task F — Integrate motion/sound with new analysis screen

Only after A1_06A visual approval:

- use standard page transition into/out of A1_06A;
- CTA press feedback uses shared component behavior;
- no unique noisy analysis animation;
- optional very short deterministic scan reveal can be proposed, but do not add unless approved.

---

# Task G — Processing + result motion

After core interaction feedback is approved, refine:

- `A1_09` discrete pixel-processing progress;
- `A1_10` short result reveal;
- semantic process/reveal sounds if approved.

No production AI calls.

---

# Task H — Decorative sprite bobbing last

Only after all interaction motion is stable:

- add gentle stepped bobbing to existing approved stationery sprites;
- 3–8px vertical movement;
- low-frame cadence;
- varied phase/duration;
- disabled under reduced motion.

Do not add new sprites.

---

# Testing / regression requirements

For each task:

- run typecheck;
- run relevant unit/component tests;
- run Playwright flow tests;
- capture 1440×1080 screenshots after motion settles;
- ensure locked Arcade 1 shell geometry is unchanged;
- verify Console 2 is unaffected.

Add specific tests for:

- double-click/double-press prevention during transition;
- sound event fires once per semantic action;
- dial detent maps one step to one value update;
- A1_06A renders four analysis categories;
- A1_07 note counter remains independent from A1_06A letter character count.

---

# Do not do

Codex must NOT:

- install an animation framework;
- add cinematic page transitions;
- add background music;
- change Arcade 1 chrome while adding feedback;
- use Console 2 analysis-card styling;
- renumber A1_07–A1_11 without necessity;
- create a live AI/vision dependency in the first pass;
- make sentiment/emotion analysis clinically authoritative;
- treat visual meaning as factual psychological diagnosis;
- add charts/graphs unless explicitly approved.

## Stop discipline

Each task is an approval gate. Do not proceed automatically to the next task after implementation. Report:

- files changed;
- behavior implemented;
- screenshots/audio assets generated;
- tests run;
- visual or audio mismatches;
- any architecture conflict.