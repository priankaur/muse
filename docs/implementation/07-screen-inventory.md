# 07 — Canonical Screen Inventory

This is the working complete screen map for the static build. Copy labels may change; screen responsibilities should remain stable unless the product flow changes explicitly.

## Registration / entry

### `REG_01` — Registration handoff

Purpose: represent/receive visitor identity from the phone registration step.

Static build: fixture-driven registration confirmation; no backend required.

Output:

- visitor ID
- first name
- optional demographic context used by the project

Next: `A1_00`.

---

# Arcade 1 — Human + AI

### `A1_00` — Attract / Discover Your Muse

Purpose: idle/start state for Arcade 1.

Visual: hero title treatment in locked shell.

### `A1_01` — Welcome / Hello [User Name]

Purpose: explain the value of slowing down and writing to someone you love.

CTA: `WRITE A LETTER TO SOMEONE YOU LOVE`.

### `A1_02` — Recipient + relationship

Purpose: collect recipient name and relationship.

Fields/options match the approved form reference.

### `A1_03` — Human writing prompt

Purpose: ask visitor to begin with their own words/materials. Provide concise thought starters and physical-making instructions.

### `A1_04` — Ready to capture

Purpose: explain the three-photo constraint and position/capture process.

### `A1_05` — Photo capture

Purpose: static camera placeholder; show capture guide and `PHOTO N / 3` state.

### `A1_06` — Photo review

Purpose: choose `USE THIS ONE` or `RETAKE`. Third attempt removes retake.

### `A1_07` — Notes for AI

Purpose: optional short machine note (legacy cap was 120 characters).

### `A1_08` — Tune the enhancement

Purpose: Human + AI tuning controls. Same physical-dial interaction grammar that can later be reused in Arcade 2.

### `A1_09` — Processing

Purpose: static generating/processing state using fixture delay or immediate continue in development.

### `A1_10` — Human + AI letter result

Purpose: display enhanced letter, retaining human-specific content.

### `A1_11` — Handoff to Arcade 2

Purpose: conclude first experience and direct visitor to the AI-only console while preserving session context.

---

# Arcade 2 — AI-only

### `A2_00` — Welcome back

Purpose: identify the visitor from the inherited session. Do not repeat registration/recipient questions.

### `A2_01` — Short prompt

Purpose: collect the short prompt the visitor wants the AI-only system to use.

### `A2_02` — Machine analysis

Purpose: show sentiment, emotion and romantic-intent detection as part of the AI-only experience.

Static build: fixture analysis only.

### `A2_03` — Intensity controls

Purpose: adjust the AI-only generation parameters using the rotary-dial grammar.

Exact copy/labels remain content-configurable and must not be hard-coded into component styling.

### `A2_04` — AI-only generating

Purpose: machine-led generation state.

### `A2_05` — AI-only letter result

Purpose: show the AI-only letter for later comparison.

The tone should not be cartoonishly robotic. The intended experience is competent but noticeably less human/soulful than the Human + AI result.

---

# Reflection / comparison / choice

### `R_01` — Which one sounds like you?

Options from legacy flow can be retained as content configuration.

### `R_02` — What did you feel?

Multi-select emotional response.

### `R_03` — Was the difference worth it?

Effort/value reflection.

### `R_04` — What did the machine get wrong?

Typed answer aimed at the machine rather than judging the visitor.

### `R_05` — Next time I want to say something that matters, I’ll…

Typed completion.

### `R_06` — Which letter would you send?

Side-by-side Human + AI and AI-only letters.

### `R_07` — Your stance

Three equal choices:

- Convenience
- Control
- More Human

No visual ranking or moral hierarchy.

### `R_08` — Print / token wall / exit handoff

Static build: represent that the chosen artifact would be printed and that the visitor should complete the physical token-wall ritual.

No printer integration yet.

## Implementation note

This inventory intentionally separates conceptual screen responsibilities from copy. If the user later combines two screens or splits one into multiple screens, update this file and the registry together rather than patching navigation ad hoc.
