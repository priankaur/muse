# 13 — Implementation Phases and Gates

Do not ask Codex to build the whole product in one pass. The plan intentionally creates approval gates so the locked design cannot drift unnoticed.

# Phase 0 — Repository preparation

Tasks:

- create/confirm Vite React TypeScript app,
- add `AGENTS.md`,
- add docs/reference assets,
- add Playwright,
- add scripts for dev/build/typecheck/test/e2e,
- create the fixed stage shell.

Gate:

- app boots,
- stage is exactly 4:3,
- no design components built twice.

# Phase 1 — Tokens and arcade world

Tasks:

- global token file,
- background grid,
- outer HUD,
- sprite layer/asset manifest,
- stage scaling.

Gate:

- 1440 × 1080 screenshot has correct global composition,
- no browser-responsive reflow.

# Phase 2 — Locked window chrome

Tasks:

- `MuseWindow`,
- blank purple title bar,
- yellow menu square,
- white close square,
- magenta backplate,
- lavender textured interior.

Gate:

- component screenshot matches blank-window reference,
- corners are sharp,
- no title-bar text.

Do not continue until this is approved. Every screen depends on it.

# Phase 3 — Locked hardware strip

Tasks:

- red arcade button component/asset,
- gold rotary dial component/asset,
- strip container,
- exact spacing.

Gate:

- screenshot matches approved hardware reference,
- no labels/instructions,
- left and right buttons are visually identical.

# Phase 4 — Core UI primitives

Tasks:

- typography roles,
- heart divider,
- primary CTA,
- text fields,
- relationship tags,
- rich-text emphasis box,
- letter preview,
- meter/tuning control.

Gate:

- component gallery screenshot approved.

# Phase 5 — First reference screens

Implement only:

- `A1_00`,
- `A1_01`,
- `A1_02`.

Gate:

- visual regression matches approved references,
- shell components frozen.

After this gate, shared visual components should change only with explicit design approval.

# Phase 6 — Complete Arcade 1

Implement `A1_03` through `A1_11` using fixtures.

Gate:

- entire Human + AI path works end-to-end,
- recipient/session data stored,
- result fixture exists,
- no new shell variants introduced.

# Phase 7 — Complete Arcade 2

Implement `A2_00` through `A2_05`.

Gate:

- inherited session works,
- no repeated registration/relationship fields,
- analysis and AI letter are fixtures,
- output available to reflection.

# Phase 8 — Reflection and completion

Implement `R_01` through `R_08`.

Gate:

- both letters compare side by side,
- final stance selected,
- printer payload stub created,
- completion screen reached.

# Phase 9 — End-to-end hardening

Tasks:

- main Playwright path,
- branch tests,
- missing-state recovery,
- stage scaling test,
- console error cleanup,
- visual regression review.

Gate:

- full static experience accepted.

# Phase 10 — Deferred integrations

Only after static acceptance:

1. real physical buttons/dial,
2. camera,
3. handwriting/vision pipeline,
4. AI generation and analysis,
5. printer/email,
6. sound,
7. animation.

Do not start Phase 10 work while shared visual foundations are still changing.
