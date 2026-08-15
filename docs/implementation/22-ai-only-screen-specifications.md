# 22 — Arcade Console 2 / AI Only — Screen Specifications

This document defines the four canonical AI-only screens at `1440 × 1080` using the current refined Console 2 visual system.

Visual references:

- `docs/reference/ai-only-console2-canonical.jpg` — content composition / four-screen flow.
- `docs/reference/ai-only-console2-system-refinement-v2.jpg` — current typography, black/grey/off-white/red system language, rules, markers and lower control deck.

If these references conflict, use the refinement image for system/chrome and the original four-screen image for screen-specific content layout.

All screens use `AiOnlyShell`, `AiOnlyIdentity`, `SystemRule` and `AiControlDeck`.

Do not render tiny screen numbers.
Do not render a bottom-center `MUSE` label.
Do not render Console 1 pixel chrome.

---

# Shared 1440×1080 structure

## Stage

```text
width: 1440
height: 1080
```

## Main content region

```text
y: 0–888
```

## Lower control deck

```text
y: 888–1080
height: 192
background: #EAEAEA starting token
```

A 2px near-black horizontal rule separates the content region from the deck.

## Persistent identity

Anchor:

```text
x: 72
y: 58
```

```text
MUSE
AI ONLY
ARCADE CONSOLE 2
```

`MUSE` uses the heavy condensed display character from the refinement reference. It must be noticeably bolder than the earlier foundation implementation.

Do not copy the reference's bottom `M U S E` treatment.

## Persistent deck controls

### BACK button

Approx center:

```text
x: 82
y: 972
```

### NEXT button

Approx center:

```text
x: 184
y: 972
```

### INTENSITY DIAL

Approx center:

```text
x: 1324
y: 966
```

All three controls remain physically visible across the AI-only flow. Availability changes by state; geometry does not.

Back/Next navigation is expressed primarily through these physical deck controls rather than duplicate floating arrow links.

`regenerate` remains a small software/system action on `A2_03` because there is no dedicated fourth hardware control.

---

# Shared style rules

## Palette

Dominant system:

- warm off-white main field
- light grey control deck
- near-black primary typography
- muted grey system metadata
- signal red `#EC5B29` for tiny square markers / dial pointer / active technical state

Do not use periwinkle/blue as the default accent.

## Typography

Use three roles:

1. heavy condensed neo-grotesk for `MUSE` identity and strong display titles where specified,
2. neutral Swiss/neo-grotesk for content,
3. mono/semi-mono technical face for system labels, control labels and metadata.

Do not make every paragraph condensed/bold.

## Rules / separators

Use shared `SystemRule` components/tokens. Do not invent one-off border thicknesses per screen.

The control-deck separator is the strongest persistent rule. Internal content separators are 1px and used sparingly.

## Red markers

Use small red squares as system anchors only where helpful. Do not place one before every text element.

---

# `A2_00` — Welcome Back / Context Loaded

## Purpose

Acknowledge that Console 2 already knows the visitor and has inherited context from Arcade 1.

It must not feel like onboarding again.

## Required content

Config shape:

```ts
{
  titlePrefix: 'welcome back,',
  contextLine: 'your context from the first experience has been loaded.',
  beginInstruction: 'PRESS [NEXT] TO BEGIN'
}
```

Visitor name is dynamic.

Do not copy `SYSTEM INITIALIZED // MUSE OS v.1.0` literally unless later approved as product copy. The refinement reference defines the **style** of system-status microcopy, not the exact words.

## Composition

### Identity

Persistent top-left identity as defined above.

### Hero block

Use the original four-screen reference's central balance, but strengthen typographic character.

Approximate content box:

```text
x: 320
width: 800
start y: 230
```

Title:

```text
welcome back,
[visitor name]
```

- 62–66px
- neutral/content display role
- near-black
- centered
- line-height ~0.98
- no blue name

