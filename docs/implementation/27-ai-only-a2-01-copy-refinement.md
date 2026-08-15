# 27 — Arcade Console 2 / AI Only — A2_01 Exhibition-Continuation Copy

This file records the latest approved copy change for `A2_01`.

It is a **copy override only**. It does not change the approved Console 2 shell, visual system, prompt-field geometry, control deck, stage, or navigation behavior.

Where this file conflicts with the earlier default A2_01 copy in `22-ai-only-screen-specifications.md`, this file wins.

## Intent

`A2_01` should feel like a continuation of the exhibition, not like a generic AI prompt form.

The visitor has already completed the Human + AI experience. The copy should briefly acknowledge that they have already shaped a love letter with AI while keeping their own memories, choices and authorship in the process, then pivot to the contrast:

> what happens when AI generates the letter on its own?

The system voice must remain concise, neutral and computational. Do not make the transition sentimental, judgmental or anti-AI.

## Locked default copy

### Primary title

```text
you've shaped a love letter with AI.
now see what AI creates on its own.
```

### Supporting line

```text
give it one short direction. it will generate the rest.
```

### Prompt placeholder

Keep the existing fixture placeholder unless separately changed:

```text
example: help me apologize for being distant lately
and express how much she means to me.
```

### Character limit

```text
120
```

## Why this wording is preferred

- It explicitly connects Console 2 to the completed Human + AI experience.
- It makes the exhibition contrast legible without explaining the whole project again.
- `you've shaped a love letter with AI` acknowledges the visitor's authorship in the first experience.
- `now see what AI creates on its own` clearly establishes the AI-only condition without framing AI as threatening or deficient.
- It avoids loaded language such as `AI takes over`, `machine replaces you`, or `now remove yourself`.
- The supporting line transitions naturally into the short prompt field and keeps the AI-only interaction concise.

## Tone constraints

Keep the copy:

- concise;
- observational;
- neutral;
- slightly provocative through contrast, not through accusation;
- readable as exhibition narration;
- non-poetic compared with Console 1;
- non-empathetic/system-led in character.

Avoid phrases such as:

- `let's create something meaningful`;
- `pour your heart out`;
- `AI will understand your feelings`;
- `AI takes over`;
- `remove yourself from the process`;
- `can AI replace you?`;
- `the machine will do it better`.

Do not frame AI as a villain or imply the outcome before the visitor sees the comparison.

## Layout consequence

The title is now longer than the original question copy.

Preserve the existing `A2_01` visual system, but allow the title box to accommodate two deliberate lines:

```text
you've shaped a love letter with AI.
now see what AI creates on its own.
```

Do not shrink the title aggressively to make it fit.

Starting constraints at `1440 × 1080`:

- keep the main content centered in the content region;
- title width approximately `800–900px`;
- use the existing screen-title role;
- preserve generous line spacing and whitespace;
- supporting line sits below as secondary text;
- prompt field remains the dominant interactive element below the transition copy.

If the exact line break renders differently because of font metrics, preserve the two-sentence hierarchy and request review before materially changing font size.

## A2_01 interaction remains unchanged

- `BACK` -> `A2_00`;
- `NEXT` disabled while prompt is empty/whitespace-only;
- `NEXT` enabled when prompt is valid;
- `INTENSITY DIAL` visible but inactive;
- maximum prompt length `120` characters.

Do not add another explanatory screen between A2_00 and A2_01.

## Codex implementation rule

Store this copy in the Console 2 content/config layer rather than hard-coding it into layout CSS/components.

Recommended shape:

```ts
{
  title: "you've shaped a love letter with AI.\nnow see what AI creates on its own.",
  subtitle: "give it one short direction. it will generate the rest.",
  placeholder: "example: help me apologize for being distant lately\nand express how much she means to me.",
  maxLength: 120
}
```

The visual design remains governed by files `19`, `22`, `26` and the canonical references.

## Acceptance

A2_01 is correct only if:

- the old `what would you like AI to focus on?` title is removed;
- the new exhibition-continuation title is rendered;
- the supporting line is rendered exactly from config/current approved copy;
- no new onboarding/explanation screen is added;
- the prompt field and 120-character counter remain;
- A2_00 remains visually unchanged;
- the shell/control deck remain identical to the approved baseline.
