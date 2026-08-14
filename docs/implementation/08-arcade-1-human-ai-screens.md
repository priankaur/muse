# 08 — Arcade 1: Human + AI Screen Specifications

Arcade 1 is the human-led path. The visitor starts with their own emotional material; the machine supports that material rather than replacing it.

All screens use the locked MUSE shell unless noted otherwise.

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

Either red button may start in the final hardware implementation. Static build also allows click/Enter.

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

Use the canonical wide magenta CTA.

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

Validation should use the same pixel language and should not shake/animate in the static phase.

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

### Static phase

No camera permission. CTA advances to the simulated capture screen.

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

- accept → `A1_07`
- retake → increment attempt and return `A1_05`

---

## `A1_07` — Notes for the machine

### Goal

Allow a short correction/addition before AI enhancement.

### UI

- one clear prompt,
- text field/textarea that visually belongs to the pixel system,
- character counter.

Legacy cap: 120 characters. Keep as configuration so it can change.

### CTA

Continue to tuning.

---

## `A1_08` — Tune the enhancement

### Goal

Let the visitor use AI as an adjustable tool after the human work exists.

### Interaction

One parameter is active at a time. The gold rotary dial eventually adjusts it. Static build uses arrow keys/click controls but preserves the dial-like visual grammar.

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

### Static phase

No real AI call and no animation requirement. Render a completed/static progress state and a continue mechanism or short deterministic timeout only if useful for flow testing.

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
- machine note,
- tuning settings,
- Human + AI result.