Do not automatically make this title uppercase. The heavy condensed uppercase treatment is a system/display option, not a reason to rewrite approved copy.

### Context line

```text
y: ~410
width: 520
```

- 17–18px
- muted grey
- centered
- maximum 2 lines

### Context signal

```text
center x: 720
center y: ~565
diameter: 170–185px
```

- static neutral dotted/radial structure
- tiny red central signal marker
- no blue
- no animation

### Begin instruction

Place as restrained technical microcopy in the lower portion of the main content region, above the deck, aligned intentionally with the system grid.

Recommended:

```text
x: 76
y: 840
```

Structure:

```text
[red square]  PRESS [NEXT] TO BEGIN
```

- mono/system role
- uppercase
- 13–15px
- near-black

The deck NEXT button triggers the action.

## Deck state

- BACK: visible but disabled/neutral
- NEXT: enabled, triggers `A2_01`
- dial: visible, inactive/neutral

No duplicate centered `press to begin` button is required once the deck pattern is implemented.

---

# `A2_01` — Short Prompt

## Purpose

Ask for one short direction that guides the AI-generated letter without recreating the Human + AI writing task.

## Default content

```ts
{
  title: 'what would you like\nAI to focus on?',
  subtitle: 'give AI a short prompt to guide the letter.',
  placeholder: 'example: help me apologize for being distant lately\nand express how much she means to me.',
  maxLength: 120
}
```

Copy remains configurable.

## Composition

### Title

Centered in main content region:

```text
x: 350
width: 740
y: 190–215
```

- 48–52px neutral/screen title role
- near-black
- line-height ~1.0
- exactly two lines at canonical copy length

A thin structural rule may sit beneath the title/subtitle group if it improves alignment with refinement-v2. Use shared rule token, not a decorative line.

### Subtitle

```text
y: ~330
```

- 16px
- muted grey
- centered

### Prompt field

```text
x: 360
width: 720
height: 190
y: 400–420
```

Treatment:

- off-white / transparent field
- 1px grey/black line
- radius 0–4px
- no blue outline
- 24px horizontal padding
- 22px vertical padding

Character count:

```text
0 / 120
```

- bottom-right
- 13–14px muted/system grey

Focus:

- border darkens and/or receives a tiny red signal detail
- no glow

## Deck state

- BACK: enabled -> `A2_00`
- NEXT: enabled only when `prompt.trim().length > 0`
- dial: visible, inactive

Do not render additional floating `← back` / `continue →` links.

---

# `A2_02` — Interpretation + Tone Controls

## Purpose

Expose the machine's read-only interpretation and allow the visitor to tune the AI-proposed generation parameters.

## Title

Default:

```text
here’s what I understand.
```

Position:

```text
x: 300
width: 840
y: 120–145
```

- 44–48px
- near-black
- centered

Optional shared horizontal rule can separate title from the analytical grid if visually consistent with refinement-v2.

## Main grid

```text
container x: 155–170
container width: 1110
top: 250–275
left column width: 500
column gap: 140
right column width: 460
```

### Left heading

```text
analysis
```

- 17–18px semibold
- near-black
- may use a small red square marker before the heading

### Analysis stack

Exactly three read-only cards:

1. sentiment analysis
2. emotion detection
3. romance detection

Approximate:

```text
width: 500
height: 108–112
gap: 14–16
```

Current visual treatment:

- no blue
- thin grey/black outline/rules
- radius 0–4px
- no shadow
- black label
- muted summary
- tiny red marker or monochrome icon only

Fixture values can remain:

```text
sentiment analysis  62 / 100
emotion detection   71 / 100
romance detection   68 / 100
```

These are static fixture readouts, not diagnostic truth.

### Right heading

```text
tone controls
```

- 17–18px semibold
- near-black
- optional red marker

### Tone controls

Exactly five rows, in order:

```text
warmth             72%
intimacy           68%
emotional depth    70%
playfulness        40%
nostalgia          55%
```

