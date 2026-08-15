# 09 — Arcade 2: AI-only Screen Specifications — Superseded

This file is retained only so older links do not break.

The AI-only experience was redesigned after this original plan. **Do not implement Console 2 from the old specification.**

Use the canonical AI-only bundle instead:

1. `18-ai-only-source-of-truth.md`
2. `19-ai-only-visual-system.md`
3. `20-ai-only-component-architecture.md`
4. `21-ai-only-data-state-interactions.md`
5. `22-ai-only-screen-specifications.md`
6. `23-ai-only-testing-acceptance.md`
7. `24-ai-only-codex-build-playbook.md`
8. `docs/reference/ai-only-console2-canonical.png`

## Important override

Console 2 does **not** use the Console 1 pixel arcade shell.

The current first four AI-only screens are:

- `A2_00` — Welcome back / context loaded
- `A2_01` — Short prompt
- `A2_02` — Analysis + editable tone controls
- `A2_03` — Generated letter + insights

After `A2_03`, continue to shared comparison/reflection.

There is no standalone machine-analysis screen separate from tone controls and no required standalone generating screen in the current static flow.

See `18-ai-only-source-of-truth.md` for the complete current contract.