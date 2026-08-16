# MUSE Codex Implementation Plan — Index

This folder breaks the implementation into durable plans for the three MUSE experience systems.

## Experience architecture

MUSE contains three intentionally distinct visual systems:

1. **Arcade Console 1 — Human + AI** — retro pixel-love-letter arcade UI.
2. **Arcade Console 2 — AI Only** — restrained editorial/technical black-grey-off-white-red UI.
3. **Reflection Experience** — separate Quiet Editorial Gallery UI in warm white / black / grey.

Share infrastructure where useful. Never merge the visual languages.

## Core plans

- `00-source-of-truth.md` — global precedence
- `02-technical-architecture.md` — shared React/stage/state architecture
- `03-design-system-implementation.md` — Console 1 visual system
- `07-screen-inventory.md` — screen registry
- `08-arcade-1-human-ai-screens.md` — Console 1 screens
- `11-testing-and-visual-regression.md` — global testing discipline
- `12-accessibility-and-exhibition-mode.md` — kiosk/accessibility constraints
- `17-preflight-audit.md` — repository/source audit

## Arcade 1 current enhancement bundle

Read:

1. `28-arcade1-motion-audio-interactions.md`
2. `29-arcade1-human-letter-analysis.md`
3. `30-arcade1-enhancement-build-playbook.md`

## Arcade 2 — AI Only current bundle

Read files `18`–`27`, then the latest overrides:

- `31-ai-only-a2-01-visual-calibration.md`
- `32-ai-only-a2-01-contextual-placeholder.md`
- `33-ai-only-a2-01-contextual-hint-calibration.md`
- `34-ai-only-post-generation-analysis-flow.md`
- `35-ai-only-a2-02-visual-calibration.md`
- `36-ai-only-a2-03-post-generation-result-plan.md`
- `37-ai-only-generation-style-guardrails.md`

Current Console 2 flow:

```text
A2_00 welcome
-> A2_01 contextual prompt
-> A2_02 tone controls only
-> A2_03 generated letter + post-generation analysis
```

## Reflection Experience — current canonical bundle

Read in order:

1. `38-reflection-source-of-truth.md`
2. `39-reflection-visual-system.md`
3. `40-reflection-screen-specifications.md`
4. `41-reflection-codex-build-playbook.md`
5. `42-reflection-foundation-visual-calibration.md`
6. `43-reflection-r01-visual-calibration.md`
7. `44-reflection-r04-send-choice-dial-interaction.md`

Current six-screen Reflection flow:

```text
both final letters exist
-> R_01 read both letters side by side
-> R_02 normalized analysis + experience tags
-> R_03 which letter sounds like you
-> R_04 which letter would you send? — dial-driven pivot-card interaction
-> R_05 future authorship/agency choice
-> R_06 physical token + printed postcard exit
```

All progress labels use:

```text
REFLECTION NN / 06
```

### R_04 special interaction

`44` is the latest authority.

The visible composition is:

```text
[ HUMAN + AI LETTER ]  [ QUESTION PIVOT CARD ]  [ AI ONLY LETTER ]
```

- turn dial left -> candidate Human + AI;
- turn dial right -> candidate AI Only;
- center question card rotates subtly toward the candidate;
- candidate letter gets restrained black-border selection feedback;
- press rotary knob -> commit `reflection.sendChoice` and advance to R_05;
- no on-screen hardware/dial graphics inside Reflection;
- no preselection from `voiceChoice`.

## Visual-shell rule

Use separate shells:

```text
ArcadeOneShell
AiOnlyShell
ReflectionShell
```

Never theme one into another.

## Reference files

- `../reference/muse-ui-style-system-v2.md` — Console 1
- `../reference/ai-only-console2-canonical.jpg` — Console 2 content/layout
- `../reference/ai-only-console2-system-refinement-v2.jpg` — Console 2 system styling
- `../reference/muse-experience-flow-legacy.md` — legacy narrative only

## Codex working model

Keep tasks small and stop at visual review gates.

- Arcade 1: follow file `30`.
- Arcade 2: follow file `24` plus latest overrides through `37`.
- Reflection: follow file `41`, then latest calibration/interaction files `42`–`44`.

When requirements conflict, later explicitly approved numbered overrides win over older generic specs.
