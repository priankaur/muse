# 23 — Arcade Console 2 / AI Only — Testing and Acceptance

Console 2 is visually minimal, so small errors in typography, line weight, control geometry and color are highly visible. Visual regression is mandatory.

Current references:

- `docs/reference/ai-only-console2-canonical.jpg` — screen composition.
- `docs/reference/ai-only-console2-system-refinement-v2.jpg` — latest system/chrome refinement.

## 1. Test categories

Implement:

1. route/flow tests
2. state-persistence tests
3. component interaction tests
4. 1440×1080 screenshot tests
5. geometry assertions
6. token/color assertions
7. anti-Console-1-chrome checks
8. persistent control-deck checks

## 2. Deterministic viewport

Canonical visual tests:

```text
stage: 1440 × 1080
DPR: 1 where possible
animations: disabled
network-dependent content: none
fixture session: fixed
```

Capture **only the internal MUSE stage**.

Exclude:

- browser chrome
- Codex preview chrome
- toasts
- debug overlays
- black host-page space
- dev status UI

## 3. Canonical fixture session

Use one deterministic fixture, e.g.:

```ts
const canonicalAiOnlySession = {
  visitor: { id: 'fixture-001', firstName: 'kristian' },
  recipient: { name: '...', relationship: 'partner' },
  arcade1: {
    completed: true,
    contextForArcade2: 'fixture context',
    humanAiLetter: 'fixture Human + AI letter'
  },
  arcade2: {
    shortPrompt: '',
    proposedToneControls: {
      warmth: 72,
      intimacy: 68,
      emotionalDepth: 70,
      playfulness: 40,
      nostalgia: 55
    },
    toneControls: {
      warmth: 72,
      intimacy: 68,
      emotionalDepth: 70,
      playfulness: 40,
      nostalgia: 55
    }
  }
};
```

## 4. Route tests

Required flow:

```text
A2_00 -> A2_01 -> A2_02 -> A2_03 -> reflection
```

Assertions:

- NEXT on welcome opens prompt
- BACK on welcome is disabled
- prompt BACK returns welcome
- empty prompt disables NEXT
- valid prompt opens interpretation screen
- interpretation BACK preserves prompt
- interpretation NEXT opens result
- result BACK preserves tone controls
- result NEXT enters shared reflection

## 5. Regenerate tests

At `A2_03`, capture before regenerate:

- short prompt
- analysis object
- current tone values
- active result variant index
- visible result body

After regenerate assert:

- short prompt unchanged
- analysis unchanged
- tone values unchanged
- result variant index changed
- visible result changed
- matching insight fixture changed if designed
- route remains `A2_03`

## 6. Analysis/editability tests

`A2_02` contains exactly:

Read-only:

- sentiment
- emotion
- romance

Editable:

- warmth
- intimacy
- emotional depth
- playfulness
- nostalgia

Assert analysis cards contain no input/select/range controls.

Assert exactly five tone range controls exist.

## 7. Dial interaction tests

If the static prototype maps the visible intensity dial to the currently active tone control:

- dial has no effect when no tone control is active/focused
- dial updates only the active tone-control value
- dial does not create a sixth state variable
- keyboard/mouse range input remains accessible
- displayed dial indicator tracks the active value when enabled

Do not test unspecified hardware behavior beyond this defined bridge.

## 8. Inheritance tests

Assert Console 2 does not render:

- registration form
- recipient-name input
- relationship selector

Welcome must use inherited visitor first name.

## 9. Anti-Console-1 checks

For all `A2_*` screens assert no Console 1 shell/chrome is mounted:

- `MuseWindow`
- pixel title bar
- navy grid
- love-letter sprite layer
- Console 1 `HardwareControlStrip`
- glossy/pixel red button assets
- gold pixel dial asset
- magenta CTA

Console 2 **does** have its own `AiControlDeck`, which is visually distinct and allowed.

## 10. Persistent control-deck tests

Every `A2_*` screen must render one `AiControlDeck` with stable geometry.

Assert:

- deck top y position within ±2px
- deck height within ±2px
- strong top separator exists
- BACK button center within ±3px
- NEXT button center within ±3px
- dial center within ±3px
- no bottom-center `MUSE` element exists
- button labels remain `BACK` / `NEXT`
- dial label remains the configured system label (`INTENSITY DIAL` by current default)

Only enabled/disabled state may change between screens.

## 11. Screenshot baselines

Create:

```text
tests/visual/baselines/ai-only/
  A2_00-welcome.png
  A2_01-prompt.png
  A2_02-interpretation.png
  A2_03-result.png
```

