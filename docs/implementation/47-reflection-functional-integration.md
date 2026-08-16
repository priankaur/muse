# 47 — MUSE Reflection Experience — Functional Integration

**Status:** Latest implementation authority for connecting the approved static Reflection screens into one functional five-screen journey.

Read after:

- `38-reflection-source-of-truth.md`
- `39-reflection-visual-system.md`
- `40-reflection-screen-specifications.md`
- `41-reflection-codex-build-playbook.md`
- `42-reflection-foundation-visual-calibration.md`
- `43-reflection-r01-visual-calibration.md`
- `44-reflection-r04-send-choice-dial-interaction.md` — legacy filename; interaction now applies to current `R_03`
- `46-reflection-five-screen-merged-letter-choice.md` — latest product-flow/state authority

This file governs **functional wiring, state, actions, routing, guards, input semantics, integration and testing**. It must not be used as permission to redesign approved screens.

---

# 1. Scope

The static Reflection screens are now approved enough to connect.

Functionalize only:

```text
A2_03 -> R_01 -> R_02 -> R_03 -> R_04 -> R_05 -> session complete
```

Do not redesign the Reflection UI while wiring it.

Do not refactor Console 1 or Console 2 visual systems.

The only Console 2 change allowed in this task is the minimal routing/action needed for `A2_03` to enter Reflection after both completed letters exist.

---

# 2. Canonical five-screen route graph

```text
A2_03 NEXT
  -> R_01

R_01 CONTINUE
  -> R_02

R_02 CONTINUE
  -> R_03

R_03 DIAL_CONFIRM
  -> R_04

R_04 CONTINUE
  -> R_05

R_05 COMPLETE
  -> session complete / physical exit state
```

Back routes:

```text
R_02 BACK -> R_01
R_03 BACK -> R_02
R_04 BACK -> R_03
```

`R_01 BACK` remains product-guarded. Do not expose a route back into Console 2 unless the current implementation already has an explicitly approved behavior.

`R_05` is the terminal Reflection screen. Do not create `R_06`.

---

# 3. Entry guard

Reflection may start only if both completed letter artifacts exist.

Required logical state:

```ts
arcade1.completed === true
arcade1.finalLetter != null
arcade2.completed === true
arcade2.activeGeneratedLetter != null
```

Recommended helper:

```ts
function canEnterReflection(session: SessionState): boolean
```

`A2_03 NEXT` must:

1. verify the guard;
2. create/refresh normalized Reflection comparison input if needed;
3. route to `R_01` only if valid.

If required data is missing:

- do not silently route;
- do not fabricate missing letters;
- use the existing recoverable app error strategy;
- development deep-links may seed deterministic fixtures explicitly.

---

# 4. Reflection state contract

Current required durable state:

```ts
type ReflectionState = {
  experienceTags: string[];

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

Recommended initial state:

```ts
const initialReflectionState: ReflectionState = {
  experienceTags: [],
  sendChoice: null,
  futureApproach: null,
  completed: false,
};
```

The old durable `voiceChoice` is superseded.

If `voiceChoice` exists in current code:

- do not use it in the current product flow;
- migrate/remove required validation/tests safely;
- do not let stale `voiceChoice` preselect `R_03`.

Transient `R_03` candidate state may be local:

```ts
type SendChoiceCandidate = 'human-ai' | 'ai-only' | null;
```

It should commit to `reflection.sendChoice` only on confirm.

---

# 5. Central action model

Use the existing central reducer/state-machine pattern rather than screen-local route hacks.

Recommended semantic actions for Reflection:

```ts
REFLECTION_CONTINUE
REFLECTION_BACK
REFLECTION_TAG_TOGGLE
REFLECTION_SEND_CANDIDATE_LEFT
REFLECTION_SEND_CANDIDATE_RIGHT
REFLECTION_SEND_CONFIRM
REFLECTION_FUTURE_APPROACH_SELECT
REFLECTION_COMPLETE
```

If the repository already has generic semantic actions such as `GO_NEXT`, `GO_BACK`, `ADJUST_UP`, `ADJUST_DOWN`, `CONFIRM`, reuse them when that produces one clear action path.

Do not make pointer, keyboard and physical hardware each own separate business logic.

All inputs must dispatch the same semantic action layer.

---

# 6. R_01 functionality — read both letters

`R_01` is read-only.

Required data:

```text
Human + AI final letter
AI Only final generated letter
```

Requirements:

- render the actual current session letters, not independent decorative fixture strings when a real session is available;
- preserve left/right order: Human + AI left, AI Only right;
- no selection state;
- no analysis mutation;
- `CONTINUE` is enabled once the screen is valid;
- `CONTINUE` routes to `R_02`.

Development deep-link may seed deterministic letter fixtures.

---

# 7. R_02 functionality — normalized comparison + tags

## Comparison data

Create one normalized Reflection model from the two completed results.

Recommended interface:

```ts
type ReflectionComparison = {
  emotionalWarmth: {
    humanAi: string;
    aiOnly: string;
  };
  personalSpecificity: {
    humanAi: string;
    aiOnly: string;
  };
  vocabularyComplexity: {
    humanAi: string;
    aiOnly: string;
  };
  affectionateLanguage: {
    humanAi: string;
    aiOnly: string;
  };
};
```

Use an adapter/service/helper so `ReflectionComparisonGrid` only renders data.

Current deterministic prototype may use approved normalized fixtures, but the visual component must not contain the values as hard-coded presentational constants.

## Tag interaction

Allowed tags remain the current approved set.

Rules:

```text
initial selected count = 0
minimum to continue = 1
maximum = 3
```

`REFLECTION_TAG_TOGGLE(tag)` behavior:

```ts
if tag already selected:
  remove it

