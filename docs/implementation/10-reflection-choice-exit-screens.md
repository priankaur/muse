# 10 — Reflection, Choice and Exit Screen Specifications

Reflection is part of the experience, not a research-survey appendix. The interface must not imply that the visitor is being scored or that one answer is morally correct.

All answer options should have equal visual legitimacy.

## `R_01` — Which one sounds like you?

Prompt:

`Which one sounds like you?`

Legacy option set available as content fixture:

- the first one
- the second one
- neither
- parts of both

Use the standard choice-tag/card component. No points, trophies or correctness state.

## `R_02` — What did you feel?

Prompt:

`When you read the machine's letter, what did you feel?`

Legacy multi-select fixture options:

- impressed
- embarrassed
- nothing much
- relieved I didn't have to write it
- uneasy
- amused

Use a multi-select variant of the same choice system. Confirm action advances.

## `R_03` — Was the difference worth it?

Legacy question:

`The first letter took about four minutes. The second took longer. Was the difference worth it?`

Because the current experience ordering has changed, final timing/copy must be content-configurable rather than copied blindly from the old flow.

Use equal-weight options. Do not build a ranking visual.

## `R_04` — What did the machine get wrong?

Typed response.

The wording should direct criticism toward the machine/system, not shame the visitor.

Use the standard text-entry component with a larger multi-line variant if required.

## `R_05` — Finish the sentence

Legacy framing:

`Next time I want to say something that matters, I'll…`

Typed response.

## `R_06` — Which letter would you send?

### Goal

Present the Human + AI letter and AI-only letter side by side.

### Layout

Use a comparison sub-layout inside the same window. Both letter cards must receive equal size and visual prominence.

Do not label one as winner/better.

Provide a clear selected state and confirmation action.

### State

Store:

`reflection.chosenLetter` = `human-ai` or `ai-only`.

## `R_07` — Your stance

Three choices:

- Convenience
- Control
- More Human

### Semantics

- Convenience — let AI take more of the writing task.
- Control — use AI but retain authorship/control.
- More Human — keep some meaningful writing fully human.

These descriptions are explanatory implementation notes; final exhibit copy lives in content config.

### Visual rule

All three choices:

- same area,
- same hierarchy,
- same interaction style,
- distinct only by text/icon/accent if approved.

Do not use gold/silver/bronze, ranking, trophy, winner labels, or a preferred default.

### State

Store stance selection. In the future, this is the logical trigger for postcard printing.

## `R_08` — Physical handoff / completion

### Static phase

Represent three things:

1. the visitor's chosen letter is ready for the takeaway pipeline,
2. the visitor should complete the physical token-wall ritual,
3. the arcade session is complete.

### Future integration seam

Call the `PrinterService` stub when entering the state after `R_07`, but the static implementation should only record/log the requested print payload.

### Print payload contract

Prepare a typed object containing:

- chosen letter text,
- visitor name,
- recipient name,
- date/time placeholder,
- stance label.

No real printing in this phase.

## Reflection progress

A simple `QUESTION N / 5` indicator is acceptable if needed, but it must not resemble score/progress points. Avoid hearts-as-lives or stars-as-score during reflection.
