# 25 — Arcade Console 2 / AI Only — A2_00 Display-Title Refinement

This file records the latest approved correction after review of the first refined Console 2 shell screenshot.

It is a **specific override for `A2_00` and the Console 2 display-title system**. Where this file conflicts with the earlier `A2_00` section in `22-ai-only-screen-specifications.md`, this file wins.

The shell/control-deck direction is otherwise retained.

## Review finding

The first refined AI-only shell correctly implemented:

- warm off-white main field,
- light-grey lower control deck,
- strong black deck separator,
- outlined BACK / NEXT buttons,
- outlined intensity dial,
- red dial pointer,
- no Console 1 pixel styling,
- sparse monochrome visual language.

However, it **missed the dominant oversized editorial title treatment** shown by `docs/reference/ai-only-console2-system-refinement-v2.jpg`.

The small top-left `MUSE / AI ONLY / ARCADE CONSOLE 2` lockup is not sufficient by itself.

## Locked correction: two separate MUSE roles

Console 2 now has two distinct typographic MUSE roles on the entry screen.

### 1. Persistent system identity

Top-left, unchanged in role:

```text
MUSE
AI ONLY
ARCADE CONSOLE 2
```

Approximate anchor:

```text
x = 72
y = 58
```

The `MUSE` line remains heavy/condensed and assertive, but this lockup is still a small persistent system identity.

### 2. Large editorial display title

`A2_00` must also contain a separate, dominant large-format:

```text
MUSE
```

inside the main content field.

This large title is the primary visual anchor of the entry screen.

Do not solve this requirement by merely increasing the top-left lockup size.

Do not move the persistent identity into the hero position.

Do not add `MUSE` to the lower control deck.

## Visual character of the large MUSE title

The large title should inherit the **weight, density and editorial authority** demonstrated by the `DIGITAL LOVE LETTER` headline in `ai-only-console2-system-refinement-v2.jpg`.

The reference phrase itself is not approved product copy.

Use:

- heavy condensed neo-grotesk,
- uppercase,
- near-black,
- visually dense,
- stark,
- technical/editorial,
- museum-poster-like,
- no decorative effects.

Starting implementation stack:

```css
font-family: "Roboto Condensed", "Arial Narrow", "Liberation Sans Narrow", Arial, sans-serif;
font-weight: 700;
font-size: 132px;
line-height: 0.88;
letter-spacing: -0.03em;
color: var(--ai-ink);
```

Calibrate within approximately `118–150px` only if screenshot comparison requires it.

No:

- outline-only type,
- gradient,
- shadow,
- red fill,
- watermark opacity,
- 3D/pixel effects.

## Approximate `A2_00` title geometry

Use the canonical `1440 × 1080` stage.

Starting box:

```text
x: 76–90px
y: 170–210px
width allowance: 560–720px
```

The large title should sit in the upper/mid-left content region and should not collide with the persistent identity.

Use the refinement screenshot for typographic mass and the current MUSE composition for exact spacing calibration.

## A2_00 hierarchy after this refinement

The entry screen should read in this order:

```text
small persistent identity

small system-status line / red marker

LARGE MUSE DISPLAY TITLE

welcome back,
[user name]

inherited-context message / context signal

begin instruction

---------------- strong deck separator ----------------

BACK       NEXT                                  INTENSITY DIAL
```

This is a hierarchy description, not a literal text mockup.

Whitespace remains important, but the page must no longer read as an almost empty off-white canvas.

## System-status microcopy

A restrained status line may sit above or near the large MUSE title.

Pattern:

```text
[red square]  SYSTEM STATUS TEXT
```

Use the existing `SignalMarker` component.

Typography:

- system/mono role,
- 13–16px,
- muted grey / near-black,
- technical tracked appearance.

Do **not** copy reference-only wording such as:

```text
SYSTEM INITIALIZED // MUSE OS v.1.0
ID: 882-99-ALPHA
```

Keep product copy configurable.

A safe temporary fixture may use neutral wording such as:

```text
CONTEXT LINK ACTIVE // AI ONLY
```

but this is fixture copy, not a permanently locked sentence.

## Red marker discipline

The latest shell underused the red signal language.

For `A2_00`, use approximately `1–3` meaningful red micro-markers maximum.

Good uses:

- system status,
- begin instruction,
- a small active machine-state label.

Do not scatter markers decoratively.

## Secondary linework

Keep the strong control-deck separator.

In the main field, a small number of `SystemRule` hairlines may be introduced to support editorial/system hierarchy.

Examples:

- short rule aligned with system metadata,
- section separator between display identity and contextual information,
- precise content alignment rule.

Rules:

- `1px` neutral grey or near-black,
- no full decorative grid,
- no boxing every element,
- no spreadsheet/dashboard look.

## Welcome content relationship

The large `MUSE` title does not replace the functional welcome content.

Keep:

```text
welcome back,
[user name]
```

plus inherited-context messaging.

The welcome block should be visually secondary to the large title and should not compete at the same scale.

Do not rewrite the welcome content into uppercase merely because the display title is uppercase.

## Control deck state on A2_00

Keep the currently approved deck geometry.

- `BACK`: visible, disabled / neutral
- `NEXT`: enabled and acts as BEGIN
- `INTENSITY DIAL`: visible, inactive / neutral

Do not redesign the deck as part of this correction unless screenshot calibration shows a geometry mismatch.

## New component recommendation

Create a dedicated reusable component:

```text
AiDisplayTitle
```

Responsibilities:

- render heavy editorial display typography,
- consume display tokens,
- accept copy via props,
- support screen-specific placement without changing font construction.

Do **not** make `AiDisplayTitle` persistent on every Console 2 screen automatically.

For now it is required on `A2_00`; future use on other screens requires explicit approval or a screen plan.

## A2_00 acceptance criteria

Do not approve `A2_00` until all are true:

- separate persistent small identity exists,
- separate oversized `MUSE` display title exists,
- title is visually dominant,
- title uses heavy condensed character,
- title is near-black and not red,
- large title is not placed in control deck,
- `DIGITAL LOVE LETTER` is not copied,
- welcome/context content remains present,
- red markers are sparse but visible,
- main-field linework is restrained,
- deck geometry remains stable,
- stage remains exactly `1440 × 1080`,
- stage-only screenshot is captured,
- no Console 1 chrome appears.

## Codex stop condition

For the next implementation pass:

1. update only the shared display-title primitive and `A2_00` composition required by this file,
2. capture a clean `1440 × 1080` A2_00 screenshot,
3. run relevant tests/typecheck,
4. report remaining visual mismatch,
5. **STOP**.

Do not proceed to `A2_01`, `A2_02` or `A2_03` until the updated A2_00 screenshot is visually reviewed.