else if selected.length < 3:
  add it

else:
  ignore additional selection
```

Requirements:

- no hidden fourth selection;
- no duplicate tag values;
- selection order is not semantically important;
- selected visual state follows approved black/white treatment;
- `CONTINUE` disabled at 0;
- `CONTINUE` enabled at 1–3;
- BACK returns to R_01 without clearing selected tags;
- returning to R_02 should restore current selected tags.

---

# 8. R_03 functionality — merged dial-driven letter choice

This is the current merged question:

```text
Which letter feels most like you — and is the one you'd actually send?
```

## Initial candidate behavior

On first entry to R_03:

```ts
candidate = null
pivotRotation = 0
```

Do not preselect based on:

- comparison analysis;
- experience tags;
- old `voiceChoice`;
- previous fixture defaults.

If the user navigates BACK from R_04 to R_03 after already committing a send choice, preserving that committed choice as the current candidate is acceptable if it clearly reflects existing state and does not auto-advance. Prefer consistency with the current app's back-navigation state policy.

## Dial mapping

Physical / keyboard-emulated dial left:

```text
semantic action -> candidate Human + AI
```

Physical / keyboard-emulated dial right:

```text
semantic action -> candidate AI Only
```

Repeated detents on the same side must not accumulate angle or create new values.

Candidate values remain binary.

## Confirm

Knob press dispatches the same semantic confirm action as keyboard accessibility fallback.

```ts
if candidate === null:
  remain on R_03

if candidate !== null:
  reflection.sendChoice = candidate
  route to R_04
```

Do not require `CONTINUE` after knob confirmation.

Do not let clicking a letter auto-submit. Pointer click selects candidate only; confirm remains a separate semantic action.

## Reentrancy guard

Prevent double-confirm from creating multiple route transitions.

Use the app's central transition lock or an equivalent short-lived `isTransitioning` guard.

Do not scatter independent timing locks across components.

---

# 9. R_04 functionality — future authorship choice

Allowed states:

```text
human-led-ai-refine
ai-led-draft
human-only
```

Initial state:

```text
no default selection
```

Pointer/keyboard/semantic-control selection must all update:

```ts
reflection.futureApproach
```

Only one may be selected at a time.

`CONTINUE`:

- disabled when `futureApproach === null`;
- enabled after a valid choice;
- routes to R_05;
- preserves the selected value when navigating back and forward.

Do not infer this choice from `reflection.sendChoice`.

These are separate questions.

---

# 10. R_05 functionality — confirmation + coin + postcard

R_05 derives content from two separate stored states:

```text
futureApproach -> displayed choice + physical coin label
sendChoice     -> postcard letter payload
```

Do not mix them.

## Future approach label mapping

```ts
const futureApproachDisplay = {
  'human-led-ai-refine': 'I write first. AI helps refine.',
  'ai-led-draft': 'AI drafts first. I choose what stays.',
  'human-only': 'I write without AI.',
};
```

## Coin label mapping

```ts
const coinLabel = {
  'human-led-ai-refine': 'HUMAN FIRST + AI REFINE',
  'ai-led-draft': 'AI DRAFTS FIRST',
  'human-only': 'HUMAN ONLY',
};
```

R_05 must not render if `futureApproach` is missing. Use route guard/recoverable error behavior rather than fabricated defaults.

## Postcard payload

The postcard content must use the letter selected in R_03.

Recommended payload:

```ts
type ReflectionPostcardPayload = {
  selectedLetterType: 'human-ai' | 'ai-only';
  selectedLetterText: string;
  visitorName?: string;
  recipientName?: string;
  futureApproach: ReflectionState['futureApproach'];
  timestamp: string;
};
```

Resolve `selectedLetterText` from the session:

```text
human-ai -> arcade1.finalLetter
ai-only  -> arcade2.activeGeneratedLetter
```

Use the current `PrinterService` interface/stub.

Do not directly call browser print APIs from R_05.

## Idempotency

Entering R_05 or clicking a completion control multiple times must not enqueue duplicate print jobs.

Recommended state/service behavior:

```text
idle -> preparing -> ready
```

or an equivalent idempotent printer-stub contract.

A repeated render must not equal a repeated print invocation.

## Completion

After the final screen is valid and the printer stub has been prepared/invoked as designed:

```ts
reflection.completed = true
session.completed = true
```

Do not create another digital survey/result screen.

---

# 11. Back-navigation persistence

Going BACK must not silently destroy completed Reflection answers.

Expected behavior:

```text
R_02 -> R_01 -> R_02
experienceTags preserved

