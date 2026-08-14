# 16 — Definition of Done

A screen is not complete because the copy appears. It is complete when it satisfies architecture, design, behaviour and regression requirements.

## Global static-build completion

- [ ] Project uses React + Vite + TypeScript.
- [ ] Internal stage is 1440 × 1080.
- [ ] Stage scales as one fixed 4:3 composition.
- [ ] Shared shell exists once.
- [ ] Main window always has sharp corners.
- [ ] Purple title bar has no title text.
- [ ] Yellow menu and white X controls match the reference.
- [ ] Pale lavender paper surface is consistent.
- [ ] Pink window backplate is consistent.
- [ ] Top-left brand lockup is consistent.
- [ ] Console label is controlled by screen/console config.
- [ ] Stationery sprites are individual assets/configured placements.
- [ ] Hardware strip is red button / gold dial / red button.
- [ ] No legacy hardware text labels exist.
- [ ] Copy is separated from components.
- [ ] Session state persists between Arcade 1 and Arcade 2.
- [ ] Arcade 2 does not repeat recipient/relationship setup.
- [ ] All planned screens are registered.
- [ ] Fixture camera flow works.
- [ ] Fixture Human + AI result works.
- [ ] Fixture AI-only analysis/result works.
- [ ] Reflection Q1–Q5 works.
- [ ] Side-by-side comparison works.
- [ ] Final stance works.
- [ ] Print payload stub is produced.
- [ ] Main Playwright path passes.
- [ ] Branch tests pass.
- [ ] Reference-backed visual snapshots reviewed.
- [ ] No console errors in happy path.
- [ ] Production build succeeds.

## Per-screen definition of done

For every screen:

- [ ] Uses `ArcadeStage`.
- [ ] Uses shared `MuseWindow` rather than recreating frame markup.
- [ ] Uses shared `HardwareControlStrip`.
- [ ] Uses appropriate console HUD configuration.
- [ ] Uses content/config for copy and options.
- [ ] Uses approved typography roles.
- [ ] Does not add new arbitrary colours.
- [ ] Does not add border radius to main window.
- [ ] Does not add old control instructions.
- [ ] Has explicit focus order for interactive controls.
- [ ] Has explicit validation/next condition.
- [ ] Has a screen-registry entry.
- [ ] Can be opened in development with fixture state.
- [ ] Has at least an interaction test if it accepts input.
- [ ] Has a visual snapshot if it has an approved visual reference.
- [ ] Does not change shared snapshots unexpectedly.

## Visual review questions

Before approval ask:

1. Does this look like the exact same arcade system as the approved welcome and recipient screens?
2. Is the main window still the dominant visual object?
3. Are all corners/chrome consistent?
4. Is the content horizontally balanced rather than drifting left/right?
5. Are the red controls and gold dial identical to other screens?
6. Is any decorative sprite competing with the content?
7. Did content length cause the design to shrink into unreadability?
8. Did this screen introduce a new card/button style that should have reused a primitive?
9. Can the visitor tell what is selected/focused?
10. Did any older deprecated MUSE design element reappear?

If any answer indicates drift, the screen is not done.
