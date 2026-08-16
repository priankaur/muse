# MUSE — Codex Project Instructions

This repository implements the MUSE physical two-console experience plus a separate post-console reflection experience.

Treat all explicitly approved visual design as **frozen** unless the user requests a change.

MUSE now has **three intentionally distinct visual systems**:

1. **Arcade Console 1 — Human + AI**
   - retro pixel-love-letter arcade / early-desktop UI
2. **Arcade Console 2 — AI Only**
   - minimal editorial/technical UI using black, grey, warm off-white and restrained signal red
3. **Reflection Experience**
   - independent quiet editorial/gallery UI in warm white, black and grey, with only letter documents on a subtle paper tint

Visual convergence between these three systems is a bug.

## Read this first

Before changing production code:

1. read `docs/implementation/README.md`;
2. read `docs/implementation/00-source-of-truth.md`;
3. read the latest numbered plan for the experience being changed;
4. inspect current implementation before creating replacement components.

## Shared rendering model

All three experiences may reuse the same exhibition-stage infrastructure:

- internal design canvas: `1440 × 1080`;
- aspect ratio: `4:3`;
- scale the complete stage proportionally;
- no independent responsive reflow of major regions;
- deterministic geometry for screenshot regression.

Shared stage/state infrastructure does **not** imply shared visual chrome.

---

# Console 1 — Human + AI

Read:

- `docs/reference/muse-ui-style-system-v2.md`
- `docs/implementation/03-design-system-implementation.md`
- `docs/implementation/08-arcade-1-human-ai-screens.md`
- `docs/implementation/28-arcade1-motion-audio-interactions.md`
- `docs/implementation/29-arcade1-human-letter-analysis.md`
- `docs/implementation/30-arcade1-enhancement-build-playbook.md`

Non-negotiable visual rules:

- deep navy grid world;
- love-letter pixel sprites;
- top-left `MUSE SYSTEM v1.0 / LOVE LETTERS, REWIRED.`;
- sharp-cornered MuseWindow;
- blank purple title bar;
- yellow menu square left;
- white X square right;
- pale textured lavender interior;
- pixel typography;
- magenta CTAs;
- red 3D button — gold dial — red 3D button hardware strip;
- no old labelled footer.

Current approved enhancements:

- CTA/button/dial feedback motion;
- short stepped page transitions;
- semantic interaction sounds;
- `A1_06A` human-letter analysis with sentiment, emotions recognized, recognized-text character count and qualified visual meaning.

Do not import Console 2 or Reflection components into Console 1.

---

# Console 2 — AI Only

Read the current bundle in order:

- `docs/implementation/18-ai-only-source-of-truth.md`
- `docs/implementation/19-ai-only-visual-system.md`
- `docs/implementation/20-ai-only-component-architecture.md`
- `docs/implementation/21-ai-only-data-state-interactions.md`
- `docs/implementation/22-ai-only-screen-specifications.md`
- `docs/implementation/23-ai-only-testing-acceptance.md`
- `docs/implementation/24-ai-only-codex-build-playbook.md`
- `docs/implementation/25-ai-only-a2-00-display-title-refinement.md`
- `docs/implementation/26-ai-only-a2-00-visual-calibration.md`
- `docs/implementation/27-ai-only-a2-01-copy-refinement.md`
- `docs/implementation/31-ai-only-a2-01-visual-calibration.md`
- `docs/implementation/32-ai-only-a2-01-contextual-placeholder.md`
- `docs/implementation/33-ai-only-a2-01-contextual-hint-calibration.md`
- `docs/implementation/34-ai-only-post-generation-analysis-flow.md`
- `docs/implementation/35-ai-only-a2-02-visual-calibration.md`
- `docs/implementation/36-ai-only-a2-03-post-generation-result-plan.md`
- `docs/implementation/37-ai-only-generation-style-guardrails.md`
- `docs/reference/ai-only-console2-canonical.jpg`
- `docs/reference/ai-only-console2-system-refinement-v2.jpg`

Current visual language:

- warm off-white main field;
- light-grey lower control deck;
- near-black primary text;
- muted grey secondary/system text;
- restrained signal red;
- heavy condensed `MUSE` identity/display role;
- neutral grotesk content typography;
- mono/semi-mono system labels;
- precise rules/separators;
- outlined BACK/NEXT physical controls;
- outlined intensity dial with restrained red pointer.

