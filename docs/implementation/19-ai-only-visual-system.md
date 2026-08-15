# 19 — Arcade Console 2 / AI Only — Visual System Specification

This file defines the current Console 2 visual system. It is intentionally prescriptive. Do not improvise a generic minimal dashboard.

## Canonical references

Use both:

- `docs/reference/ai-only-console2-canonical.jpg` — four-screen composition/content reference.
- `docs/reference/ai-only-console2-system-refinement-v2.jpg` — latest system/chrome refinement and higher authority for typography character, palette emphasis, separators, red markers, and the lower control deck.

When the two references conflict, refinement-v2 wins for visual system/chrome.

---

## 1. Design character

Console 2 should feel like a museum-grade computational instrument: editorial, precise, sparse, technical and quiet.

Keywords:

- editorial
- technical
- computational
- restrained
- industrial
- typographic
- precise
- highly legible
- unemotional
- system-driven

It is **not**:

- a SaaS dashboard
- a futuristic AI interface
- glassmorphism
- glossy Apple-style UI
- cyberpunk / terminal UI
- brutalist novelty UI
- retro pixel computing
- Console 1 arcade styling

The interface should gain structure from typography, whitespace, rules and physical-control geometry — not decorative panels.

---

## 2. Stage geometry

Internal stage is always:

```css
--stage-width: 1440px;
--stage-height: 1080px;
```

Scale the complete stage as one unit:

```ts
scale = Math.min(viewportWidth / 1440, viewportHeight / 1080)
```

Do not reflow major regions responsively.

### Main vertical regions

Use two persistent regions:

```text
MAIN CONTENT REGION   y = 0 .. 888
CONTROL DECK          y = 888 .. 1080
```

The exact divider may be calibrated ±8px from screenshot comparison, but it must be a shared token and must not vary per screen.

Recommended tokens:

```css
--ai-deck-height: 192px;
--ai-deck-top: 888px;
```

---

## 3. Outer stage treatment

Console 2 should not read as a giant rounded app card.

Rules:

- no large outer stage radius
- no drop shadow around the full stage
- no card elevation
- no glass panel
- stage fills the canonical 1440×1080 composition

A subtle perimeter/hairline may remain if required by the original four-screen reference, but the stronger visual structure now comes from the horizontal rule separating content and controls.

If an inset perimeter frame is retained:

```css
--ai-frame-inset: 20px;
--ai-frame-border: 1px;
--ai-frame-radius: 4px; /* max; may be 0 after calibration */
```

Do not use an 8–16px app-like outer corner radius.

---

## 4. Current color system

The latest refinement shifts Console 2 away from blue. The primary palette is **black / grey / off-white / signal red**.

Starting production tokens:

```css
:root {
  --ai-bg: #F7F6F2;
  --ai-surface: #F2F1ED;
  --ai-deck-bg: #EAEAEA;

  --ai-ink: #090909;
  --ai-ink-secondary: #454545;
  --ai-ink-muted: #8A8A8A;

  --ai-line-strong: #111111;
  --ai-line: #BDBDBD;
  --ai-line-soft: #D9D9D9;

  --ai-signal: #EC5B29;
  --ai-signal-dark: #C94A20;
  --ai-signal-faint: #F3C3B2;
}
```

`#EC5B29` is sampled from the latest refinement reference and should be treated as the Console 2 **signal red** even though it has a warm/orange-red character.

### Color discipline

- Main field stays warm off-white, not bright blue-white.
- Control deck is a neutral light grey distinct from the main field.
- Main typography is near-black.
- Secondary system metadata is mid/muted grey.
- Strong separators are near-black.
- Red appears only in micro-signals, dial indicator, active state accents and very small markers.
- Do not create large red buttons or red panels.
- Do not restore periwinkle/blue as the default action color.
- Sentiment/emotion/romance remain monochrome; do not semantic-color them green/pink/etc.

If calibration changes a value, update the token globally rather than patching individual screens.

---

## 5. Typography system

Console 2 now uses **three typographic roles**.

### A. Display / title role

Character:

- heavy condensed neo-grotesk
- bold black mass
- tall, compact letterforms
- tight line spacing
- editorial poster character
- no rounded/friendly geometric styling

Preferred open-source implementation:

```css
font-family: "Roboto Condensed", "Arial Narrow", "Liberation Sans Narrow", Arial, sans-serif;
font-weight: 700;
```

Bundle locally if possible. No runtime network dependency.

This role is visually inspired by the `DIGITAL LOVE LETTER` headline in refinement-v2.

Important: the user request is about **weight/character**, not blindly copying the exact wording, position or scale of the reference headline.