Slider rules:

- grey inactive track
- black active track by default
- signal red only for focused/active control if needed
- off-white outlined thumb
- no blue
- no shadow

## Dial behaviour in static prototype

The visible `INTENSITY DIAL` can mirror/drive the currently focused tone control.

Requirements:

- do not create a new sixth value
- dial changes the active/focused tone-control value only
- keyboard/mouse range controls remain accessible
- if no tone row is focused/selected, dial does not silently modify an arbitrary control

## Deck state

- BACK: enabled -> `A2_01`
- NEXT: enabled -> `A2_03`
- dial: enabled for the active tone control

---

# `A2_03` — Generated AI Letter + Insights

## Purpose

Present the AI-only generated letter as the dominant object and show machine insight alongside it.

This is the final Console 2 screen before shared reflection.

## Result composition

Main content region must fit above the control deck.

Recommended grid:

```text
container x: 185–205
container y: 165–190
container width: 1100
columns: 770px 250px
gap: 70–80px
```

The letter must remain visually dominant.

## Letter document

Main sheet:

```text
width: 750–770px
height: 500–520px
```

Use:

- warm off-white paper
- thin grey/black outline
- 1–2 offset outline layers
- restrained shadow only if required

Body:

- 17–18px neutral sans
- line-height 1.42
- left aligned
- near-black

No handwriting, stamps, doodles or colored decoration in the current build.

## Letter insights

Exactly four categories:

1. sentiment
2. emotion
3. romance
4. tone profile

Use:

- black labels
- muted grey confidence text
- strong black key values
- tiny red signal marker / monochrome icon where useful
- no blue values
- no semantic green/pink/red category coding

## Regenerate action

Because the deck has no fourth hardware button, display a restrained text/system action above the deck or centered beneath the result content:

```text
[red marker optional] REGENERATE
```

Do not style it as a large CTA.

Regenerate:

- stays on `A2_03`
- preserves inherited context
- preserves prompt
- preserves analysis
- preserves current tone-control values
- cycles deterministic result variant + matching insights

## Deck state

- BACK: enabled -> `A2_02`
- NEXT: enabled -> shared reflection first screen
- dial: visible, inactive/neutral unless later explicitly assigned

No duplicate floating continue link.

---

# Cross-screen invariants

## Control deck

The deck is pixel-identical in geometry across all four screens.

Only control enabled/disabled/indicator state may change.

## Identity

Top-left identity never moves.

## No bottom MUSE

Never render the bottom-center `MUSE` from the refinement reference.

## Accent

Signal red is sparse. If red becomes visually dominant, the implementation has drifted.

## Lines

Rules should align to shared system coordinates. Do not create random decorative linework per screen.

## Whitespace

The refined system adds structure, not density. Preserve large open regions.

## Content overflow

If copy becomes longer:

1. preserve stage/deck geometry,
2. preserve identity/control anchors,
3. allow controlled wrapping,
4. request design review before materially shrinking titles or letter body.

---

# Static transition map

```text
A2_00
  NEXT -> A2_01

A2_01
  BACK -> A2_00
  NEXT(valid prompt) -> A2_02

A2_02
  BACK -> A2_01
  tone edits / dial edits -> remain A2_02
  NEXT -> A2_03

A2_03
  BACK -> A2_02
  REGENERATE -> A2_03 (new deterministic result variant)
  NEXT -> shared reflection first screen
```

---

# Screen approval gate

A screen is not complete until:

- rendered at exactly 1440×1080
- stage-only screenshot captured
- refined reference palette is respected
- no dominant blue appears
- `MUSE` identity uses the heavier condensed character
- control deck divider and hardware geometry match shared tokens
- no bottom-center MUSE exists
- red square markers are sparse and consistent
- no Console 1 pixel chrome appears
- no duplicate floating Back/Next navigation appears
- screen-specific content still follows the original four-screen reference
- tests confirm route/state behavior.