Do not use Console 1 pixel chrome on any `A2_*` route.

Current flow:

```text
A2_00 welcome/context
-> A2_01 contextual short prompt
-> A2_02 five AI-proposed tone controls only
-> generate
-> A2_03 generated letter + post-generation analysis
```

Important current rules:

- no sentiment/emotion/romance analysis on A2_02;
- analysis appears only after generation on A2_03;
- each generated variant owns matching analysis;
- AI-only writing remains high-vocabulary, polished and comparatively emotionally restrained even when all tone settings are maximized;
- tone sliders operate inside that fixed AI-only expressive envelope.

Do not import Reflection UI into Console 2.

---

# Reflection Experience — third visual system

Reflection begins only after **both** console experiences are complete and both final letters exist.

Read in order:

- `docs/implementation/38-reflection-source-of-truth.md`
- `docs/implementation/39-reflection-visual-system.md`
- `docs/implementation/40-reflection-screen-specifications.md`
- `docs/implementation/41-reflection-codex-build-playbook.md`

`docs/implementation/10-reflection-choice-exit-screens.md` is now a superseded pointer only.

Current flow:

```text
both letters complete
-> R_01 side-by-side normalized analysis + experience tags
-> R_02 which letter sounds like you
-> R_03 which letter would you send
-> R_04 future authorship/agency choice
-> R_05 physical token + postcard exit
```

## Reflection visual rules

Reflection must use its own `ReflectionShell`.

Use:

- warm-white background;
- black/near-black typography;
- muted grey secondary text;
- thin neutral rules;
- neutral contemporary grotesk typography;
- generous whitespace;
- equal-weight comparison columns;
- subtle neutral paper tint for letter documents only;
- the SAME letter-paper tint for both letters to avoid bias;
- simple text Back/Continue actions;
- sequence progress only if useful.

Do NOT render:

- `MuseWindow`;
- Arcade 1 navy grid/pixel sprites/pixel typography/magenta CTA/hardware strip;
- `AiOnlyShell`;
- Console 2 persistent identity;
- Console 2 grey hardware deck;
- Console 2 arcade buttons or intensity dial;
- Console 2 red-square system motif as a persistent visual language;
- winner/better/recommended badges;
- moralized green/red answer states;
- game-like scoring.

Reflection must not look like Arcade 1 with colors removed or Arcade 2 with the control deck removed.

It is a separate editorial chapter of the exhibition.

## Reflection comparison neutrality

Both letters must receive identical visual prominence.

For R_01, use one normalized shared comparison schema rather than placing incompatible Console 1 and Console 2 analysis components side by side.

Current shared comparison dimensions:

- emotional warmth;
- personal specificity;
- vocabulary complexity;
- affectionate language.

For R_02 and R_03:

- keep Letter A / Letter B ordering stable;
- keep card size/background/border identical;
- store `voiceChoice` and `sendChoice` separately;
- do not default one based on analysis or prior selection.

For R_04 use exactly three equal future-approach choices:

- `I write first. AI helps refine.`
- `AI drafts first. I choose what stays.`
- `I write without AI.`

Do not visually privilege one choice.

---

# Architecture rule

Share only genuinely shared infrastructure.

Recommended separation:

```text
shared:
  stage scaler
  session state
  route/state machine
  semantic input abstraction
  tests

visual systems:
  ArcadeOneShell
  AiOnlyShell
  ReflectionShell
```

Never implement Reflection as a prop/theme of either console shell.
Never implement Console 2 as a theme of `MuseWindow`.

## Copy rule

Copy is editable. Approved visual geometry/component styling is not.

Keep copy and fixtures in content/config/state layers rather than hard-coding them into visual components.

## Visual acceptance

For every approved screen:

1. render at exactly `1440 × 1080`;
2. capture stage only;
3. compare against current approved reference/calibration;
4. correct through shared tokens/components rather than compensating decoration;
5. confirm unrelated experiences did not change.

## Change discipline

For every task:

1. name the implementation-plan file governing the work;
2. identify which of the three visual systems is active;
3. audit existing components;
4. make the smallest reversible change;
5. run typecheck/tests/relevant screenshots;
6. report changed files and unresolved mismatches.

If something is ambiguous, stop and report it instead of designing through it.