When `MUSE` appears as the persistent identity title, its `MUSE` line should use this heavy condensed character. Do not add the bottom-center `MUSE` wordmark from the reference.

### B. Neutral content role

For body copy, prompts, analysis summaries and letter text:

```css
font-family: "Liberation Sans", Arial, "Helvetica Neue", Helvetica, sans-serif;
font-weight: 400;
```

### C. System metadata/control role

For system status, small labels, control labels and compact technical microcopy, use a restrained mono/semi-mono character:

```css
font-family: "Liberation Mono", "Courier New", monospace;
font-weight: 400;
```

Do not use mono for the entire interface.

### Font size roles

Starting 1440×1080 values:

```css
--ai-font-display-xl: 92px;
--ai-line-display-xl: 0.88;
--ai-font-display-lg: 64px;
--ai-line-display-lg: 0.94;
--ai-font-screen-title: 48px;
--ai-line-screen-title: 1.0;
--ai-font-section: 20px;
--ai-font-body: 18px;
--ai-line-body: 1.42;
--ai-font-control: 14px;
--ai-font-small: 13px;
--ai-font-micro: 12px;
```

Use the heavy display role selectively. Do not make every sentence poster-sized.

---

## 6. Persistent identity

Component: `AiOnlyIdentity`

Anchor:

```text
x = 72
y = 58
```

Structure:

```text
MUSE
AI ONLY
ARCADE CONSOLE 2
```

Current recommended styling:

- `MUSE`: 30–34px, heavy condensed, 700, near-black
- `AI ONLY`: 12px system/content label, muted grey
- `ARCADE CONSOLE 2`: 12px, semibold/stronger black
- compact vertical spacing

The `MUSE` line must feel significantly bolder than before.

Do not:

- add a heart/icon
- add a badge background
- add a screen number
- move identity into a bar
- add `MUSE` again at bottom center

---

## 7. Red square marker system

Component: `SignalMarker`

A small filled red square is the primary micro-accent anchor.

Recommended geometry:

```css
--ai-marker-size: 8px;
```

Allow 6–10px depending on context.

Use before:

- system status microcopy
- control/deck metadata
- selected technical state labels where reference evidence supports it
- optional IDs/status fields

Do not use it:

- before every paragraph
- as a bullet list decoration everywhere
- as a large logo
- as a background pattern

The marker is a signal, not decoration.

---

## 8. Rules and separators

Linework is a core part of the refined visual system.

Components/tokens:

```css
--ai-rule-strong-width: 2px;
--ai-rule-hairline-width: 1px;
```

### Strong horizontal deck separator

At approximately `y = 888`:

- full stage width
- 2px near-black
- no shadow
- no gradient

### Internal separators

Use 1px neutral/black rules for:

- section boundaries where needed
- analysis/tone grouping when the original four-screen composition benefits from added structure
- metadata alignment
- input baselines or content grouping

Do not draw arbitrary boxes around every content block.

---

## 9. Lower physical-control deck

Component: `AiControlDeck`

Persistent region:

```text
x: 0
y: 888
width: 1440
height: 192
background: --ai-deck-bg
```

Top border:

```text
2px near-black horizontal rule
```

The deck must be visually quiet and physical, not a software toolbar.

### Left button cluster

Two outlined circular arcade buttons:

```text
BACK    NEXT
```

Recommended centers:

```text
BACK center: x ~82, y ~972
NEXT center: x ~184, y ~972
```

Button visual diameter:

```text
72–78px
```

Button construction:

- off-white/very-light face
- black outer circular stroke 4px
- black inner ring 2px
- slight neutral-grey inner line if useful
- no glossy 3D rendering
- no pixel art
- no colored fill
- no drop shadow

Labels under buttons:

- `BACK`, `NEXT`
- system/mono role
- uppercase
- ~13px
- letter-spacing ~0.14–0.18em
- near-black

Static web prototype: button drawings can be actual `<button>` elements with circular visual layers.

### Right intensity dial

Recommended center:

```text
x ~1324
y ~966
```

Diameter:

```text
96–108px
```

Construction:

- off-white face
- thick black outer ring ~4–5px
- thin grey inner ring
- subtle inset circle
- restrained red pointer/tick/wedge at lower-right quadrant
- no gold
- no pixel extrusion
- no glossy chrome

Label:

```text
INTENSITY DIAL
```

- uppercase system/mono role
- ~13px
- tracked
- centered below dial

### Bottom-center rule

Do **not** render `MUSE` in the center of the deck.

That element exists only in the refinement reference and is explicitly excluded from production.

