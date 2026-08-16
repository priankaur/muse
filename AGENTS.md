# MUSE — Codex Project Instructions

This repository implements the MUSE physical two-console experience plus a separate post-console Reflection experience.

Treat explicitly approved visual design as frozen unless the user requests a change.

MUSE has three intentionally distinct visual systems:

1. **Arcade Console 1 — Human + AI** — retro pixel-love-letter arcade / early-desktop UI.
2. **Arcade Console 2 — AI Only** — minimal editorial/technical UI in black, grey, warm off-white and restrained signal red.
3. **Reflection Experience** — independent Quiet Editorial Gallery UI in warm white, black and grey, with only letter documents on subtle neutral paper tint.

Visual convergence between these systems is a bug.

## Read first

Before changing production code:

1. read `docs/implementation/README.md`;
2. read `docs/implementation/00-source-of-truth.md`;
3. read the latest numbered plan for the active experience;
4. inspect current implementation before replacing components.

Shared stage/state/input infrastructure may be reused. Visual shells must remain separate.

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

Read files `18`–`27` plus current overrides `31`–`37`.

Current flow:

```text
A2_00 welcome
→ A2_01 contextual prompt
→ A2_02 tone controls only
→ A2_03 generated letter + post-generation analysis
```

AI-only writing remains high-vocabulary, polished and comparatively emotionally restrained even when tone controls are maximized.

Do not import Reflection UI into Console 2.

---

# Reflection Experience — third visual system

Reflection begins only after both completed letters exist.

Read in order:

1. `docs/implementation/38-reflection-source-of-truth.md`
2. `docs/implementation/39-reflection-visual-system.md`
3. `docs/implementation/40-reflection-screen-specifications.md`
4. `docs/implementation/41-reflection-codex-build-playbook.md`
5. `docs/implementation/42-reflection-foundation-visual-calibration.md`
6. `docs/implementation/43-reflection-r01-visual-calibration.md` — applies to the analysis/tag composition now indexed as R_02
7. `docs/implementation/44-reflection-r04-send-choice-dial-interaction.md` — legacy filename; detailed dial interaction now applies to R_03
8. `docs/implementation/46-reflection-five-screen-merged-letter-choice.md` — **latest current flow/state authority**
9. `docs/implementation/47-reflection-functional-integration.md` — **latest authority for wiring the static Reflection screens into a functional journey**

`45-reflection-consolidated-current-directive.md` is superseded six-screen context only.

## Current five-screen flow

```text
both letters complete
→ R_01 read both letters side by side
→ R_02 normalized analysis + experience-feeling tags
→ R_03 choose the letter that feels most like the visitor and that they would actually send — dial-driven
→ R_04 future authorship/agency choice
→ R_05 confirm that choice + matching coin + bowl + postcard exit
```

All Reflection progress labels use:

```text
REFLECTION NN / 05
```

No `/06` labels remain in current Reflection code.

## Reflection functionalization rule

When converting approved static screens into working screens, follow file `47`.

Functional wiring must:

- preserve approved Reflection geometry/styles;
- use the central route/state/action model rather than screen-local navigation hacks;
- enter Reflection from `A2_03` only when both final letters exist;
- preserve Reflection answers across Back/forward navigation;
- route pointer, keyboard and physical hardware through the same semantic actions;
- keep `R_03` dial preview separate from knob-confirmed `reflection.sendChoice`;
- keep `reflection.sendChoice` separate from `reflection.futureApproach`;
- use `reflection.sendChoice` for postcard content;
- use `reflection.futureApproach` for the matching physical coin;
- keep the printer as an idempotent service stub in the current build;
- test the full five-screen journey end-to-end.

Do not accept functional wiring that visually changes the approved screens.

## Reflection visual rules

Use only `ReflectionShell`.

Use:

- warm-white background;
- black/near-black typography;
- muted grey secondary text;
- thin neutral rules;
- neutral contemporary grotesk;
- generous whitespace;
- equal-weight letter comparison;
- the same subtle paper tint for both letters;
- simple text navigation where applicable.

Do not render:

- `MuseWindow`;
- Arcade 1 grid/pixel/decorative/hardware chrome;
- `AiOnlyShell`;
- Console 2 identity/control deck/on-screen dial;
- Console 2 red-square system motif as persistent Reflection language;
- winner/recommended/score states.

## R_03 merged dial choice

Current question:

```text
Which letter feels most like you — and is the one you'd actually send?
```

Use:

```text
[ HUMAN + AI LETTER ]  [ CENTRAL QUESTION PIVOT CARD ]  [ AI ONLY LETTER ]
```

Dial left/right previews a candidate. The center card leans subtly toward the candidate and the candidate letter receives restrained border feedback.

Knob press commits:

```ts
reflection.sendChoice
```

and advances to R_04.

Do not render a hardware dial graphic. The physical dial is a semantic input only.

The old standalone `reflection.voiceChoice` answer and `Parts of both` / `Neither` voice options are superseded.

## R_05 physical exit language

R_05 must show the selected `reflection.futureApproach` first, then tell the visitor:

```text
01  Pick up the coin that matches your choice.
02  Drop that coin into the bowl.
03  Collect your printed postcard on the way out.
```

Use `coin`, not `token`.
Use `bowl`, not `box`.

Postcard content comes from `reflection.sendChoice` made on R_03.

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

Never implement Reflection as a theme of either console shell.

## Copy

Copy remains configurable. Approved geometry/component styling remains frozen unless explicitly changed.

## Visual acceptance

For every screen:

1. render exactly `1440 × 1080`;
2. capture stage only;
3. compare against latest approved calibration;
4. preserve unrelated experiences;
5. stop and report ambiguity instead of inventing design decisions.
