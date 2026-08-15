# 26 — Arcade Console 2 / AI Only — A2_00 Visual Calibration

This file records the visual review of the updated `A2_00` screenshot at `1440 × 1080` after implementation of the large editorial `MUSE` title and refined control deck.

It is the latest calibration authority for `A2_00`. Where it conflicts with earlier A2_00 guidance in files `22` or `25`, this file wins.

## Review status

The overall A2_00 composition is **approved as the baseline direction**. Do not redesign it.

The following elements are now locked:

- warm off-white main field;
- light-grey lower physical-control deck;
- 2px near-black deck separator;
- small persistent top-left identity: `MUSE / AI ONLY / ARCADE CONSOLE 2`;
- separate oversized editorial `MUSE` display title in the main field;
- system-status row with a sparse red square marker;
- one restrained hairline rule beneath the large title;
- left-aligned `welcome back,` + visitor name block;
- inherited-context sentence below the welcome block;
- technical begin instruction near the lower-left of the content field;
- BACK / NEXT outlined circular controls in the deck;
- outlined intensity dial at right with restrained red pointer;
- no bottom-center `MUSE` wordmark;
- no dominant blue/periwinkle;
- no Console 1 pixel styling.

## Final calibration: large display MUSE

The large `MUSE` title is now present and must remain.

Current hierarchy is correct: small persistent identity first, then status line, then oversized display title.

One final typography requirement remains: **verify that the display title is actually using the approved condensed neo-grotesk face rather than falling back to a broad Arial-style sans.**

Preferred stack:

```css
font-family: "Roboto Condensed", "Arial Narrow", "Liberation Sans Narrow", Arial, sans-serif;
font-weight: 700;
```

Target character:

- heavy;
- tall;
- condensed;
- near-black;
- editorial/system-poster authority;
- no shadow, outline, gradient or red fill.

Starting size range remains approximately `132–146px` at 1440×1080. Do not enlarge simply to fill space. Preserve the current overall vertical hierarchy.

If `Roboto Condensed` is intended but not actually bundled/loaded, fix the font loading before approving the screen.

## Persistent top-left identity

Keep its current geometry.

The `MUSE` line should remain bold/condensed, but it must stay visually subordinate to the oversized display title.

`AI ONLY` is intentionally quieter, but it must remain readable. Do not reduce it below practical legibility merely to make it look technical.

Recommended minimum contrast/size at the canonical stage:

- `AI ONLY`: ~11–12px, muted grey but clearly readable;
- `ARCADE CONSOLE 2`: ~11–12px, near-black/stronger than `AI ONLY`.

## Status row

Current pattern is approved:

```text
[red square] CONTEXT LINK ACTIVE // AI ONLY
```

This is fixture/configurable copy, not immutable product copy.

Lock the visual treatment:

- one 8px signal-red square;
- mono/system typography;
- muted grey text;
- left aligned with the main editorial column;
- no additional iconography;
- no animation/blink.

Do not add more status rows to A2_00.

## Main hairline rule

The single rule beneath the large MUSE title is approved.

Keep it:

- 1px neutral grey;
- aligned with the left editorial column;
- approximately 600–640px long;
- visually secondary to the 2px deck separator.

Do not extend it full-width and do not add a decorative grid.

## Welcome block

Current left-aligned composition is approved.

Hierarchy:

```text
welcome back,
[visitor name]
```

Recommended character:

- `welcome back,`: regular neutral sans;
- visitor name: stronger/bold neutral sans;
- name may be larger/heavier than the prefix but must remain clearly secondary to the giant `MUSE` title.

Do not center this block again unless a new approved reference changes the composition.

Do not uppercase the welcome copy.

## Context transfer visual

The earlier four-screen reference included a radial/dotted context-transfer signal. In the current refined A2_00 composition, the combination of:

- `CONTEXT LINK ACTIVE // AI ONLY`,
- inherited-context sentence,
- and the technical control-deck language

already communicates transfer sufficiently.

**Do not reintroduce the radial context signal into A2_00 unless explicitly requested later.**

This omission is now intentional for the refined editorial composition, not a missing component.

## Begin instruction

Current placement/pattern is approved:

```text
[red square] PRESS [NEXT] TO BEGIN
```

Keep:

- lower-left content region above the deck;
- mono/system role;
- near-black text;
- one small red square marker;
- no filled CTA;
- no centered duplicate begin button.

NEXT in the physical deck performs BEGIN.

## Red marker count

A2_00 should use **exactly two primary red square markers** in the current composition:

1. system/status marker;
2. begin-instruction marker.

The dial pointer is also red but is a control indicator, not a square marker.

Do not add more red markers merely to make the screen feel designed.

## Control deck

The current deck composition is approved and should become the shared visual baseline for all A2 screens.

Lock:

- deck top at shared token around `y = 888`;
- height `192px`;
- light neutral-grey background;
- full-width 2px near-black top separator;
- BACK and NEXT left;
- intensity dial right;
- intentional empty center;
- no bottom-center wordmark.

### A2_00 states

- BACK: visible, disabled, grey/inactive;
- NEXT: visible, enabled, black/active;
- INTENSITY DIAL: visible, inactive; label and outer treatment may be muted while pointer remains the restrained signal detail.

Do not remove disabled hardware; keep geometry stable.

## Whitespace

The large open right/middle area is intentional and approved.

Do not add:

- helper copy;
- progress indicators;
- decorative IDs;
- pseudo-data panels;
- extra rules;
- diagrams;
- AI sparkle motifs;
- extra status labels

to fill the space.

The screen should remain strongly left-weighted and editorial.

## A2_00 final acceptance checklist

Before moving to `A2_01`, Codex must verify:

- stage is exactly 1440×1080;
- stage-only screenshot is captured;
- giant MUSE title remains separate from small identity;
- display title actually resolves to the approved condensed font or a documented equivalent;
- no radial context signal is rendered;
- exactly two red square micro-markers are used in A2_00;
- single 1px title hairline remains restrained;
- BACK disabled state is visibly distinct;
- NEXT is clearly active;
- dial remains visually present but inactive;
- deck geometry is unchanged;
- no bottom-center MUSE;
- no floating duplicate Back/Next actions;
- no dominant blue;
- no Console 1 styling.

## Next implementation gate

Once the above typography verification and A2_00 regression snapshot pass, `A2_00` may be considered visually locked.

Then proceed to **Task D / A2_01 only** from `24-ai-only-codex-build-playbook.md`.

When implementing A2_01:

- reuse the exact same shell, identity and control deck;
- do not show the giant `MUSE` display title unless a future screen-specific plan explicitly requests it;
- only the main content body and hardware enabled/disabled states should change.
