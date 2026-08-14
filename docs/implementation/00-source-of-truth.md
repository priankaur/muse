# 00 — Source of Truth and Conflict Resolution

MUSE has evolved during design exploration. Several earlier documents and generated screens contain superseded naming, station ordering, footer instructions, and window treatments. Codex must not average those versions together.

## Priority order

When two sources conflict, use this priority order:

1. **Explicit latest user instruction in the current implementation task.**
2. `AGENTS.md`.
3. This implementation-plan bundle in `docs/implementation/`.
4. `docs/reference/muse-ui-style-system-v2.md`.
5. Approved latest visual reference screenshots stored in the repository.
6. Legacy flow documents and older image generations.

If a lower-priority source disagrees with a higher-priority source, the lower-priority rule is obsolete.

## Locked visual truth

The canonical UI is the latest MUSE pixel-arcade / early-desktop hybrid:

- 4:3 composition.
- Dark navy square-grid world.
- Sparse love-letter sprites around the edges.
- Persistent top-left MUSE lockup and top-right console label where specified.
- Large centered desktop-style window.
- **Sharp 90-degree corners on the main window.**
- Purple title bar, yellow menu square, white close square.
- Blank title-bar text area.
- Pale warm lavender/paper interior.
- Chunky pixel typography.
- Magenta primary CTA.
- Dark/purple form outlines.
- Separate 3D physical control strip under the window.
- Red arcade button on the left, gold rotary dial in the center, red arcade button on the right.
- No instructional labels in the hardware strip.

The blank-window-frame asset/reference is the best chrome reference. The latest greeting and recipient-form screens are the best content-layout references.

## Locked experience override

The old flow calls the first console `Ex-Love` and makes it AI-first. That is no longer the current product structure.

The current implementation should model:

1. Registration / entry context.
2. **Arcade 1 — Human + AI**: the visitor starts with their own human material and AI supports/enhances it.
3. **Arcade 2 — AI-only**: the visitor experiences an AI-led alternative using inherited session context, with intentionally reduced soulfulness/empathy compared with the human-led path.
4. Reflection and side-by-side comparison.
5. Final stance / choice.
6. Physical token-wall handoff and printed/takeaway artifact later in the production pipeline.

The user does **not** repeat registration, recipient name, or relationship selection on Arcade 2. Arcade 2 inherits that context from Arcade 1.

## Legacy material that remains useful

The legacy experience flow remains valuable for:

- three-photo capture constraint
- camera/review flow
- typed notes field
- five-dial interaction grammar
- comparison/reflection concepts
- postcard/print handoff concept
- token wall concept
- general physical-control philosophy

Use those details only when they do not conflict with the current Human + AI → AI-only structure.

## Deprecated implementation details

Do not restore any of these merely because they appear in older references:

- `Ex-Love` as the current first-arcade name
- `Next Love` as the current second-arcade name
- AI-first Console 1 ordering
- `MUSE SYSTEM` text inside the purple window bar
- rounded main-window corners
- `HOLD BOTH`
- `SYSTEM MENU` as a footer instruction
- text labels explaining the controls on every screen
- large decorative moon/star scenes that displace the love-letter sprite language
- older dense collage treatment around the window
- controls rendered as flat circles instead of the approved 3D red/red + gold dial set

## Copy is not a design token

Copy can change without changing layout primitives. Codex should never use a copy change as a reason to restyle the screen.

If text becomes longer:

1. use the content-specific type role defined in the design system,
2. adjust content flow within the existing window grid,
3. preserve the same window geometry and shell,
4. only escalate for a design decision if the content genuinely cannot fit at the approved minimum readable size.
