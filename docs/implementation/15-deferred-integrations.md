# 15 — Deferred Integrations

This file tracks systems that remain postponed and records explicit exceptions that have now moved into current scope.

# Hardware controls

Future source may be:

- USB keyboard-emulating arcade controls,
- serial/Arduino,
- MIDI/encoder bridge,
- another local input process.

The UI consumes semantic actions only. A future `HardwareService` converts physical events into those actions.

Do not let hardware key codes leak into screen components.

The on-screen visual press/rotation feedback for Arcade 1 buttons/dial is now current scope under file `28`; **real hardware wiring remains deferred**.

# Camera

Future requirements:

- live preview,
- capture countdown,
- three-attempt limit,
- image review,
- upload fallback for development.

Current build uses a fixture image through the same service interface.

# Vision/handwriting extraction

Human + AI requires the machine to use the visitor's handwritten material.

Future `AiService` / vision pipeline should accept the chosen capture and return structured extracted content. UI must not assume OCR happens synchronously.

Prepare states:

- idle,
- processing,
- success,
- recoverable failure.

Arcade 1 now includes a fixture-driven human-letter analysis screen (`A1_06A`) showing sentiment, emotions recognized, character count and visual meaning. The **UI/data/service seam is current scope**, but production OCR/vision/model analysis remains deferred. See file `29`.

# AI generation

Two distinct generation contexts are required:

## Human + AI

Input eventually includes:

- human handwritten content/extraction,
- recipient context,
- notes,
- tuning values.

## AI-only

Input eventually includes:

- inherited recipient context,
- short prompt,
- machine analysis,
- intensity values.

Keep separate request types even if both use the same model provider.

Production generation/model calls remain deferred.

# Sentiment/emotion/romance analysis

## Arcade 1

Current scope now includes a **fixture-driven human-letter analysis UI/data model** for:

- sentiment;
- emotions recognized;
- recognized character count;
- visual meaning / visible-cue interpretation.

Production model/vision analysis remains deferred.

## Arcade 2

The AI-only experience renders fixture-driven:

- sentiment,
- emotion(s),
- romantic intent.

Production model analysis remains deferred.

The UI should render structured labels, not parse prose model output directly.

# Printer

Printing is triggered after final stance/letter selection according to the final production flow.

Use a `PrintPayload` type now. Future service can target the selected printer implementation.

Never block the visitor on an OS print dialog.

# Email

Future email sends the chosen full letter if retained in the final product flow. UI should not own SMTP/provider logic.

# Sound

## Arcade 1 exception — current scope

Arcade 1 interaction sound is now approved for implementation under `28-arcade1-motion-audio-interactions.md`.

Current Arcade 1 semantic cues include:

- CTA confirm;
- arcade-button press;
- dial tick;
- dial confirm where used;
- page transition;
- optional processing/result reveal after core review.

Use semantic events and local/WebAudio placeholder cues. No background music.

## Still deferred

- final production sound-design assets/mix;
- venue speaker calibration;
- Console 2 sound unless explicitly approved later.

# Animation

## Arcade 1 exception — current scope

Arcade 1 now permits the scoped interaction motion defined in file `28`:

- CTA press/depth collapse;
- red arcade-button press;
- dial tick/rotation frames;
- short stepped content/page transitions;
- restrained processing/result reveal;
- optional gentle stepped sprite bobbing after core feedback is approved.

Preserve low-frame/pixel feel and `prefers-reduced-motion` handling.

## Still deferred

- cinematic transitions;
- large decorative motion systems;
- Console 2 motion unless explicitly approved later.
