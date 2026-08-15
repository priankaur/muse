# 08 — Arcade 1: Human + AI Screen Specifications

Arcade 1 is the human-led path. The visitor starts with their own emotional material; the machine supports that material rather than replacing it.

All screens use the locked MUSE shell unless noted otherwise.

Arcade 1 now also has an approved motion/sound extension and a new human-letter analysis step. Read files `28`–`30` for the current implementation rules.

## Persistent shell for Arcade 1

- top-left MUSE lockup
- top-right `CONSOLE 1`
- dark navy grid
- sparse love-letter sprites
- sharp-cornered MUSE window
- blank purple title bar
- yellow menu square
- white X square
- pale textured lavender window surface
- red / gold dial / red hardware strip

No control instructions appear beneath the hardware.

The shell geometry remains frozen even when motion is added. Motion affects pressed states, content/page transitions, dial steps and approved sprite bobbing; it does not redesign the shell.

---

## `A1_00` — Attract / Discover Your Muse

### Goal

Invite the visitor into the first arcade experience.

### Content hierarchy

1. small line: `DISCOVER YOUR`
2. large hero word: `MUSE`
3. heart divider
4. concise invitation copy or start CTA depending on final copy direction

### Layout

Use the canonical centered hero composition. `DISCOVER YOUR` should visually span approximately the width of `MUSE`, matching the approved reference treatment.

### Interaction

Either red button may start in the final hardware implementation. Current browser build also allows click/Enter.

Use the shared Arcade 1 button/CTA press feedback and semantic sound event when enabled by file `28`.

### Do not

- introduce long body copy,
- add a separate intro card,
- alter window chrome,
- add extra footer instructions.

---

## `A1_01` — Welcome / Hello [User Name]

### Goal

Set the emotional premise before collecting recipient information.

### Locked title treatment

Large uppercase pixel greeting:

`HELLO, [USER NAME]`

Then the purple heart divider.

### Body copy

Use the current content configuration. The recent approved direction describes writing to someone you love as a way to pause, reflect, observe, and slow down.

The body supports solid rectangular highlight blocks behind selected phrases. Highlight styling is part of the component system, not hard-coded into this screen.

### CTA

`WRITE A LETTER TO SOMEONE YOU LOVE`

Use the canonical wide magenta CTA and the shared CTA press/depth-collapse feedback from file `28`.

### Layout

The greeting sits high enough to avoid the old large blank area. Body copy is centered and comfortably spaced. CTA sits above the bottom content padding, not against the frame.

---

## `A1_02` — Recipient + relationship

This screen has a direct approved visual reference and should receive a visual-regression snapshot.

### Question 1

`WHO DO YOU WISH TO WRITE TO?`

Helper label:

`Recipient Name`

Then one wide text field.

### Separator

Heart-centered horizontal divider.

### Question 2

`WHAT DO THEY MEAN TO YOU?`

Relationship tags:

- Partner
- Crush
- Girlfriend / Boyfriend
- Sibling
- Parent
- Son
- Daughter
- Other

### Other field

When `Other` is selected, allow free-text relationship entry.

### CTA

`CONTINUE`.

### Focus order

1. recipient text field
2. relationship tags in visual order
3. other text field when active
4. continue

### Validation

Require:

- non-empty recipient name,
- selected relationship,
- non-empty other relationship when `Other` is selected.

Validation should use the same pixel language. Do not add modern shaking/bouncing error motion; file `28` governs permitted interaction feedback.

---

## `A1_03` — Human writing prompt

### Goal

Make it explicit that the visitor begins with their own human material.

### Content

Use concise physical instructions based on the current project copy:

- use papers, pens, cutouts and supplied materials,
- think about someone special,
- consider what you love or miss,
- write what you want to say,
- doodle/draw if desired.

Exact wording lives in content config.

### Layout

Do not turn this into a dense instruction manual. Use 2–3 grouped pixel panels or concise columns inside the same window. Preserve breathing room.

### CTA

A concise readiness action such as `I'M READY` or current approved copy.

Do not invent permanent copy if not supplied; use content config fixture.

---

## `A1_04` — Ready to capture

### Goal

Transition from physical making to digitisation.

### Required concept

Visitor gets three capture attempts.

### Content

- short instruction on positioning the letter,
- explicit `3 PHOTOS` constraint,
- camera/capture icon if an approved sprite exists.

### Current prototype phase

No camera permission required yet. CTA advances to the simulated capture screen.

---

## `A1_05` — Photo capture

### Goal

Represent the final camera composition without requiring hardware.

### UI

- large capture guide box centered inside the window,
- demo/placeholder letter image or neutral preview,
- counter `PHOTO 1 / 3`, then 2/3, 3/3,
- primary capture action.

### State

Maintain `photoAttempt` in the session.

### Static capture

Pressing capture selects the fixture image and advances to review.

A semantic capture sound may be added only through the shared Arcade 1 audio layer; do not wire audio directly inside this screen.

---

## `A1_06` — Photo review

