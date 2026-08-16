# 45 — MUSE Reflection Experience — Consolidated Current Directive

**Status:** Latest consolidated implementation authority for the Reflection experience as of the latest reviewed screenshots and interaction decisions.

Read this file **after** `38`–`44`. When this file summarizes or clarifies a later decision, it is the fastest current reference for Codex before continuing Reflection work.

This file does not replace the detailed visual-system rules in `39`, the foundation calibration in `42`, the analysis/tag calibration in `43`, or the dial-driven send-choice interaction in `44`. It consolidates the current flow, current screen numbering, approved states, and remaining implementation work so Codex does not rely on chat history.

---

# 1. Reflection is a third visual system

Reflection begins only after both console experiences are complete and both final letters exist.

It is not a continuation of Arcade 1 or Arcade 2 styling.

Use only `ReflectionShell` and Reflection-specific components.

Do not mount or visually reproduce:

- `MuseWindow`;
- Arcade 1 navy grid, purple/lavender desktop window, pixel sprites, magenta CTA, pixel typography, arcade hardware strip;
- `AiOnlyShell`;
- Console 2 `MUSE / AI ONLY / ARCADE CONSOLE 2` identity;
- Console 2 grey control deck;
- Console 2 outlined on-screen BACK/NEXT hardware controls;
- Console 2 on-screen dial graphic;
- Console 2 red-square signal motif as a persistent Reflection language.

Shared stage/state/input infrastructure may be reused.

---

# 2. Shared Reflection visual baseline

The approved Reflection shell is governed by file `42`.

At `1440 × 1080`:

- background: approximately `#FAF9F6`;
- top-left progress at approximately `x:72`, `y:58–64`;
- bottom-left text BACK anchor around `x:72`, baseline near `y:1010`;
- bottom-right text CONTINUE anchor with right edge around `x:1368`, baseline near `y:1010` where the screen uses Continue;
- no persistent footer line/control deck;
- no MUSE identity by default;
- no decorative color outside subtle letter-paper tint;
- neutral contemporary grotesk typography;
- generous whitespace.

Enabled navigation uses near-black. Disabled navigation uses pale neutral grey.

Do not move shared anchors when states change.

---

# 3. Current canonical flow — SIX screens

The Reflection sequence is now:

```text
A2_03 NEXT
→ R_01 Read both letters
→ R_02 Analysis + experience tags
→ R_03 Which letter sounds like you?
→ R_04 Which letter would you actually send? — dial-driven selector
→ R_05 Future authorship / agency choice
→ R_06 Physical token + printed postcard exit
→ session complete
```

All progress labels must use:

```text
REFLECTION NN / 06
```

Do not use `/05` anywhere in the current Reflection implementation.

---

# 4. R_01 — Read both letters first

## Purpose

The visitor must see and read the two completed letters **before** seeing normalized analysis or being asked to evaluate the experience.

This is a quiet reading/pause screen.

## Progress

```text
REFLECTION 01 / 06
```

## Copy

Heading:

```text
Read both letters side by side.
```

Supporting line:

```text
Take a moment with each one before comparing how they feel.
```

## Layout

Show two equal `ReflectionLetterCard` components side by side.

Left:

```text
LETTER A
HUMAN + AI
```

Right:

```text
LETTER B
AI ONLY
```

Both cards use:

- identical dimensions;
- identical subtle paper tint (`~#F1EEE8` starting token);
- identical border;
- identical typography;
- identical elevation;
- equal horizontal prominence.

No analysis.
No tags.
No choice.
No highlighted letter.

This screen is read-only.

R_01 CONTINUE routes to R_02.

R_01 BACK remains product-guarded because returning to A2_03 after entering Reflection may be undesirable. Keep existing guard behavior unless explicitly changed.

---

# 5. R_02 — Analysis + experience-feeling tags

This is the screen already visually developed in the latest screenshots.

## Progress

```text
REFLECTION 02 / 06
```

## Approved copy

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

Helper still required unless explicitly removed later:

```text
choose up to 3
```

Keep the helper quiet, centered, approximately `13–14px`, muted grey.

## Normalized comparison schema

Use exactly:

1. emotional warmth
2. personal specificity
3. vocabulary complexity
4. affectionate language

Use one normalized Reflection adapter/model.

Do not place raw Arcade 1 and Arcade 2 analysis components side by side.

The current deterministic fixture may resolve to:

```text
                     HUMAN + AI      AI ONLY
emotional warmth     high            moderate
personal specificity high            medium
vocabulary complexity medium         high
affectionate language high            restrained
```

