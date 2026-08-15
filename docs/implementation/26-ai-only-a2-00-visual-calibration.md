# 26 — Arcade Console 2 / AI Only — A2_00 Visual Calibration

This file records the visual review of the updated `A2_00` screenshot at `1440 × 1080` after implementation of the large editorial `MUSE` title and refined control deck.

It is the latest calibration authority for `A2_00`. Where it conflicts with earlier A2_00 guidance in files `22` or `25`, this file wins.

## Final review status — APPROVED

The latest submitted `A2_00` screenshot is **visually approved and locked as the Console 2 entry-screen baseline**.

Do not redesign this screen while implementing later AI-only screens.

The following elements are now locked:

- warm off-white main field;
- light-grey lower physical-control deck;
- 2px near-black deck separator;
- small persistent top-left identity: `MUSE / AI ONLY / ARCADE CONSOLE 2`;
- separate oversized editorial `MUSE` display title in the main field;
- large title left aligned with the editorial column;
- system-status row with a sparse red square marker;
- one restrained hairline rule beneath the large title;
- left-aligned `welcome back,` + visitor name block;
- inherited-context sentence below the welcome block;
- technical begin instruction near the lower-left of the content field;
- BACK / NEXT outlined circular controls in the deck;
- outlined intensity dial at right with restrained red pointer;
- no bottom-center `MUSE` wordmark;
- no dominant blue/periwinkle;
- no Console 1 pixel styling;
- strongly left-weighted composition with intentionally large open space to the right.

## Large display MUSE — locked

The separate giant `MUSE` title is approved in its current scale, hierarchy and placement.

It must remain visually dominant over the welcome block.

Approved character:

- heavy condensed / narrow neo-grotesk character;
- uppercase;
- near-black;
- stark editorial/system-poster authority;
- no outline, gradient, shadow, red fill or decorative distortion.

Preferred stack remains:

```css
font-family: "Roboto Condensed", "Arial Narrow", "Liberation Sans Narrow", Arial, sans-serif;
font-weight: 700;
```

Codex must document which actual face resolves in the build. If the approved screenshot was produced using an intentional bundled equivalent rather than `Roboto Condensed`, keep that equivalent stable; do not silently change fonts while building later screens.

Do not enlarge or reposition the title simply to occupy open space.

## Persistent top-left identity — locked

Keep the current geometry and hierarchy.

```text
MUSE
AI ONLY
ARCADE CONSOLE 2
```

- `MUSE` stays bold/condensed and assertive;
- `AI ONLY` stays quiet but readable;
- `ARCADE CONSOLE 2` stays slightly stronger than `AI ONLY`;
- no icon, heart, screen number or badge;
- do not move this identity between AI-only screens.

## Status row — locked

Current pattern:

```text
[red square] CONTEXT LINK ACTIVE // AI ONLY
```

This wording remains fixture/configurable copy, but the visual treatment is locked:

- one small signal-red square;
- mono/system typography;
- muted grey text;
- left aligned with the main editorial column;
- no iconography beyond the square marker;
- no animation/blink.

Do not add more status rows to A2_00.

## Main hairline rule — locked

The single rule beneath the large `MUSE` is approved.

Keep it:

- 1px neutral grey;
- aligned with the left editorial column;
- approximately 600–640px long;
- visually secondary to the 2px deck separator.

Do not extend it full width and do not build a decorative grid around it.

## Welcome block — locked

Current left-aligned composition is approved:

```text
welcome back,
[visitor name]
```

Hierarchy:

- `welcome back,`: regular neutral sans;
- visitor name: stronger/bold neutral sans;
- name remains clearly secondary to the giant `MUSE` display title;
- inherited-context sentence sits beneath in neutral/secondary styling.

Do not recenter or uppercase this content without a new explicit design decision.

## Context-transfer visual — intentionally omitted

Do not restore the earlier radial/dotted context graphic.

The current combination of:

- `CONTEXT LINK ACTIVE // AI ONLY`,
- the inherited-context sentence,
- the technical control deck,

is the approved way to communicate continuity from Arcade 1 on this screen.

## Begin instruction — locked

Current pattern:

```text
[red square] PRESS [NEXT] TO BEGIN
```

Keep:

- lower-left content region above the deck;
- mono/system role;
- near-black text;
- one red square marker;
- no filled CTA;
- no centered duplicate begin button.

The physical `NEXT` deck control performs `BEGIN`.

## Red-marker count — locked

A2_00 uses exactly two primary square markers:

1. status marker;
2. begin marker.

The red dial pointer is a control indicator, not a third square marker.

Do not add extra markers to fill whitespace.

## Control deck — global baseline

The current deck is approved and becomes the shared Console 2 deck baseline.

Lock:

- deck top at shared token around `y = 888`;
- height `192px`;
- light neutral-grey background;
- full-width 2px near-black top separator;
- BACK and NEXT on the left;
- intensity dial on the right;
- intentional empty center;
- no bottom-center wordmark.

### A2_00 states

- `BACK`: visible, disabled / grey;
- `NEXT`: visible, enabled / black;
- `INTENSITY DIAL`: visible, inactive / neutral, with restrained red pointer detail.

Do not remove disabled hardware; geometry must stay fixed across A2 screens.

## Whitespace — locked

The large open right/middle region is an intentional part of the approved composition.

Do not fill it with:

- helper copy;
- progress indicators;
- decorative IDs;
- pseudo-data panels;
- extra rules;
- diagrams;
- AI sparkle motifs;
- extra status labels.

Console 2 should remain strongly left-weighted, sparse and editorial.

## A2_00 regression contract

Any later shared-shell change must preserve this screen.

Before merging a change that touches shared Console 2 tokens/components, re-capture A2_00 at exactly `1440 × 1080` and verify:

- giant title scale/position unchanged;
- small identity anchor unchanged;
- status/begin markers unchanged;
- title hairline unchanged;
- welcome hierarchy unchanged;
- deck split/geometry unchanged;
- BACK disabled and NEXT enabled styling unchanged;
- no bottom-center MUSE;
- no floating duplicate Back/Next actions;
- no dominant blue;
- no Console 1 chrome.

## Next implementation gate — A2_01

`A2_00` is now complete.

Proceed to **Task D / `A2_01` only** from `24-ai-only-codex-build-playbook.md`.

When implementing `A2_01`:

- reuse the exact approved shell;
- reuse the exact small identity anchor;
- reuse the exact control-deck geometry;
- `BACK` becomes enabled;
- `NEXT` is disabled until the prompt contains non-whitespace content, then becomes enabled;
- intensity dial remains visible but inactive;
- do **not** carry the giant `MUSE` display title to A2_01;
- do not carry A2_00-specific status/begin copy into A2_01;
- only the main content body and hardware state may change;
- preserve the black / grey / off-white / restrained-red system;
- stop after a clean `1440 × 1080` A2_01 screenshot for review before implementing A2_02.