### Goal

Allow visitor to accept or retake.

### UI

- large image preview,
- `USE THIS ONE`,
- `RETAKE` when attempts remain.

On attempt 3, `RETAKE` is removed/disabled according to final interaction decision.

### Branching

- accept → `A1_06A`
- retake → increment attempt and return `A1_05`

---

## `A1_06A` — Human letter analysis

### Goal

Show a transparent readback of what the machine recognized from the visitor's human-created letter **before AI enhancement begins**.

This is read-only analysis, not a judgment and not the generated result.

### Required four outputs

Exactly:

1. sentiment analysis;
2. emotions recognized;
3. character count;
4. visual meaning.

### Copy direction

Recommended configurable title:

`HERE'S WHAT THE MACHINE PICKED UP`

Recommended helper:

`A quick read of your letter before AI adds anything to it.`

Store copy in config.

### Layout

Use the locked Arcade 1 shell and pixel component language.

Recommended arrangement:

```text
TITLE / HELPER

[ SENTIMENT ]          [ EMOTIONS RECOGNIZED ]
[ CHARACTER COUNT ]    [ VISUAL MEANING      ]

CONTINUE CTA
```

Use compact pixel panels or equivalent Arcade 1 primitives. Do not copy Console 2's minimal analytics cards.

### Sentiment

Display a concise label such as `warm + reflective`, with optional score if later visually approved.

Do not traffic-light color positive/negative sentiment.

### Emotions recognized

Show a small maximum set, recommended 3 visible emotions, for example:

- love
- nostalgia
- longing

Use Arcade 1 pixel tags or compact list styling.

### Character count

This is the count of the recognized/extracted **human letter text**, not the note-field counter on `A1_07`.

Example:

```text
CHARACTERS RECOGNIZED
384
```

### Visual meaning

This is the machine's qualified interpretation of visible non-text cues such as hearts, doodles, underlines, cutouts, colors, spacing or emphasis.

Example fixture:

```text
heart doodles + emphasized phrases appear to reinforce affection and closeness.
```

Use uncertainty-aware language; do not present visual interpretation as objective psychological fact.

### Interaction

- back → `A1_06` if current semantic navigation supports it;
- continue → `A1_07`.

The visitor cannot directly edit the analysis. `A1_07` gives them the chance to add or correct context before enhancement.

### Data

Use `HumanLetterAnalysis` / fixture service defined in file `29`.

No production vision/OCR/model call is required in the current pass.

---

## `A1_07` — Notes for the machine

### Goal

Allow a short correction/addition after the machine readback and before AI enhancement.

### UI

- one clear prompt,
- text field/textarea that visually belongs to the pixel system,
- character counter.

Legacy cap: 120 characters. Keep as configuration so it can change.

Important: this counter measures the optional machine note and is independent from the recognized human-letter character count shown on `A1_06A`.

### CTA

Continue to tuning.

---

## `A1_08` — Tune the enhancement

### Goal

Let the visitor use AI as an adjustable tool after the human work exists.

### Interaction

One parameter is active at a time. The gold rotary dial eventually adjusts it. Current browser build uses arrow keys/click controls while preserving the dial visual grammar.

The shared motion/audio plan now allows discrete dial rotation and tick sound per detent.

### Legacy parameter set available as a starting fixture

- Warmth
- Playfulness
- Nostalgia
- Boldness
- Length

The exact final names are content configuration, not component code.

### Meter

Use a large pixel meter with discrete steps and low/high labels. Do not use a modern HTML range slider visual.

### CTA

After the final parameter, advance to processing.

---

## `A1_09` — Processing

### Goal

Show the system applying AI support to human material.

### Current motion phase

File `28` now permits a restrained deterministic pixel-processing animation:

- 2–5 stepped progress states;
- no long fake wait;
- no glossy loading spinner;
- optional semantic processing sound.

No real AI call is required in this build.

### Copy tone

Supportive and collaborative, not smug.

---

## `A1_10` — Human + AI result

### Goal

Display the enhanced letter as the first comparison artifact.

### Layout

The letter becomes the dominant content object. Use a readable letter-preview subcomponent inside the same shell.

### Requirements

- preserve recipient name,
- include fixture lines that feel specific/human,
- allow long text to fit without making the system chrome disappear,
- avoid decorative sprites behind the letter body.

If scroll is unavoidable, use an intentional pixel-scroll region; prefer fitting the content for the exhibition copy length.

A short stepped result reveal and semantic completion cue are permitted after core motion/audio review.

### CTA

Continue/handoff.

---

## `A1_11` — Handoff to Arcade 2

### Goal

Close Arcade 1 and tell the visitor to move to Arcade 2.

### State guard

Before completing, verify that `arcade1.enhancedLetter` exists.

### UI

Simple transition screen. Do not introduce a new visual theme.

### Output

The session now contains:

- visitor identity,
- recipient identity,
- relationship,
- human letter image fixture,
- human-letter analysis,
- machine note,
- tuning settings,
- Human + AI result.
