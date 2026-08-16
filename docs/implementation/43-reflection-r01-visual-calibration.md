# 43 — MUSE Reflection Experience — Analysis + Tag Visual Calibration

**Status:** Approved visual calibration for the normalized analysis + experience-tag screen. This composition is now **R_02 / 05** in the current Reflection flow.

Read with files `38`–`42` and latest override `46`.

## Review result

The reviewed analysis/tag screen is visually approved and should be preserved.

Keep:

- warm-white Reflection background;
- `REFLECTION 02 / 05` at the shared progress anchor;
- centered editorial heading hierarchy;
- neutral supporting line;
- wide normalized comparison table;
- equal Human + AI / AI Only treatment;
- thin neutral row rules;
- no charts/dashboard cards;
- centered experience-feeling question;
- restrained outlined tags;
- active BACK and state-driven CONTINUE;
- generous whitespace.

Do not redesign this screen.

## Locked copy

Heading:

```text
Two letters. Two ways of getting there.
```

Supporting line:

```text
Before choosing between them, look at what each one carries.
```

Question:

```text
How did the two experiences feel?
```

Helper:

```text
choose up to 3
```

## Comparison grid

Keep exactly:

1. emotional warmth
2. personal specificity
3. vocabulary complexity
4. affectionate language

Column labels:

```text
LETTER A                  LETTER B
HUMAN + AI                AI ONLY
```

Both columns remain equal in width/hierarchy.

Values must come from normalized Reflection data, not be hard-coded inside presentation markup.

Current deterministic fixture may resolve to:

```text
emotional warmth:      high / moderate
personal specificity: high / medium
vocabulary complexity: medium / high
affectionate language: high / restrained
```

Do not add winner/better language, icons, colored meters, charts, or metric cards.

## Tags

Current fixture:

```text
personal
easy
surprising
thoughtful
too polished
distant
expressive
awkward
familiar
made me think
```

Maximum selection:

```text
3
```

Minimum to continue:

```text
1
```

The screenshot state showing `personal`, `thoughtful`, and `too polished` selected is only a selected-state demonstration.

Initial state must be:

```ts
reflection.experienceTags = []
```

### Idle

- warm-white fill;
- 1px neutral border;
- near-black text;
- small radius;
- no shadow.

### Selected

- near-black fill;
- warm-white text;
- same geometry.

No semantic colors.

## Tag wrap

Prefer a balanced centered group at `1440 × 1080`, approximately `5 + 5` if label widths permit.

Use a centered max-width around `700–780px` with `10–14px` gaps.

Do not force equal widths.

## Navigation

Zero selected:

```text
BACK enabled
CONTINUE disabled
```

One to three selected:

```text
BACK enabled
CONTINUE enabled
```

A fourth selection is prevented.

Do not move navigation anchors when state changes.

## Regression

Preserve:

- Reflection shell/background;
- progress/navigation anchors;
- neutral type system;
- absence of console chrome;
- exact `1440 × 1080` stage.

## Current next route

When R_02 is valid:

```text
CONTINUE → R_03
```

R_03 is now the merged dial-driven letter choice defined in file `46`.
