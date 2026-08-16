# MUSE Codex Implementation Plan — Index

This folder breaks the implementation into durable plans for the three MUSE experience systems.

## Experience architecture

MUSE contains three intentionally distinct visual systems:

1. **Arcade Console 1 — Human + AI** — retro pixel-love-letter arcade UI.
2. **Arcade Console 2 — AI Only** — restrained editorial/technical black-grey-off-white-red UI.
3. **Reflection Experience** — separate Quiet Editorial Gallery UI in warm white / black / grey.

Share infrastructure where useful. Never merge the visual languages.

## Arcade 1 current enhancement bundle

Read:

1. `28-arcade1-motion-audio-interactions.md`
2. `29-arcade1-human-letter-analysis.md`
3. `30-arcade1-enhancement-build-playbook.md`

## Arcade 2 — AI Only current bundle

Read files `18`–`27`, then current overrides:

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
→ A2_01 contextual prompt
→ A2_02 tone controls only
→ A2_03 generated letter + post-generation analysis
```

## Reflection Experience — current canonical bundle

Read in order:

1. `38-reflection-source-of-truth.md`
2. `39-reflection-visual-system.md`
3. `40-reflection-screen-specifications.md`
4. `41-reflection-codex-build-playbook.md`
5. `42-reflection-foundation-visual-calibration.md`
6. `43-reflection-r01-visual-calibration.md` — analysis/tag visual calibration, now R_02
7. `44-reflection-r04-send-choice-dial-interaction.md` — legacy filename, current dial interaction now applies to R_03
8. `46-reflection-five-screen-merged-letter-choice.md` — **latest flow/state/numbering authority**

`45-reflection-consolidated-current-directive.md` is superseded six-screen context only.

Current five-screen Reflection flow:

```text
both final letters exist
→ R_01 read both letters side by side
→ R_02 normalized analysis + experience tags
→ R_03 merged letter choice: feels most like me + I would actually send it — dial-driven
→ R_04 future authorship/agency choice
→ R_05 confirm chosen approach + matching coin + bowl + printed postcard exit
```

All Reflection progress labels use:

```text
REFLECTION NN / 05
```

### R_03 special interaction

The visible composition is:

```text
[ HUMAN + AI LETTER ]  [ QUESTION PIVOT CARD ]  [ AI ONLY LETTER ]
```

- turn dial left -> Human + AI candidate;
- turn dial right -> AI Only candidate;
- pivot card rotates subtly toward the candidate;
- candidate letter gets restrained black-border feedback;
- press rotary knob -> commit `reflection.sendChoice` and advance to R_04;
- no on-screen hardware/dial graphics;
- no separate `voiceChoice` answer in the current flow.

### R_05 physical exit

R_05 first displays the selected future-writing approach, then instructs the visitor to:

```text
pick up the matching coin
→ drop it into the bowl
→ collect the printed postcard
```

Use `coin`, not `token`, and `bowl`, not `box`.

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

- Arcade 1: follow file `30`.
- Arcade 2: follow file `24` plus current overrides through `37`.
- Reflection: follow files `38`–`44`, then **file `46` as the latest authority**.

When requirements conflict, later explicitly approved numbered overrides win over older generic specs.
