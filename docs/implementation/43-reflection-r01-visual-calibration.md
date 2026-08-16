# 43 — MUSE Reflection Experience — R_01 Visual Calibration

**Status:** Approved empty-state baseline for `R_01`, with small final refinements before locking the screen.

Read this after:

- `38-reflection-source-of-truth.md`
- `39-reflection-visual-system.md`
- `40-reflection-screen-specifications.md`
- `41-reflection-codex-build-playbook.md`
- `42-reflection-foundation-visual-calibration.md`

Where this file conflicts with earlier generic R_01 layout guidance, **this file wins for the reviewed R_01 composition**.

## Review result

The current R_01 screenshot is visually successful and clearly belongs to the Reflection experience rather than either arcade console.

The screen is approved as the **empty-selection baseline**.

The following are working and should be preserved:

- warm-white Reflection background;
- quiet top-left `REFLECTION 01 / 05` progress;
- centered editorial question hierarchy;
- neutral supporting line;
- wide side-by-side normalized comparison table;
- equal visual treatment of Letter A / Human + AI and Letter B / AI Only;
- thin neutral row rules;
- no charts or dashboard cards;
- no console colors/chrome;
- centered experience-feeling question;
- restrained outlined tags;
- active BACK and disabled CONTINUE in the empty-selection state;
- generous whitespace around the main content.

Do not redesign this screen.

---

# Locked copy

## Main heading

```text
Two letters. Two ways of getting there.
```

## Supporting line

```text
Before choosing between them, look at what each one carries.
```

## Experience question

```text
How did the two experiences feel?
```

Keep all three strings configurable in the Reflection content layer.

---

# Comparison grid

The current table-like editorial treatment is approved.

Keep exactly four normalized comparison dimensions:

1. emotional warmth
2. personal specificity
3. vocabulary complexity
4. affectionate language

Column structure remains:

```text
LETTER A                  LETTER B
HUMAN + AI                AI ONLY
```

Both columns must remain equal in width and hierarchy.

Do not:

- highlight one column;
- tint one letter type differently;
- add winner/better language;
- add icons;
- add colored meters;
- add radar/pie/progress charts;
- put each metric inside a card.

The row-label column may remain muted grey while the two compared values remain near-black.

## Data provenance

The visible comparison values must come from a **normalized Reflection comparison adapter** built from the two completed letters / their available analysis data.

Do not permanently hard-code the reviewed values only as decorative copy.

For deterministic prototype fixtures, it is acceptable for the normalized adapter to resolve to values such as:

```text
emotional warmth:
  Human + AI -> high
  AI Only -> moderate

personal specificity:
  Human + AI -> high
  AI Only -> medium

vocabulary complexity:
  Human + AI -> medium
  AI Only -> high

affectionate language:
  Human + AI -> high
  AI Only -> restrained
```

But those values should live in fixture/state/normalization data, not be embedded in the visual component.

The same component must be able to render different normalized comparison data later.

---

# Tag block

The current outlined tag style is approved.

Keep the initial fixture set:

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

Maximum selections:

```text
3
```

## Small usability refinement

Add a very quiet helper line under the question and before the tags:

```text
choose up to 3
```

Treatment:

- approximately `13–14px`;
- regular weight;
- muted Reflection grey;
- centered;
- no icon;
- no box;
- no color accent.

This is functional guidance, not decorative copy.

## Tag wrapping

The reviewed screenshot currently resolves visually to a long first row and a short two-tag second row.

Refine the tag container so the ten options form a more balanced centered composition.

Preferred canonical target at `1440 × 1080`:

```text
5 tags
5 tags
```

or an equivalently balanced wrap if exact label widths require slight variation.

Do not force equal tag widths. Preserve content-driven tag widths.

Use a centered max-width container so a final row with only one or two orphaned tags is avoided at the canonical viewport.

Recommended starting max width:

```text
700–780px
```

Maintain approximately `10–14px` gaps.

Do not increase tag size simply to fill width.

## Tag visual states

### Idle

Keep:

- warm-white fill;
- 1px neutral border;
- near-black text;
- small `4–8px` radius;
- no shadow.

### Selected

Use:

- near-black fill;
- warm-white text;
- same geometry;
- optional restrained check mark only if needed.

Do not use semantic colors.

### Maximum-selection behavior

When 3 tags are selected:

- selected tags remain selected;
- unselected tags may remain visually available but further selection must not exceed 3;
- do not hide tags;
- do not recolor unavailable tags red;
- use accessible disabled/interaction semantics if implementation prevents selecting a fourth.

---

# Navigation state

The current empty-state screenshot is correct:

```text
BACK = enabled
CONTINUE = disabled
```

Once at least one tag is selected:

```text
CONTINUE = enabled
```

Use the shared Reflection navigation states from file `42`.

Do not move either navigation control when enabled/disabled.

Do not require all 3 tags; `1–3` selections are valid.

---

# Layout and whitespace

Preserve the reviewed hierarchy:

```text
progress

main heading
supporting line

normalized comparison grid

experience-feeling question
helper line
balanced tag group

large quiet whitespace

BACK / CONTINUE
```

The comparison grid should remain the densest element on R_01.

Do not add:

- an outer card around the whole screen;
- a divider between every major section beyond the existing comparison row rules;
- extra explanatory paragraphs;
- letter thumbnails;
- console icons;
- system labels;
- colored accents.

---

# Regression requirements

Changes made for R_01 must not alter:

- Reflection stage background;
- progress anchor;
- navigation anchors;
- Reflection type system;
- absence of console chrome;
- 1440 × 1080 stage geometry.

Do not alter Console 1 or Console 2 components while calibrating Reflection.

---

# Final R_01 acceptance

R_01 is visually locked when:

- screenshot is exactly `1440 × 1080`;
- comparison grid remains equal-weight and neutral;
- normalized values come from data/fixture mapping rather than hard-coded presentation text;
- `choose up to 3` appears quietly beneath the experience question;
- tags wrap into a visually balanced centered group at canonical resolution;
- zero selected -> CONTINUE disabled;
- one selected -> CONTINUE enabled;
- up to three tags can be selected;
- a fourth cannot be added;
- selected tags use black fill + warm-white text;
- BACK remains enabled;
- Reflection foundation geometry remains unchanged;
- no Arcade 1 or Arcade 2 visual language appears.

## Next gate

After the selected-tag screenshot is reviewed and the above behavior passes, R_01 may be treated as locked.

Then Codex may proceed to `R_02` only.

Do not implement `R_03`–`R_05` in the same task.
