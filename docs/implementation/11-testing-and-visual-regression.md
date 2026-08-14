# 11 — Testing and Visual Regression

Visual regression is a core engineering requirement because the project has a locked, reference-driven interface.

## Test layers

### Typecheck

Every task should run the project typecheck.

### Unit/logic tests

Test at least:

- screen registry completeness,
- transition rules,
- required-data guards,
- relationship `Other` validation,
- camera attempt branching,
- session inheritance from Arcade 1 to Arcade 2,
- final print-payload construction.

### Playwright end-to-end

Primary happy-path test:

1. seed registration,
2. enter Arcade 1,
3. pass welcome,
4. enter recipient,
5. select relationship,
6. complete writing/capture fixtures,
7. accept photo,
8. set tuning fixtures,
9. reach Human + AI result,
10. handoff to Arcade 2,
11. enter prompt,
12. pass analysis,
13. tune AI-only controls,
14. reach AI-only result,
15. answer all reflection questions,
16. choose a letter,
17. choose a stance,
18. reach completion.

Add branch tests for:

- `Other` relationship,
- photo retake,
- third-photo no-retake condition,
- missing inherited session state,
- back navigation where allowed.

## Visual reference tests

### Canonical viewport

Always render golden screenshots at the internal 1440 × 1080 stage with a deterministic device-scale setup.

### First required baselines

Create exact screenshot baselines for:

- `A1_00` / latest Discover Your Muse reference if available,
- `A1_01` / latest Hello screen,
- `A1_02` / recipient/relationship form,
- blank MUSE window-frame component showcase,
- hardware-control strip component showcase.

### Component baseline page

Create a development-only route or Storybook-free internal gallery such as:

`/?components=1`

It should render:

- window frame,
- CTA states,
- text field states,
- choice tag states,
- heart divider,
- 3D controls,
- key typography roles.

This allows shared-component regressions to be caught before they spread to all screens.

## Overlay workflow

For reference-backed screens:

1. capture current output,
2. open the approved reference at the same dimensions,
3. compare using overlay/difference mode,
4. correct numeric geometry/tokens,
5. re-run.

Prioritize differences in this order:

1. stage/window geometry,
2. title bar/control geometry,
3. hardware strip,
4. typography scale/position,
5. CTA size/position,
6. body spacing,
7. sprite placement,
8. texture/color nuance.

Do not compensate for a wrong window width by moving individual content elements arbitrarily.

## Snapshot tolerance

Exact raster comparison can vary with fonts and rendering engines. Start strict once fonts/assets are stable. During setup, visual tests can use a small documented threshold, but screenshots should still be human-reviewed against the approved reference.

Never update visual baselines automatically just to make CI green. A baseline change is a design change and should be reviewed.

## Regression rule

If a task only changes one screen's content, shared visual snapshots should remain unchanged. If a shared snapshot changes, Codex must explain why.