But the visual component must consume structured data rather than hard-code these strings into presentation markup.

## Tag options

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

Selection rules:

- minimum to continue: 1;
- maximum: 3;
- no fourth selection;
- no requirement to select all 3.

Idle tag:

- warm-white fill;
- 1px neutral border;
- near-black text;
- small radius;
- no shadow.

Selected tag:

- near-black fill;
- warm-white text;
- same geometry.

The latest reviewed selected-state screenshot demonstrates the correct selection treatment: selected tags such as `personal`, `thoughtful`, and `too polished` use black fill with white text, while unselected tags remain outlined.

CONTINUE:

- disabled when zero tags are selected;
- enabled near-black when at least one tag is selected.

## Remaining R_02 polish

Earlier calibration requested a more balanced tag wrap (ideally close to `5 + 5` at 1440×1080) instead of a long first row with only two tags on the second row.

Treat this as a layout refinement if not yet implemented, but do not change the approved tag component style or overall R_02 composition.

---

# 6. R_03 — Which letter sounds more like you?

## Purpose

Voice identity only. This is NOT the send-choice screen.

## Progress

```text
REFLECTION 03 / 06
```

## Copy

Heading:

```text
Which letter sounds more like you?
```

Supporting line:

```text
Not which one is better — which one feels closer to your voice.
```

Optional quiet microcopy above answer controls:

```text
Select the closest fit
```

## Layout

Show both complete letters side by side using the same left/right ordering and equal visual treatment used throughout Reflection.

Left:

```text
LETTER A
HUMAN + AI
```

Right:

```text
LETTER B
AI ONLY
```

Use equal card size/tint/border/typography.

## Choices

Provide exactly four current options:

- Human + AI
- AI Only
- Parts of both
- Neither

Store:

```ts
reflection.voiceChoice =
  | 'human-ai'
  | 'ai-only'
  | 'parts-of-both'
  | 'neither'
  | null;
```

No default selection.

Use Reflection-style black/white selection controls, not console styling.

CONTINUE remains disabled until one option is selected.

R_03 CONTINUE routes to R_04.

---

# 7. R_04 — Dial-driven “Which letter would you actually send?”

Detailed authority: file `44`.

This screen intentionally introduces one memorable physical interaction while preserving the quiet Reflection visual system.

## Progress

```text
REFLECTION 04 / 06
```

## Prompt

```text
Which letter would you actually send?
```

Supporting line:

```text
Choose the one you would put your name behind.
```

## Composition

Use three objects horizontally:

```text
[ HUMAN + AI LETTER ]    [ CENTRAL QUESTION / PIVOT CARD ]    [ AI ONLY LETTER ]
```

The letters must remain identical in size, tint and prominence.

The central card is visually smaller and behaves as a directional selector.

No bright colors, hearts, decorative patterns or playful website styling from the interaction reference are allowed.

## Dial candidate state

```ts
type SendChoiceCandidate = 'human-ai' | 'ai-only' | null;
```

Initial:

```text
candidate = null
pivot = 0deg
```

Dial left:

```text
candidate = human-ai
pivot ≈ -5deg to -7deg
translateX ≈ -6px to -12px
```

Dial right:

```text
candidate = ai-only
pivot ≈ +5deg to +7deg
translateX ≈ +6px to +12px
```

Motion:

- subtle editorial transition;
- around `140–190ms`;
- no spring/bounce/wobble;
- respect `prefers-reduced-motion`.

## Candidate-letter feedback

Selected candidate letter:

```text
2px near-black border
```

Unselected letter:

```text
1px neutral border
```

Do not change paper tint.
Do not heavily dim the unselected letter.
Do not add green checks, winner labels or color coding.

## Knob press

Dial movement previews only.

Knob press / semantic `DIAL_CONFIRM` commits the choice and advances.

```ts
if (candidate === null) {
  // stay on R_04
}

if (candidate === 'human-ai' || candidate === 'ai-only') {
  reflection.sendChoice = candidate;
  routeTo('R_05');
}
```

Do not require a second on-screen Continue action after knob confirmation.

BACK remains bottom-left and routes to R_03.

Do not show an active `CONTINUE →` that bypasses dial selection/confirmation.

Development/accessibility fallback:

- clicking a letter may set the candidate;
- clicking does not auto-submit;
- Enter/Space may dispatch the same confirm action;
- visible design remains unchanged.

Critically:

```text
voiceChoice != sendChoice
```

Do not preselect R_04 from R_03.

