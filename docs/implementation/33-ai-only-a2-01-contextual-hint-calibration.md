# 33 — Arcade Console 2 / AI Only — A2_01 Contextual Hint Calibration

This file records the screenshot review after the contextual Arcade 1-derived prompt hint from file `32` was implemented on `A2_01`.

It is the latest visual/content calibration for the hint itself. Where it conflicts with generic placeholder rules in files `27` or `31`, this file wins. File `32` remains the source/behavior authority.

## Review status

The contextual-hint direction is **approved**.

The current screenshot successfully makes Console 2 feel like a continuation of Arcade 1 rather than a generic AI prompt form.

The approved visible pattern is:

```text
example: stay close to this from your first letter —
“I love the life we are making in all its imperfect, playful detail.”
```

This exact excerpt is approved **only if Codex has verified that it exists verbatim in the active Arcade 1 session/fixture**. If it does not exist in the source data, replace it with an exact short sentence that does. Do not preserve an invented quote merely because the screenshot looks correct.

## What is visually locked

Preserve:

- the current A2_01 title and supporting line;
- the centered textarea position and dimensions;
- the two-line contextual hint structure;
- the neutral prefix `example: stay close to this from your first letter —`;
- quotation marks around the inherited source excerpt;
- the `0 / 120` counter at bottom-right;
- BACK active / NEXT disabled in the empty state;
- inactive intensity dial;
- the current large whitespace region;
- the existing shell and control-deck geometry.

Do not add another explanation label such as `FROM YOUR FIRST LETTER`, a quote card, icon, badge, or red marker around the hint.

## Placeholder typography calibration

The current hint reads correctly but must remain visibly a **hint**, not prefilled content.

Use:

- content sans role;
- regular weight (`400` preferred);
- approximately `16–18px` at the 1440×1080 stage;
- muted grey around the existing A2_01 hint color;
- normal line-height;
- no italics;
- no bold quote styling.

If the current browser/CSS rendering makes the hint look semibold, explicitly set placeholder font weight to `400`.

The inherited quote must not be visually promoted above the prefix with a separate font, color, size, or weight.

## Counter calibration

The counter remains slightly low-contrast in the reviewed screenshot.

Keep its exact position and mono/system role, but ensure final readability around:

```text
#777777 – #858585
```

Do not make the counter black in the normal empty state.

## Context provenance requirement

Before treating this screen as fully locked, Codex must report:

1. the exact Arcade 1 source object/field used;
2. whether the excerpt came from:
   - handwritten/extracted human-letter text,
   - the Human + AI result fixture,
   - or a deterministic fallback fixture;
3. the exact source sentence copied into the hint.

No runtime AI generation is allowed for placeholder copy in the current build.

## State behavior remains locked

The contextual hint is not input.

Empty state:

```text
prompt === ''
characterCount === 0
NEXT === disabled
contextualHint === visible
```

After the visitor types:

```text
contextualHint === hidden
characterCount === prompt.length
NEXT === enabled when prompt.trim().length > 0
```

Do not automatically copy the Arcade 1 quote into the prompt state on focus/click.

## Regression acceptance

A2_01 can be treated as visually locked once all of the following pass:

- the contextual excerpt is verified against Arcade 1 source data;
- placeholder weight is regular, not semibold;
- counter contrast is readable;
- empty-state screenshot matches the approved composition;
- typed-state behavior works;
- A2_00 remains unchanged;
- no geometry shifts occur from the two-line contextual hint;
- NEXT remains disabled while only the placeholder is visible.

## Next gate

After this verification, proceed to `Task E — A2_02 interpretation + tone controls` from file `24` only.

Do not redesign A2_01 while working on A2_02. Treat A2_00 and A2_01 as regression baselines.
