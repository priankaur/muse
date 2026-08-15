# 31 — Arcade Console 2 / AI Only — A2_01 Visual Calibration

This file records the visual review of the current `A2_01` screenshot after the exhibition-continuation copy from file `27` was implemented.

It is the latest visual authority for `A2_01`. Where it conflicts with the earlier A2_01 geometry in file `22`, this calibration wins. File `27` remains the latest copy authority.

## Review status

The overall A2_01 composition is **approved as the baseline direction**, with only small readability calibration required before moving to `A2_02`.

The following are now locked:

- warm off-white main field;
- persistent small top-left `MUSE / AI ONLY / ARCADE CONSOLE 2` identity in the same anchor as A2_00;
- no oversized hero `MUSE` on A2_01;
- centered two-line exhibition-continuation title;
- centered supporting line;
- large centered rectangular prompt field;
- character counter inside the prompt field at bottom-right;
- fixed lower physical-control deck;
- BACK enabled/black;
- NEXT visible but disabled/grey while prompt is empty;
- intensity dial visible but inactive;
- no floating Back/Continue links;
- no Console 1 chrome;
- no dominant blue;
- no bottom-center MUSE wordmark.

## Title

Current title is approved:

```text
you've shaped a love letter with AI.
now see what AI creates on its own.
```

Preserve the deliberate two-line composition at the canonical 1440×1080 stage.

Rules:

- neutral Swiss/neo-grotesk content/display face;
- regular/medium weight rather than the heavy condensed A2_00 hero role;
- near-black;
- centered;
- large but not poster-dominant;
- do not add the giant A2_00 `MUSE` title here;
- do not uppercase the sentence;
- do not shrink simply to create more whitespace.

The current title scale and line break are accepted as the baseline.

## Supporting line

Current copy remains:

```text
give it one short direction. it will generate the rest.
```

The current placement is approved, but the screenshot shows the supporting line close to the lower end of acceptable contrast.

Final calibration:

- keep approximately 16–18px at 1440×1080;
- use the shared muted-ink token but ensure practical readability;
- do not render lighter than approximately `#777777` against the warm off-white field unless measured contrast is still acceptable;
- keep regular weight;
- no red emphasis;
- no additional explanatory paragraph.

Do not move the subtitle significantly closer to the title or prompt field.

## Prompt field

The prompt-field geometry is approved.

Lock the following character:

- centered in the main content region;
- wide horizontal rectangle;
- low/zero radius;
- transparent/warm-off-white interior;
- thin neutral grey outline;
- no shadow;
- no blue focus ring;
- no modern floating-label treatment.

Starting dimensions remain approximately:

```text
width: 720px
height: 190px
```

The current screenshot proportions are acceptable.

### Border calibration

Idle border may remain light, but it must remain visible on exhibition hardware.

Recommended:

- idle: shared neutral line around `#B8B8B8`–`#BDBDBD`;
- focus: near-black/darker neutral line;
- optional tiny signal-red focus detail only if already supported by the shared component;
- no glow.

Do not add a red border around the full field.

## Placeholder

Current placeholder remains the configured fixture from file `27` unless the user explicitly changes the copy.

Visual rule:

- regular neutral sans, not bold;
- approximately 16–18px;
- muted grey;
- line-height sufficient for two lines;
- top-left within field with existing padding;
- do not make placeholder text compete with entered user text.

If the browser default placeholder styling is producing semibold/bold appearance, override it explicitly.

## Character counter

The screenshot's `0 / 120` placement is approved but its contrast is too faint to become the final baseline.

Keep:

- bottom-right inside prompt field;
- system/mono role;
- approximately 13–14px;
- no surrounding badge/background.

Increase legibility slightly:

- use the shared muted/system text token at a readable contrast;
- target approximately `#777777`–`#858585` rather than an extremely pale grey;
- do not make the counter near-black unless the user approaches the limit.

Optional future state behavior is allowed only if implemented consistently:

- normal: muted grey;
- near limit: stronger black or small signal-red detail;
- at limit: restrained signal-red text/marker.

Do not implement a large warning state in this calibration pass.

## Red signal language

A2_01 does **not** require an always-visible red square marker in the main content region.

The sparse system language is preserved through the shared control deck and signal-red dial pointer.

Do not add decorative red markers simply for consistency with A2_00.

If the prompt field later uses a red signal marker for focus/limit state, it must be state-driven and small.

## Whitespace

The large open region below the prompt field and above the deck is intentional.

Do not fill it with:

- instructions;
- examples outside the textarea;
- AI status graphics;
- progress UI;
- decorative rules;
- icons;
- helper cards.

A2_01 should remain quieter than A2_00 and let the prompt field be the sole active content object.

## Control deck state

Keep deck geometry pixel-identical to locked A2_00.

On empty prompt:

- BACK: active / near-black;
- NEXT: disabled / grey;
- intensity dial: inactive, geometry unchanged.

When `prompt.trim().length > 0`:

- NEXT changes to the approved active black state;
- do not alter the button's position, size or label;
- dial remains inactive.

Do not duplicate navigation with floating text links.

## Content note — placeholder pronoun

The current placeholder contains a gendered pronoun (`she`). This file does **not** change it automatically because the user has not explicitly requested a placeholder-copy revision.

If recipient gender is not guaranteed by session data, prefer a neutral/contextual placeholder in a later copy pass rather than displaying a mismatched pronoun. Keep this as a content-layer change, not a layout change.

## A2_01 acceptance checklist

Before moving to A2_02, verify:

- stage remains exactly 1440×1080;
- A2_00 regression screenshot remains unchanged;
- A2_01 title uses the current exhibition-continuation copy from file `27`;
- title remains two lines and centered;
- no giant A2_00 MUSE hero appears;
- subtitle is readable and not excessively faint;
- prompt field geometry matches the approved screenshot;
- placeholder is regular weight;
- character counter is readable and remains bottom-right;
- BACK is active;
- NEXT is disabled with empty prompt and active with valid prompt;
- dial remains inactive;
- no duplicate software Back/Continue actions;
- no added decorative UI;
- no dominant blue;
- no Console 1 styling.

## Next gate

After the small subtitle/counter readability calibration and interaction-state verification pass, `A2_01` may be considered visually locked.

Then proceed to `Task E — A2_02 interpretation + tone controls` from file `24` **only**.

Do not implement A2_03 in the same uncontrolled pass.