---

## 10. Navigation semantics after control-deck refinement

The earlier floating `← back` / `continue →` links are superseded as the **primary persistent navigation representation**.

Preserve the navigation semantics, but express Back/Next primarily through the physical deck buttons.

Mapping:

- `BACK` button = semantic back action where available
- `NEXT` button = begin/continue action where available
- `INTENSITY DIAL` = tone/intensity adjustment when the active screen has adjustable controls

For screens where an action is unavailable:

- keep physical hardware visible for consistency
- disabled control should remain visually present but reduced to a neutral inactive state
- do not remove the whole deck or reflow it

`REGENERATE` has no dedicated reference hardware button. On `A2_03`, keep it as a minimal text/system action above the deck or in the content action row, unless later hardware mapping is explicitly defined.

Do not duplicate Back/Next with floating arrow links and deck buttons simultaneously unless a screen-specific approved reference requires both.

---

## 11. Input field / textarea

Component: `AiPromptField`

Reference character:

- off-white/transparent field
- 1px neutral-grey or near-black border
- rectangular
- low radius 0–4px preferred in refined system
- no floating label
- character count bottom-right

Current cap:

```text
120 characters
```

Canonical dimensions remain:

```text
width: 720px
height: 190px
padding: 24px 22px
```

Focus:

- line/border darkens or receives a tiny red marker accent
- no glow
- no blue outline

---

## 12. Analysis cards

Used for sentiment, emotion and romance.

Keep original content geometry but make the styling more editorial/technical:

```text
width ~500px
height >=112px
gap 16px
```

Treatment:

- off-white background / transparent
- 1px neutral rule
- 0–4px radius
- no shadow
- black/grey typography
- tiny red square or line marker may anchor the card label
- monochrome custom line icons if retained

Do not use blue icons.

---

## 13. Tone controls

Five controls, in order:

1. warmth
2. intimacy
3. emotional depth
4. playfulness
5. nostalgia

Row geometry remains:

```text
row height: 64px
label column: 180px
slider: 240px
value column: 72px
```

Slider:

- 2px track
- inactive grey
- active section near-black or signal red only when focused/active
- 14px outlined thumb
- off-white center
- no blue
- no shadow

The right-side physical dial visually reinforces the tuning concept; it does not replace accessible native range inputs in the static browser build.

---

## 14. Insight rail

Result-screen insight rail keeps four categories:

1. sentiment
2. emotion
3. romance
4. tone profile

Styling:

- thin neutral rules
- low/no radius
- no shadow
- black labels
- key values can use strong black with a small red marker, not blue text
- confidence stays muted grey

Do not semantic-color categories.

---

## 15. Letter document

The letter remains the dominant visual object.

Main sheet:

```text
width: 760px
height: ~520px minimum
padding: 54px 64px
```

Use:

- warm/off-white sheet
- thin grey/black outline
- 1–2 restrained offset outline layers
- subtle shadow only if necessary to preserve physical-sheet depth

Typed content:

- neutral sans
- 17–18px
- line-height 1.42
- near-black

No handwriting/stamps/doodles/color decoration in current build.

---

## 16. Whitespace discipline

Whitespace remains a primary design element.

The new rules/separators are structural. They do **not** justify filling empty regions with UI.

Do not add:

- helper cards
- progress bars
- AI sparkle graphics
- background shapes
- pseudo-data displays
- decorative line grids

---

## 17. No motion in first build

No:

- entry animations
- page transitions
- blinking/pulsing markers
- animated sliders
- loading-dot spectacle
- moving dial animation

The visual controls may change state instantly.

---

## 18. Anti-drift checklist

Reject the implementation if any of these occur:

- blue returns as dominant accent
- red becomes a large decorative surface
- bottom-center `MUSE` is copied from refinement reference
- controls become Console 1 red/gold pixel hardware
- main stage becomes a rounded app card
- cards gain modern heavy shadows
- buttons become pill UI
- headline becomes geometric/friendly rather than condensed neo-grotesk
- every screen invents different linework
- the control deck changes position/height between screens
- Back/Next are duplicated unnecessarily as both floating links and physical deck controls
- generic component-library defaults determine radius/spacing
- content density grows to fill intentional whitespace

---

## 19. Calibration rule

The images are visual targets, not assets to copy literally.

During visual regression:

1. calibrate stage/background/deck split,
2. calibrate display typography,
3. calibrate deck button/dial geometry,
4. calibrate rules and red marker scale,
5. calibrate screen-specific content layout from the original four-screen reference.

Change shared tokens first. Do not create screen-specific patches to compensate for a wrong system token.