# 37 — Arcade Console 2 / AI Only — Generation Style Guardrails

**Status:** Latest generation-style authority for Console 2 AI-only letter output.

This file records an explicit product decision about how the AI-only letter must sound.

Where this file conflicts with older assumptions that the five tone sliders can make Console 2 fully soulful, affectionate or emotionally expressive, **this file wins**.

It does not change the A2_02 visual design or the five existing controls. It changes how those controls are interpreted by the generation layer.

## Core product decision

Console 2 should produce a letter that is:

- lexically sophisticated;
- articulate;
- polished;
- compositionally controlled;
- comparatively restrained in emotional expression;
- comparatively restrained in overtly loving/affectionate vocabulary.

This remains true **even when the visitor sets warmth, intimacy, emotional depth, playfulness or nostalgia to their maximum values**.

The five controls therefore operate **inside a constrained AI-only envelope**. They are not permission to make the output as soulful, tender or emotionally rich as the Human + AI letter.

This constraint is intentional and supports the exhibition contrast between:

```text
Human + AI
= personal source material + human authorship + AI assistance

AI Only
= highly competent language generation with limited emotional texture
```

Do not make Console 2 robotic, grammatically stiff or nonsensical. The difference should come from **emotional restraint and lexical polish**, not bad writing.

---

# 1. Fixed generation priorities

The generation layer should apply these priorities in order:

1. preserve factual/contextual relevance;
2. use high lexical sophistication and precise diction;
3. preserve readability and coherence;
4. honor the five tone controls within the allowed envelope;
5. keep emotional and affectionate expression below the Human + AI ceiling;
6. avoid overt empathy, gushy intimacy, or highly sentimental romantic language.

The visitor's sliders cannot override priorities 2 and 5.

---

# 2. High-vocabulary requirement

Console 2 output should consistently prefer:

- precise verbs rather than generic emotional verbs;
- varied sentence structure;
- controlled subordinate clauses;
- nuanced adjectives/adverbs used sparingly;
- abstract/reflective phrasing where appropriate;
- polished transitions;
- less colloquial repetition;
- more formally composed syntax than the Human + AI result.

The target is **sophisticated but readable**, not thesaurus-heavy or pretentious.

Avoid:

- obscure vocabulary used only to sound intelligent;
- archaic diction;
- academic jargon;
- long sentences that damage clarity;
- purple prose.

A good Console 2 letter may sound impressively composed, but it should also feel slightly more authored by a language system than by a vulnerable person.

---

# 3. Emotional-expression ceiling

Regardless of slider values, keep emotional expression comparatively restrained.

The output may acknowledge:

- care;
- appreciation;
- closeness;
- memory;
- gratitude;
- attraction;
- relational importance.

But limit:

- repeated declarations of love;
- intense longing;
- overt vulnerability;
- pleading/reassurance language;
- emotional hyperbole;
- highly intimate confessions;
- sentimental repetition;
- emotionally loaded pet names;
- excessive exclamation marks;
- melodramatic metaphors.

The AI-only output should not repeatedly use phrases equivalent to:

- `I love you more than words can say`;
- `you are my everything`;
- `I cannot imagine my life without you`;
- `my heart belongs to you`;
- `I miss you every second`;
- `you make me feel whole`.

If such language exists in inherited context, the AI can preserve the underlying meaning while rephrasing it more analytically or composedly.

---

# 4. Loving-word restraint

Use overtly affectionate vocabulary less frequently than in the Human + AI experience.

Prefer words such as:

- value;
- appreciate;
- admire;
- significant;
- meaningful;
- close;
- important;
- familiar;
- enduring;
- considerate;
- connected;
- memorable.

Use more sparingly:

- love;
- adore;
- darling;
- sweetheart;
- beloved;
- soulmate;
- heart;
- forever;
- deeply in love.

Do not ban the word `love` entirely. The experience is still generating a love letter. The goal is **lower frequency and lower emotional saturation**, not lexical censorship.

---

# 5. Slider semantics under the constrained envelope

The existing A2_02 controls remain:

1. warmth;
2. intimacy;
3. emotional depth;
4. playfulness;
5. nostalgia.

They must now be interpreted as follows.

## Warmth

Higher warmth may increase:

- courtesy;
- acknowledgement;
- positive regard;
- softer sentence cadence;
- appreciative phrasing.

Higher warmth must **not** automatically increase:

- declarations of love;
- emotional gushiness;
- endearments;
- sentimental intensifiers.

At `100`, the letter should feel warm **for Console 2**, not maximally affectionate in absolute terms.

## Intimacy

Higher intimacy may increase:

- specificity of shared context;
- direct second-person address;
- references to private/shared details already present in session context;
- closeness of phrasing.

Higher intimacy must **not** automatically increase:

- vulnerable confessions;
- erotic content;
- pet names;
- dependency language;
- emotionally exposing declarations.

At `100`, intimacy means **more personally specific**, not more emotionally naked.

## Emotional depth

Higher emotional depth may increase:

- reflection;
- nuance;
- acknowledgement of mixed feelings;
- abstract relational insight;
- complexity of sentence structure.

Higher emotional depth must **not** simply mean more emotional adjectives or stronger declarations.

At `100`, prefer **conceptual depth over emotional intensity**.

## Playfulness

Higher playfulness may increase:

- light wit;
- clever phrasing;
- gentle irony;
- rhythmic variation;
- subtle wordplay.

Do not make it:

- cute or childish;
- emoji-like;
- full of pet names;
- exaggeratedly flirty;
- emotionally bubbly.

## Nostalgia

Higher nostalgia may increase:

- references to shared memories;
- reflective temporal framing;
- contrast between past and present;
- precise recall of inherited context.

Do not turn nostalgia into:

- sentimental longing;
- repeated `I miss...` language;
- idealization of the past;
- melodramatic memory language.

At `100`, nostalgia means **more memory-oriented and reflective**, not more sentimental.

---

# 6. Recommended generation-envelope model

The implementation may encode the above as explicit policy constants rather than relying on prose alone.

Conceptual example:

```ts
type AiOnlyGenerationPolicy = {
  vocabularySophistication: 'high';
  emotionalExpressivenessCeiling: number;
  affectionateLexiconCeiling: number;
  sentimentalityCeiling: number;
  empathySimulation: 'low';
};

const AI_ONLY_GENERATION_POLICY: AiOnlyGenerationPolicy = {
  vocabularySophistication: 'high',
  emotionalExpressivenessCeiling: 0.45,
  affectionateLexiconCeiling: 0.35,
  sentimentalityCeiling: 0.35,
  empathySimulation: 'low'
};
```

These numbers are implementation heuristics, not scientific measurements. They exist to make the product rule testable and to prevent slider values from accidentally erasing the distinction between the two consoles.

A tone control value should be mapped inside the allowed range rather than directly to absolute expressive intensity.

Conceptual example:

```ts
function mapWarmthForAiOnly(userWarmth: number) {
  return lerp(0.15, 0.45, userWarmth / 100);
}
```

The exact internal mapping may evolve, but the **ceiling behavior is locked**.

---

# 7. Prompt / model instruction contract

When production AI generation is introduced, the generation instruction must explicitly include the fixed Console 2 policy before applying user controls.

Conceptual instruction order:

```text
SYSTEM / PRODUCT STYLE POLICY
- write with high lexical sophistication and polished syntax
- remain readable and coherent
- maintain emotional restraint
- use affectionate/loving vocabulary sparingly
- do not simulate deep empathy or vulnerability
- do not become gushy even at maximum warmth/intimacy/emotional-depth settings

SESSION CONTEXT
- inherited Arcade 1 context
- recipient/relationship
- A2_01 short prompt

USER-ADJUSTABLE TONE
- warmth X
- intimacy X
- emotional depth X
- playfulness X
- nostalgia X

IMPORTANT
Interpret the tone values only within the fixed AI-only style envelope above.
```

Do not put the fixed style guardrail after the user values where it can be treated as optional.

---

# 8. Static fixture requirement

The current prototype uses deterministic fixtures.

Update all A2_03 result fixtures so they visibly demonstrate this rule.

Even the fixture generated from all-high tone values should remain:

- more lexically polished than the Human + AI result;
- less emotionally saturated;
- lower in overtly loving words;
- less soulful/empathetic;
- still clearly recognizable as a love letter.

Do not make the high-setting fixture suddenly sound indistinguishable from Arcade 1.

At least one fixture/test should represent an extreme input such as:

```text
warmth: 100
intimacy: 100
emotionalDepth: 100
playfulness: 100
nostalgia: 100
```

and verify that the output still respects the Console 2 style envelope.

---

# 9. Post-generation analysis on A2_03

File `34` remains authoritative that analysis appears only after generation.

The post-generation analysis must analyze the **actual generated fixture/output**.

Do not artificially force analysis values to be low just because Console 2 is intended to be emotionally restrained.

Instead:

1. generate/write the result according to this style policy;
2. analyze that result;
3. display the resulting sentiment/emotion/romance/tone profile.

The analysis should remain internally consistent with the letter shown.

For deterministic fixtures, author matching analysis values that plausibly describe each fixture.

---

# 10. Comparison with Human + AI

The intended qualitative contrast is:

## Human + AI

- more personal texture;
- more uneven/human phrasing;
- more emotional specificity;
- more direct affection;
- more vulnerable or soulful moments;
- AI assists rather than defines the voice.

## AI Only

- more polished;
- more syntactically controlled;
- more lexically sophisticated;
- less emotionally saturated;
- fewer overt loving words;
- less vulnerability;
- less empathy/soulfulness;
- machine competence is visible in the language itself.

Do not make AI Only intentionally bad. The contrast should be **polish versus human emotional texture**, not good writing versus bad writing.

---

# 11. UI implication

Do **not** rename or remove the five A2_02 controls solely because of this policy.

The visitor can still set all values to 100.

That is useful to the exhibit: even at maximum values, the resulting AI-only letter should reveal that the system is operating inside its own stylistic/emotional limits.

Do not add visible warning copy such as:

- `AI cannot feel emotions`;
- `warmth is capped`;
- `AI emotional range limited`.

Let the difference be experienced through the generated result and later comparison/reflection.

---

# 12. Acceptance tests

Add/adjust tests or fixture assertions to verify:

- five A2_02 controls still accept 0–100 values;
- a 100-value does not bypass the generation policy;
- all-high settings still produce a restrained AI-only fixture;
- high warmth does not introduce repeated endearments/love declarations;
- high intimacy increases specificity rather than vulnerable confession;
- high emotional depth increases reflection/nuance rather than adjective intensity;
- generated fixtures remain lexically sophisticated and readable;
- A2_03 analysis corresponds to the actual result fixture;
- regenerate preserves the style policy for every variant;
- no change is made to approved A2_00/A2_01/A2_02 visual geometry.

Avoid brittle tests that count one exact word such as `love`. Prefer fixture-level/content-contract assertions and review fixtures directly.

---

# Authority

For Console 2 generated-letter voice/style, use this precedence:

1. `37-ai-only-generation-style-guardrails.md`
2. later explicit user-approved generation overrides
3. `36-ai-only-a2-03-post-generation-result-plan.md`
4. `34-ai-only-post-generation-analysis-flow.md`
5. older Console 2 generation guidance

This file changes **how AI writes**, not the locked Console 2 visual system.
