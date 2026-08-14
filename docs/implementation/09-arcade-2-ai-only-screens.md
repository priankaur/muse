# 09 — Arcade 2: AI-only Screen Specifications

Arcade 2 is intentionally AI-led. It inherits context from Arcade 1 and should not make the visitor repeat setup.

The experience should not be written as a cartoonishly mechanical parody. It can be competent and smooth while intentionally lacking the human specificity, empathy and soulfulness produced by the human-first path.

## Persistent shell

Use the same canonical MUSE design system. If the second console receives a distinct accent treatment later, implement it through tokens/variant props rather than a separate component library.

Top-right label becomes the Arcade 2 console label when visible.

## Inherited state

On entry, Arcade 2 already knows:

- visitor name,
- recipient name,
- relationship,
- Human + AI result required for later comparison.

Do not ask for these again.

---

## `A2_00` — Welcome back

### Goal

Acknowledge continuity between the two arcades.

### Content

Use visitor first name and, if appropriate, recipient context in a concise way.

### UI

Narrative screen using existing greeting/hero components. No new onboarding form.

---

## `A2_01` — Short prompt

### Goal

Give AI a small amount of user direction without recreating the human-writing exercise.

### UI

- one prompt question,
- text field/textarea,
- character counter if the content config specifies a cap,
- concise CTA.

The user has asked that a short prompt remains part of AI-only.

### Validation

Require the minimum prompt content defined by config. Keep the UI permissive and quick.

---

## `A2_02` — Machine analysis

### Goal

Make the AI system's interpretation visible.

The AI-only experience includes:

- sentiment analysis,
- emotion detection,
- romance / romantic-intent detection.

### Static phase

Use deterministic fixtures such as:

```ts
{
  sentiment: 'positive',
  emotions: ['affection', 'nostalgia'],
  romanceIntent: 'moderate'
}
```

These are implementation fixtures, not final exhibit copy.

### Visual treatment

Use 2–3 compact system readouts inside the existing window. They should feel like machine interpretation, not a scored diagnosis.

Avoid scientific-looking precision that the actual system will not support. Do not show fake percentages unless the product explicitly chooses them later.

### CTA

Continue to intensity controls.

---

## `A2_03` — Intensity controls

### Goal

Allow the visitor to tune AI-only output.

### Interaction grammar

Use the same rotary/dial system as Arcade 1 so the visitor does not relearn controls.

### Configuration

Exact controls should be defined in `src/content/tuningControls.ts`. Do not hard-code labels in the component.

The system must support at least:

- a list of named parameters,
- low/high labels,
- discrete numeric steps,
- active parameter index,
- confirmed value per parameter.

### Important experience difference

Arcade 2 does not receive the handwritten letter as its semantic source. It starts from inherited recipient context + short prompt + machine analysis + intensity settings.

---

## `A2_04` — AI-only generating

### Goal

Show machine-led generation.

### Static phase

No API call. Use fixture state.

### Tone

System copy can be efficient/confident but should not become villainous or intentionally broken.

---

## `A2_05` — AI-only result

### Goal

Present the second letter so the visitor can later compare it with the Human + AI result.

### Requirements

- readable letter-preview component reused from Arcade 1,
- recipient name inherited from session,
- fixture result stored as `arcade2.generatedLetter`,
- no repeated context questions.

### Fixture writing goal

The static fixture should illustrate the intended contrast without making the answer obviously terrible. It can be polished but more generic and less personally grounded.

### Completion guard

Do not enter reflection unless both result letters exist.