R_04 -> R_03
futureApproach not yet relevant / preserved if already selected through a later dev route

R_03 committed sendChoice should remain durable once confirmed unless the user deliberately selects and reconfirms a different letter
```

If revisiting R_03, allow the visitor to change the candidate and reconfirm. The most recently confirmed value becomes `reflection.sendChoice`.

Do not reset the entire Reflection state on every route change.

Reset only when starting a genuinely new MUSE session.

---

# 12. Input parity

Every functional control should support the inputs appropriate to its screen without duplicating logic.

## Reflection text navigation

Pointer/click:

```text
BACK / CONTINUE
```

Keyboard fallback:

```text
Enter/Space for focused control
```

Physical arcade controls may dispatch equivalent semantic navigation actions if the hardware integration layer already maps them.

Do not render console hardware graphics in Reflection.

## R_03 dial

Must support:

- physical rotary detents through `HardwareService`/semantic input abstraction;
- keyboard dev fallback;
- mouse/touch candidate selection;
- knob/Enter/Space confirm.

All paths must reach the same candidate/confirm reducer actions.

---

# 13. Transition behavior

Functional wiring must not introduce new visual transition design unless already approved.

For this integration pass:

- use existing route transition behavior;
- avoid browser-history-driven navigation;
- prevent double navigation;
- preserve the fixed 1440×1080 stage;
- do not flash another console shell between A2_03 and R_01;
- Reflection entry should switch directly into `ReflectionShell`.

---

# 14. Development deep-links

Keep development-only deep-link support for static/functional testing.

Examples:

```text
/?screen=R_01&debug=1
/?screen=R_02&debug=1
/?screen=R_03&debug=1
/?screen=R_04&debug=1
/?screen=R_05&debug=1
```

Deep-link fixture seeding must satisfy each screen's route guard explicitly.

Never expose debug chrome in exhibition mode.

---

# 15. Error and guard cases

Functional integration must handle at least:

```text
missing Arcade 1 final letter
missing Arcade 2 generated letter
R_02 with zero tags trying to continue
R_03 confirm with null candidate
R_04 continue with no future approach
R_05 missing sendChoice
R_05 missing futureApproach
missing printer fixture/service
invalid Reflection route ID
```

Use recoverable app error handling consistent with the project.

Do not silently invent state.

---

# 16. Tests — reducer/state unit coverage

Add tests for:

## Entry

- cannot enter Reflection without both letters;
- valid A2_03 NEXT enters R_01.

## R_01

- renders both current session letters;
- continue routes R_01 -> R_02.

## R_02

- starts with zero tags in a fresh session;
- one tag enables continue;
- three tags allowed;
- fourth tag rejected;
- deselection works;
- tags persist through back/forward.

## R_03

- starts with null candidate;
- dial left selects Human + AI candidate;
- dial right selects AI Only candidate;
- repeated same-direction detents do not create additional values/rotation accumulation;
- confirm with null stays on R_03;
- confirm with candidate stores sendChoice and routes to R_04;
- pointer selection does not auto-submit;
- no stale voiceChoice preselection;
- double confirm causes one route transition.

## R_04

- no default futureApproach;
- exactly one selection stored;
- changing selection replaces old value;
- continue disabled while null;
- continue routes to R_05 when valid.

## R_05

- displays futureApproach label from stored state;
- maps correct coin label;
- resolves postcard letter from sendChoice;
- Human + AI sendChoice uses Arcade 1 final letter;
- AI Only sendChoice uses Arcade 2 active generated letter;
- printer stub invocation is idempotent;
- completion state is set once.

---

# 17. Playwright end-to-end flows

Add at least these deterministic E2E paths.

## Path A — Human + AI letter + human-led future approach

```text
seed both completed letters
A2_03 -> R_01
R_01 continue
R_02 select 1–3 tags -> continue
R_03 dial left -> confirm
R_04 choose human-led-ai-refine -> continue
R_05 assert selected approach
assert HUMAN FIRST + AI REFINE coin
assert postcard payload uses Arcade 1 final letter
assert session complete
```

## Path B — AI Only letter + AI-led future approach

```text
seed both completed letters
enter Reflection
R_02 select tags
R_03 dial right -> confirm
R_04 choose ai-led-draft -> continue
R_05 assert AI DRAFTS FIRST coin
assert postcard payload uses Arcade 2 generated letter
```

## Path C — Human-only future approach

```text
choose either valid send letter
R_04 choose human-only
R_05 assert HUMAN ONLY coin
```

## Path D — back/edit behavior

```text
select R_02 tags
continue to R_03
back to R_02
assert tags preserved
continue
select/confirm a sendChoice
proceed to R_04
back to R_03
change candidate and reconfirm
assert newest sendChoice is used for postcard
```

---

# 18. Visual regression during functionality work

Do not accept functionality at the cost of visual drift.

After wiring, capture stage-only 1440×1080 screenshots for:

- R_01;
- R_02 zero tags;
- R_02 three tags;
- R_03 neutral;
- R_03 left candidate;
- R_03 right candidate;
- R_04 no selection;
- R_04 selected;
- R_05 each futureApproach fixture if practical.

Compare against approved static screens/calibrations.

Functional state may change visible selection states. Geometry/style must remain otherwise unchanged.

Also rerun Console 1 and Console 2 smoke/visual regression tests.

---

# 19. Implementation order

Do not connect everything through ad-hoc edits in one pass.

Recommended sequence:

```text
1. audit current static Reflection implementation
2. normalize route IDs/progress to current five-screen flow
3. implement/clean ReflectionState + reducer actions
4. wire A2_03 entry guard -> R_01
5. wire R_01 navigation/data
6. wire R_02 normalized data + tag state
7. wire R_03 dial candidate + confirm
8. wire R_04 futureApproach state
9. wire R_05 coin mapping + printer stub + completion
10. add reducer/unit tests
11. add Playwright E2E flows
12. run visual regressions
13. run Console 1/2 regressions
```

Commit in logical steps if the working branch allows it.

---

# 20. Functional acceptance checklist

Reflection is functionally complete only when all are true:

- exactly five current Reflection screens exist in the active route graph;
- all progress labels are `/05`;
- A2_03 enters Reflection only with both final letters;
- R_01 uses actual session letters;
- R_02 comparison uses structured normalized data;
- R_02 tags select/deselect with max 3;
- R_02 continue gating works;
- R_03 dial candidate works left/right;
- R_03 knob confirm commits one sendChoice and advances;
- R_04 futureApproach selection and gating work;
- R_05 displays the stored futureApproach;
- R_05 maps the correct physical coin label;
- R_05 postcard uses the R_03-selected letter;
- printer stub cannot duplicate jobs from rerenders/double actions;
- back navigation preserves user choices;
- pointer/keyboard/physical semantic inputs share one logic path;
- invalid states are guarded rather than fabricated;
- Reflection completion sets session state once;
- static approved visuals have not drifted;
- Console 1/Console 2 regressions remain clean.

## Stop gate

After functional wiring, provide:

1. a route/state audit summary;
2. files changed;
3. reducer/actions added or changed;
4. input mappings;
5. tests added;
6. test/typecheck results;
7. stage-only screenshots of key interaction states;
8. any remaining hardware/printer integration that is still stubbed.

Do not introduce new product behavior beyond this plan without approval.
