# 15 — Deferred Integrations

These systems are intentionally postponed. The static build should prepare interfaces but not implement production integrations.

# Hardware controls

Future source may be:

- USB keyboard-emulating arcade controls,
- serial/Arduino,
- MIDI/encoder bridge,
- another local input process.

The UI consumes semantic actions only. A future `HardwareService` converts physical events into those actions.

Do not let hardware key codes leak into screen components.

# Camera

Future requirements:

- live preview,
- capture countdown,
- three-attempt limit,
- image review,
- upload fallback for development.

Static phase uses a fixture image through the same service interface.

# Vision/handwriting extraction

Human + AI requires the machine to use the visitor's handwritten material.

Future `AiService` / vision pipeline should accept the chosen capture and return structured extracted content. UI must not assume OCR happens synchronously.

Prepare states:

- idle,
- processing,
- success,
- recoverable failure.

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

# Sentiment/emotion/romance analysis

Arcade 2 will later perform or derive:

- sentiment,
- emotion(s),
- romantic intent.

The UI should render structured labels, not parse prose model output directly.

# Printer

Printing is triggered after final stance/letter selection according to the final production flow.

Use a `PrintPayload` type now. Future service can target the selected printer implementation.

Never block the visitor on an OS print dialog.

# Email

Future email sends the chosen full letter if retained in the final product flow. UI should not own SMTP/provider logic.

# Sound

Sound design is deferred until the static experience is visually stable.

When added, create semantic events:

- navigate tick,
- confirm,
- text commit,
- capture countdown,
- generation,
- result reveal.

Do not trigger sound from arbitrary component re-renders.

# Animation

Animation is deliberately last.

Primary later motion:

- gentle stepped floating of stationery sprites,
- button press/depth collapse,
- dial tick/rotation frames,
- short window/panel appearance,
- loading meter increments.

Avoid smooth modern easing. Preserve low-frame/pixel feel.

Add `prefers-reduced-motion` handling when motion is introduced.