Optional states:

```text
A2_01-prompt-focused.png
A2_02-tone-edited.png
A2_02-dial-active.png
A2_03-regenerated.png
```

## 12. Screenshot preparation

Before capture:

- use canonical fixture
- reset focus unless testing focus
- disable caret blink if possible
- disable all animations/transitions
- wait for bundled fonts to load
- wait for layout stable
- ensure screenshot is stage-only 1440×1080

## 13. Visual comparison priorities

Compare in this order:

1. main field tone and deck background split
2. strong horizontal deck separator
3. identity position and heavier `MUSE` weight
4. main content bounding box
5. display/screen title scale and line breaks
6. physical BACK/NEXT button geometry
7. right dial geometry and red indicator
8. red marker size/frequency
9. internal rules and separators
10. analysis/result column proportions
11. form/card line weights
12. fine typography details

Do not tune tiny icons before the global structure is correct.

## 14. Reference adaptation

The original four-screen montage supplies content composition. The refinement image supplies system/chrome character.

Do not literally copy unrelated reference content such as:

- `DIGITAL LOVE LETTER`
- reference-only IDs
- `SYSTEM INITIALIZED` copy unless separately approved
- bottom-center `MUSE`

Do copy/refine:

- heavy condensed display character
- signal-red square markers
- strong system rules
- grey lower deck
- outlined BACK/NEXT buttons
- outlined dial with red pointer

## 15. Geometry assertions

Recommended tolerances:

- identity x/y: ±2px
- deck top: ±2px
- deck height: ±2px
- deck separator thickness: ±1px
- button centers: ±3px
- dial center: ±3px
- prompt field bounds: ±2px
- interpretation grid positions: ±3px

## 16. Color assertions

Use computed styles/tokens.

Validate at minimum:

```text
--ai-bg
--ai-deck-bg
--ai-ink
--ai-ink-muted
--ai-line-strong
--ai-line
--ai-signal
```

Reject dominant blue/periwinkle in Console 2 production styles.

Signal red should be close to the current sampled `#EC5B29` token unless deliberately recalibrated globally.

## 17. Typography acceptance

Assert/inspect:

- persistent `MUSE` uses the heavy condensed display stack
- body text uses neutral sans stack
- system/control labels use mono/semi-mono stack
- no screen is entirely monospaced
- no accidental Inter/Poppins/Montserrat/etc. substitution if the specified bundled fonts exist

## 18. Accessibility acceptance

Interactive controls must:

- be keyboard reachable
- expose correct role/name/state
- show visible focus without neon glow
- not rely only on color for disabled state
- preserve native range semantics for tone controls

Physical-looking deck controls in the browser must still be semantic `<button>`/input elements.

## 19. Content overflow tests

Test:

- long first name
- prompt exactly 120 characters
- analysis summaries wrapping
- `emotional depth` label
- letter body filling reference page

Fix internal layout without changing stage/deck geometry.

## 20. Manual visual checklist

### All screens

- warm off-white main field
- light grey bottom deck
- strong thin deck separator
- identity fixed top-left
- `MUSE` line visibly heavy/condensed
- no screen number
- no bottom-center MUSE
- no dominant blue
- sparse red square markers
- outlined monochrome BACK/NEXT hardware
- outlined monochrome dial with red indicator
- no Console 1 pixel assets
- generous whitespace

### A2_00

- context signal restrained
- tiny red central signal, no blue
- begin instruction uses system microcopy character
- NEXT performs begin

### A2_01

- textarea dominates input task
- field stays rectangular/technical
- NEXT disabled correctly for empty prompt

### A2_02

- exactly 3 analysis blocks
- exactly 5 tone controls
- sliders thin/monochrome
- dial may control active tone only
- layout remains spacious

### A2_03

- letter dominates insight rail
- exactly 4 insight categories including emotion
- regenerate remains a small software action
- BACK/NEXT remain on deck

## 21. Stop condition

If the refined shell/deck/typography is visibly off, do not proceed through all screens.

Calibrate shared tokens and control geometry first.

## 22. Visual approval definition

Console 2 is approved only when a reviewer can compare it against both references and recognize:

- the original four-screen content system
- the refinement's editorial machine character
- black/grey/off-white/red palette
- heavy typography
- precise linework
- minimal physical controls

without seeing:

- Console 1 styling
- generic SaaS UI
- accidental decorative additions
- bottom-center MUSE
- dominant blue
- inconsistent deck geometry.