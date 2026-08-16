# 45 — MUSE Reflection Experience — Superseded Six-Screen Consolidation

**Status:** Superseded.

This file documented the earlier six-screen Reflection sequence.

The current Reflection flow is now **five screens** because the separate voice-choice and send-choice screens were merged into one dial-driven letter-choice screen.

Do not implement from the old six-screen sequence in this file.

Use the current authorities instead:

1. `38-reflection-source-of-truth.md`
2. `39-reflection-visual-system.md`
3. `40-reflection-screen-specifications.md`
4. `41-reflection-codex-build-playbook.md`
5. `42-reflection-foundation-visual-calibration.md`
6. `43-reflection-r01-visual-calibration.md` — visual calibration for the analysis/tag composition now R_02
7. `44-reflection-r04-send-choice-dial-interaction.md` — legacy filename, current detailed dial interaction now applied to R_03
8. `46-reflection-five-screen-merged-letter-choice.md` — **latest flow/state/numbering authority**

Current canonical sequence:

```text
R_01 Read both letters
→ R_02 Analysis + experience tags
→ R_03 Merged letter choice: feels most like me + I would send it (dial-driven)
→ R_04 Future authorship / agency choice
→ R_05 Confirm chosen approach + matching coin + bowl + postcard exit
```

All progress indicators use:

```text
REFLECTION NN / 05
```

The old separate `reflection.voiceChoice` product answer is no longer required. Current letter selection is committed as `reflection.sendChoice` on R_03.