---

# 8. R_05 — Future authorship / agency choice

## Progress

```text
REFLECTION 05 / 06
```

## Question

```text
Next time you want to say something that matters,
how would you rather write it?
```

Use exactly three visually equal Reflection choice cards.

### A

```text
I write first. AI helps refine.
```

Supporting copy:

```text
Start with my own words, then use AI to improve or clarify them.
```

State:

```text
human-led-ai-refine
```

### B

```text
AI drafts first. I choose what stays.
```

Supporting copy:

```text
Begin with an AI-written draft, then edit or keep what feels right.
```

State:

```text
ai-led-draft
```

### C

```text
I write without AI.
```

Supporting copy:

```text
Keep meaningful writing entirely in my own words.
```

State:

```text
human-only
```

All three must have identical dimensions, hierarchy and selected-state treatment.

Do not label one recommended/balanced/best.

Store independently in `reflection.futureApproach`.

CONTINUE routes to R_06.

---

# 9. R_06 — Token + postcard physical exit

## Progress

```text
REFLECTION 06 / 06
```

## Headline

```text
One last choice — make it physical.
```

## Instructions

```text
01  Pick up the token that matches your choice.
02  Drop it into the corresponding box.
03  Collect your printed postcard on the way out.
```

Physical mapping:

```text
human-led-ai-refine -> HUMAN FIRST + AI REFINE
ai-led-draft       -> AI DRAFTS FIRST
human-only         -> HUMAN ONLY
```

Prepare postcard content from `reflection.sendChoice`.

Current implementation uses the printer stub only.

No real printer dependency yet.

No confetti.
No score.
No winner screen.
No additional survey question.

---

# 10. Current Reflection state contract

Recommended:

```ts
type ReflectionState = {
  experienceTags: string[];

  voiceChoice:
    | 'human-ai'
    | 'ai-only'
    | 'parts-of-both'
    | 'neither'
    | null;

  sendChoice:
    | 'human-ai'
    | 'ai-only'
    | null;

  futureApproach:
    | 'human-led-ai-refine'
    | 'ai-led-draft'
    | 'human-only'
    | null;

  completed: boolean;
};
```

R_04 may keep `sendChoiceCandidate` as transient/local state until confirmation.

Do not collapse `voiceChoice`, `sendChoice`, and `futureApproach`.

---

# 11. Cross-screen invariants

Across `R_01`–`R_06`:

- use the same `ReflectionShell`;
- use `/06` progress count;
- preserve Reflection background and navigation anchors;
- no console identity/chrome;
- identical letter A/B ordering;
- identical paper tint for both letters;
- no moralized color coding;
- no winner/recommended language;
- copy remains configurable;
- visual neutrality remains mandatory.

Physical input may drive semantic actions without adding on-screen console hardware graphics.

---

# 12. Current build order from the latest reviewed state

The latest reviewed implementation already contains the R_02 analysis/tag composition and selected-tag state.

Codex should now audit what is actually present before changing routes.

Recommended next sequence:

```text
A. preserve/refine current R_02
B. insert new R_01 read-both-letters screen before it
C. renumber progress/state routes to /06
D. implement R_03 voice-choice screen
E. implement R_04 dial-driven send-choice screen from file 44
F. implement R_05 agency choice
G. implement R_06 exit
H. integrate full flow
I. full regression
```

Do not rebuild already-approved Reflection components unnecessarily.

Stop after each new screen for screenshot review unless the user explicitly asks Codex to continue through multiple phases.

---

# 13. Current required visual regression set

At minimum capture stage-only `1440 × 1080` screenshots for:

- R_01 read-both-letters;
- R_02 zero tags selected;
- R_02 one tag selected;
- R_02 three tags selected;
- R_03 no choice;
- R_03 one voice choice selected;
- R_04 neutral candidate;
- R_04 Human + AI candidate;
- R_04 AI Only candidate;
- R_05 no stance selected;
- R_05 one stance selected;
- R_06 exit.

Also verify no Arcade 1 or Arcade 2 visual regressions.

---

# 14. Non-negotiable product logic

The emotional sequence must remain:

```text
READ
→ COMPARE + REFLECT
→ RECOGNIZE MY VOICE
→ CHOOSE WHAT I WOULD SEND
→ CHOOSE MY FUTURE WRITING APPROACH
→ PHYSICAL EXIT
```

Do not reorder this sequence without explicit product-owner approval.

The interaction reference for R_04 changes only the **selection behavior**, not the Reflection visual style.
