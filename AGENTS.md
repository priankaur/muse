# MUSE — Codex Project Instructions

This repository implements the MUSE physical two-console experience plus a separate post-console reflection experience.

Treat all explicitly approved visual design as **frozen** unless the user requests a change.

MUSE has **three intentionally distinct visual systems**:

1. **Arcade Console 1 — Human + AI**
   - retro pixel-love-letter arcade / early-desktop UI
2. **Arcade Console 2 — AI Only**
   - minimal editorial/technical UI using black, grey, warm off-white and restrained signal red
3. **Reflection Experience**
   - independent quiet editorial/gallery UI in warm white, black and grey, with only letter documents on a subtle paper tint

Visual convergence between these systems is a bug.

## Read first

Before changing production code:

1. read `docs/implementation/README.md`;
2. read `docs/implementation/00-source-of-truth.md`;
3. read the latest numbered plan for the active experience;
4. inspect current implementation before creating replacement components.

All three experiences may share the `1440 × 1080` stage scaler, session state, semantic input abstraction and tests. They must not share visual shells.

---

# Console 1 — Human + AI

Read:

- `docs/reference/muse-ui-style-system-v2.md`
- `docs/implementation/03-design-system-implementation.md`
- `docs/implementation/08-arcade-1-human-ai-screens.md`
- `docs/implementation/28-arcade1-motion-audio-interactions.md`
- `docs/implementation/29-arcade1-human-letter-analysis.md`
- `docs/implementation/30-arcade1-enhancement-build-playbook.md`

Use only the approved pixel-love-letter arcade visual language.

Do not import Console 2 or Reflection styling.

---

# Console 2 — AI Only

Read the current bundle through the latest numbered overrides:

- `18-ai-only-source-of-truth.md`
- `19-ai-only-visual-system.md`
- `20-ai-only-component-architecture.md`
- `21-ai-only-data-state-interactions.md`
- `22-ai-only-screen-specifications.md`
- `23-ai-only-testing-acceptance.md`
- `24-ai-only-codex-build-playbook.md`
- `25-ai-only-a2-00-display-title-refinement.md`
- `26-ai-only-a2-00-visual-calibration.md`
- `27-ai-only-a2-01-copy-refinement.md`
- `31-ai-only-a2-01-visual-calibration.md`
- `32-ai-only-a2-01-contextual-placeholder.md`
- `33-ai-only-a2-01-contextual-hint-calibration.md`
- `34-ai-only-post-generation-analysis-flow.md`
- `35-ai-only-a2-02-visual-calibration.md`
- `36-ai-only-a2-03-post-generation-result-plan.md`
- `37-ai-only-generation-style-guardrails.md`

Console 2 remains high-vocabulary, polished and comparatively emotionally restrained even when tone controls are maximized.

Do not import Reflection UI into Console 2.

---

# Reflection Experience — third visual system

Reflection begins only after both completed letters exist.

Read in order:

- `docs/implementation/38-reflection-source-of-truth.md`
- `docs/implementation/39-reflection-visual-system.md`
- `docs/implementation/40-reflection-screen-specifications.md`
- `docs/implementation/41-reflection-codex-build-playbook.md`
- `docs/implementation/42-reflection-foundation-visual-calibration.md`
- `docs/implementation/43-reflection-r01-visual-calibration.md`
- `docs/implementation/44-reflection-r04-send-choice-dial-interaction.md`

`10-reflection-choice-exit-screens.md` is superseded.

## Current six-screen flow

```text
both letters complete
-> R_01 read both letters side by side
-> R_02 normalized analysis + experience-feeling tags
-> R_03 which letter sounds like you
-> R_04 which letter would you send? (dial-driven)
-> R_05 future authorship/agency choice
-> R_06 token + postcard exit
```

All progress indicators use:

```text
REFLECTION NN / 06
```

## Reflection visual rules

Use only `ReflectionShell`.

Use:

- warm-white background;
- black/near-black typography;
- muted grey secondary text;
- thin neutral rules;
- neutral contemporary grotesk typography;
- generous whitespace;
- equal-weight comparison columns;
- same subtle neutral paper tint for both letters;
- simple Reflection navigation.

Do not render:

- `MuseWindow`;
- Arcade 1 grid/pixel sprites/pixel typography/magenta CTAs/hardware graphics;
- `AiOnlyShell`;
- Console 2 identity or hardware deck;
- Console 2 red-square system motif as persistent Reflection language;
- winner/recommended/score states.

## R_04 dial-driven send choice

`44-reflection-r04-send-choice-dial-interaction.md` is the latest authority.

R_04 uses a three-object composition:

```text
[ HUMAN + AI LETTER ]  [ CENTRAL QUESTION PIVOT CARD ]  [ AI ONLY LETTER ]
```

The physical rotary dial controls a transient `sendChoiceCandidate`:

- left detent -> Human + AI;
- right detent -> AI Only.

The central question card rotates subtly toward the candidate side while the corresponding letter receives restrained border feedback.

Pressing the rotary knob commits `reflection.sendChoice` and advances to R_05.

Important:

- do not render an on-screen hardware deck or dial graphic;
- the physical dial is a semantic input only;
- do not preselect from `reflection.voiceChoice`;
- do not change letter paper colors;
- mouse/keyboard fallback may use the same semantic actions without changing visible design.

---

# Architecture

Share only genuine infrastructure:

```text
shared:
  stage scaler
  session state
  route/state machine
  semantic input abstraction
  tests

visual shells:
  ArcadeOneShell
  AiOnlyShell
  ReflectionShell
```

Never implement Reflection as a theme/prop of either console shell.

## Copy

Copy remains configurable in content/state layers. Approved geometry and component styling remain frozen unless explicitly changed.

## Visual acceptance

For every screen:

1. render exactly `1440 × 1080`;
2. capture stage only;
3. compare against the latest approved calibration;
4. correct shared tokens/components instead of adding compensating decoration;
5. confirm unrelated experiences did not regress.

If a requirement is ambiguous, stop and report it instead of inventing a design decision.
