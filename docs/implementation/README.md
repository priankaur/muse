# MUSE Codex Implementation Plan — Index

This folder breaks the implementation into small, durable plans so Codex can work without receiving one giant prompt.

## Experience architecture

MUSE now contains **three intentionally distinct visual systems**:

1. **Arcade Console 1 — Human + AI**
   - retro pixel-love-letter arcade / early-desktop UI
2. **Arcade Console 2 — AI Only**
   - restrained editorial/technical UI using black, grey, warm off-white and sparse signal red
3. **Reflection Experience**
   - separate post-console minimal editorial gallery UI in warm white / black / grey, with only the letter documents on a subtle paper tint

The reflection experience is not a theme of Console 1 or Console 2.

> Share infrastructure where useful. Never merge the three visual languages.

## Core plans

| File | Purpose |
|---|---|
| `00-source-of-truth.md` | Global precedence and current project direction. |
| `01-static-build-scope.md` | Original static implementation scope; later numbered files explicitly override where noted. |
| `02-technical-architecture.md` | Shared React/state/stage architecture. |
| `03-design-system-implementation.md` | Console 1 visual system. |
| `04-assets-and-pixel-rendering.md` | Console 1 asset/pixel rules. |
| `05-content-and-data-model.md` | Shared copy/session contracts. |
| `06-navigation-and-input-model.md` | Shared state machine/input abstraction. |
| `07-screen-inventory.md` | Canonical screen registry. |
| `08-arcade-1-human-ai-screens.md` | Console 1 screen specifications. |
| `09-arcade-2-ai-only-screens.md` | Superseded pointer only. |
| `10-reflection-choice-exit-screens.md` | Superseded pointer to current reflection bundle. |
| `11-testing-and-visual-regression.md` | Global testing discipline. |
| `12-accessibility-and-exhibition-mode.md` | Exhibition/readability/accessibility constraints. |
| `13-implementation-phases.md` | Global implementation phasing. |
| `14-codex-task-playbook.md` | General Codex task sizing. |
| `15-deferred-integrations.md` | Deferred integrations and explicit exceptions. |
| `16-definition-of-done.md` | Global completion criteria. |
| `17-preflight-audit.md` | Repository/source audit. |

## Arcade 1 — Human + AI enhancement bundle

For current Arcade 1 enhancement work read:

1. `28-arcade1-motion-audio-interactions.md`
2. `29-arcade1-human-letter-analysis.md`
3. `30-arcade1-enhancement-build-playbook.md`

Current capture flow includes:

```text
A1_05 capture
-> A1_06 review
-> A1_06A human-letter analysis
-> A1_07 notes/correction
-> A1_08 tuning
-> A1_09 processing
-> A1_10 result
```

The Arcade 1 shell remains visually frozen while motion/sound and the new analysis responsibility are added.

## Arcade 2 — AI Only canonical bundle

For any `A2_*` work, read the current Console 2 bundle and latest overrides:

1. `18-ai-only-source-of-truth.md`
2. `19-ai-only-visual-system.md`
3. `20-ai-only-component-architecture.md`
4. `21-ai-only-data-state-interactions.md`
5. `22-ai-only-screen-specifications.md`
6. `23-ai-only-testing-acceptance.md`
7. `24-ai-only-codex-build-playbook.md`
8. `25-ai-only-a2-00-display-title-refinement.md`
9. `26-ai-only-a2-00-visual-calibration.md`
10. `27-ai-only-a2-01-copy-refinement.md`
11. `31-ai-only-a2-01-visual-calibration.md`
12. `32-ai-only-a2-01-contextual-placeholder.md`
13. `33-ai-only-a2-01-contextual-hint-calibration.md`
14. `34-ai-only-post-generation-analysis-flow.md`
15. `35-ai-only-a2-02-visual-calibration.md`
16. `36-ai-only-a2-03-post-generation-result-plan.md`
17. `37-ai-only-generation-style-guardrails.md`

Current Console 2 flow:

```text
A2_00 welcome / inherited context
-> A2_01 contextual short prompt
-> A2_02 AI-proposed tone controls only
-> generate AI-only letter
-> A2_03 generated letter + post-generation analysis
```

Important current rules:

- A2_02 does not show sentiment/emotion/romance analysis;
- A2_03 is the first visible post-generation analysis state;
- AI-only writing remains high-vocabulary and comparatively emotionally restrained even when tone controls are maximized;
- Console 2 visual shell remains independent from Console 1.

## Reflection Experience — current canonical bundle

Reflection begins only after both final letters exist.

Read in this order:

1. `38-reflection-source-of-truth.md`
2. `39-reflection-visual-system.md`
3. `40-reflection-screen-specifications.md`
4. `41-reflection-codex-build-playbook.md`

Current flow:

```text
both console letters complete
-> R_01 side-by-side normalized analysis + experience tags
-> R_02 which letter sounds like you
-> R_03 which letter would you send
-> R_04 future authorship/agency choice
-> R_05 token + printed postcard exit
```

Reflection visual style:

- warm-white background;
- near-black typography;
- muted grey secondary text;
- thin neutral rules;
- neutral contemporary grotesk typography;
- no console branding/chrome;
- no arcade hardware graphics;
- only letter documents receive a subtle neutral paper tint;
- both letters use the same tint and geometry so comparison remains unbiased.

The reflection interface is a **third visual system**, not a continuation of either console.

## Reference files

- `../reference/muse-ui-style-system-v2.md` — Console 1 canonical visual reference.
- `../reference/ai-only-console2-canonical.jpg` — Console 2 content/layout reference.
- `../reference/ai-only-console2-system-refinement-v2.jpg` — Console 2 latest visual-system/chrome reference.
- `../reference/muse-experience-flow-legacy.md` — legacy narrative context only.

## Key architecture principle

Shared infrastructure may include:

- 1440×1080 stage scaler;
- session state;
- route/state machine;
- semantic input abstraction;
- testing utilities.

Visual shells must remain separate:

```text
ArcadeOneShell
AiOnlyShell
ReflectionShell
```

Do not theme one shell into another.

## Recommended Codex working model

Keep tasks small and stop at visual review gates.

- Arcade 1: follow `30`.
- Arcade 2: follow `24` plus latest numbered overrides through `37`.
- Reflection: follow `41` and stop after foundation and every screen.

Never build reflection inside `MuseWindow` or `AiOnlyShell` simply because those components already exist.

When a requirement is ambiguous, report it rather than inventing a fashionable default.