# 32 — Arcade Console 2 / AI Only — A2_01 Contextual Prompt Hint

This file records the latest approved placeholder/hint behavior for `A2_01`.

It is a **content-source override only**. It does not change the approved A2_01 layout, textarea geometry, character counter, control deck, typography system, stage, or navigation behavior.

Where this file conflicts with the generic placeholder in files `22`, `27`, or `31`, **this file wins**.

## Intent

The prompt hint should no longer feel like a generic AI-writing example.

Because Console 2 is a continuation of the Human + AI experience, the hint inside the prompt field should visibly carry forward the visitor's own earlier letter context.

The visitor should see one or two short sentences drawn from the Arcade 1 letter they already created, rather than an unrelated example such as apologizing for being distant.

This reinforces the exhibit logic:

```text
I already wrote something personal with Human + AI
→
AI Only already knows that context
→
I now give AI one small direction using that same emotional material
```

## Source priority

The hint must use **existing Arcade 1 session/fixture content**. Do not invent a new romantic sentence merely to populate the placeholder.

Use this source order:

1. recognized/extracted text from the visitor's handwritten Arcade 1 letter, when available;
2. otherwise the Human + AI Arcade 1 letter/result fixture that represents that same visitor/session;
3. otherwise a deterministic development fixture derived from the Arcade 1 letter fixture in the current implementation.

Do not use:

- the AI-only generated letter;
- Console 2 analysis summaries;
- generic relationship copy;
- an unrelated stock example;
- model-generated placeholder text at runtime.

## Sentence selection

Select **one or two short sentences** from the Arcade 1 source text.

Prefer sentences that contain:

- a concrete shared memory;
- a clear statement of affection/care;
- something the writer misses;
- a small personal observation;
- a distinctive human detail.

Avoid selecting:

- salutations (`Dear ...`, `Hey ...`);
- sign-offs (`Love,`, `Always,`);
- very long sentences;
- purely logistical sentences;
- duplicated AI-added filler;
- sentences that expose technical metadata or analysis.

Target total quoted source length:

```text
60–110 characters preferred
120 characters maximum for the quoted example block when practical
```

If two source sentences are too long, use the single strongest short sentence.

Do not paraphrase the selected source sentence merely to make it shorter unless the product owner explicitly approves rewriting. Prefer selecting a shorter original sentence instead.

## Placeholder pattern

Use a neutral system-led prefix plus the source sentence(s).

Preferred pattern:

```text
example: stay close to this from your first letter —
“[exact sentence 1] [exact sentence 2 if short]”
```

Alternative compact pattern if field wrapping requires it:

```text
example: build from this — “[exact Arcade 1 sentence]”
```

The quoted sentence(s) must come from the actual Arcade 1 source for the active session/fixture.

The prefix is configurable copy. The quoted source text is contextual data.

## Important implementation distinction

The placeholder is a **hint**, not the user's Console 2 prompt value.

It must never:

- prefill `prompt` state;
- increment the `0 / 120` counter;
- enable `NEXT` while the field is still empty;
- silently submit the Arcade 1 sentence as the user's new instruction.

Expected empty state:

```text
prompt === ''
character counter === 0 / 120
NEXT === disabled
contextual hint visible
```

When the visitor types, the contextual hint disappears exactly like a normal placeholder/hint.

## Recommended data shape

Do not hard-code the selected Arcade 1 sentence inside the `AiPromptField` component.

Recommended derivation:

```ts
type A2PromptContextHint = {
  source: 'arcade1-human-letter' | 'arcade1-human-ai-result' | 'fixture';
  excerpt: string;
};
```

Suggested helper:

```ts
getArcade1PromptHint(session): A2PromptContextHint | null
```

Then content composition can produce:

```ts
const placeholder = hint
  ? `example: stay close to this from your first letter —\n“${hint.excerpt}”`
  : fallbackPlaceholder;
```

The visual component should receive the finished string via props.

## Fallback behavior

If no valid Arcade 1 text exists, do **not** fabricate a fake personal quote and pretend it came from the visitor.

Use a neutral fallback such as:

```text
example: keep the same feeling as your first letter.
```

This fallback is less preferred than using real fixture/session content and should normally only appear in broken/dev state.

## Static prototype requirement

For the current deterministic prototype, Codex must inspect the actual Arcade 1 fixture/session data in the implementation worktree and choose one or two **exact** short sentences from that fixture.

Do not invent the fixture quote in code if an Arcade 1 fixture already exists.

If the current implementation does not yet contain any Arcade 1 letter text, report that as a missing fixture and add a clearly labelled deterministic Arcade 1 letter fixture first; do not claim an invented sentence was previously written by the visitor.

## Visual rules

The approved A2_01 field treatment from file `31` remains unchanged:

- regular neutral sans;
- 16–18px;
- muted grey;
- no bold browser-default placeholder;
- top-left field padding;
- normal wrapping;
- no additional card, callout, icon, or red decoration.

The contextual nature comes from the words, not from a new visual treatment.

## Acceptance

A2_01 is correct only if:

- the old generic apology placeholder is removed;
- the hint references Arcade 1 content;
- one or two exact short source sentences are used when available;
- selected text comes from the active Arcade 1 session/fixture;
- no gendered stock pronoun is introduced;
- prompt state remains empty while the hint is visible;
- counter remains `0 / 120` while empty;
- NEXT remains disabled while empty;
- no A2_01 geometry changes;
- A2_00 regression remains unchanged.

## Codex stop condition

Before moving to A2_02:

1. identify the exact Arcade 1 source field/fixture used;
2. report the exact excerpt selected;
3. implement the context-aware placeholder;
4. capture the empty-state A2_01 screenshot;
5. type a test prompt and verify the hint disappears, counter updates, and NEXT enables;
6. run A2_00/A2_01 regressions;
7. STOP for review if the selected excerpt or wrapping materially changes the approved composition.
