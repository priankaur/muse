# 07 — Canonical Screen Inventory

This is the working complete screen map for the static build. Copy labels may change; screen responsibilities remain stable unless the product flow explicitly changes.

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

Visual: hero title treatment in locked pixel-arcade shell.

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

Purpose: optional short machine note.

### `A1_08` — Tune the enhancement

Purpose: Human + AI tuning controls.

### `A1_09` — Processing

Purpose: static generating/processing state using fixture state.

### `A1_10` — Human + AI letter result

Purpose: display enhanced letter, retaining human-specific content.

### `A1_11` — Handoff to Arcade 2

Purpose: conclude first experience and direct visitor to the AI-only console while preserving session context.

---

# Arcade 2 — AI Only

Console 2 uses its own minimal visual system. See `18`–`24` AI-only plans.

### `A2_00` — Welcome back / context loaded

Purpose: recognize visitor from inherited session and confirm that context from the first experience has been loaded.

No repeated registration, recipient or relationship questions.

### `A2_01` — Short prompt

Purpose: collect one short prompt describing what the visitor wants AI to focus on.

Current cap: 120 characters.

### `A2_02` — AI interpretation + tone controls

Purpose: show machine interpretation and allow visitor adjustment before generation.

Read-only analysis:

- sentiment
- emotion
- romance / romantic intent

Editable AI-proposed tone controls:

- warmth
- intimacy
- emotional depth
- playfulness
- nostalgia

Analysis uses inherited Arcade 1 context + recipient/relationship context + short prompt.

### `A2_03` — AI-only letter + insights

Purpose: display the generated typed AI-only letter plus a right-side insight rail.

Insights:

- sentiment
- emotion
- romance
- tone profile

Actions:

- back
- regenerate in place
- continue to shared reflection

Regenerate preserves prompt, inherited context and tone-control values.

There is no separate required analysis-only page and no standalone generating page in the current static canonical flow.

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

This inventory separates conceptual screen responsibilities from copy. If a screen is later combined/split by explicit product decision, update this inventory and screen registry together rather than patching navigation ad hoc.