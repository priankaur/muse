# 12 — Accessibility and Exhibition Mode

The interface is stylized but still needs to be legible and operable in a physical exhibition context.

## Standing-distance readability

Test the real display from normal standing distance.

Requirements:

- major questions readable immediately,
- body text does not fall below the approved minimum size,
- relationship options readable without leaning into the screen,
- focus/selection visible without relying only on subtle colour shifts.

## Focus

Every interactive element has a visible focused state.

Focus must use at least one non-colour cue:

- thicker outline,
- pixel bracket/cursor,
- hard positional lift/depth change,
- marker icon.

Do not remove native keyboard focus semantics even when styling custom visuals.

## Colour

The palette uses deep navy, lavender, magenta, purple and yellow. Maintain strong enough contrast for essential text.

Decorative sprites are not information-bearing and may have lower contrast.

## Text length

Do not force long narrative copy into tiny all-caps text. The body type can use the secondary pixel/mono face and normal sentence casing.

User-generated letters should prioritize readability over strict interface type styling.

## Motion

Motion is deferred. When added later:

- avoid flashing,
- keep sprite movement slow and small,
- allow a reduced-motion mode,
- keep animation away from long reading areas.

## Kiosk/exhibition behaviour

The production shell should eventually support:

- fullscreen mode started by operator,
- no browser chrome in the visible installation,
- hidden development/debug controls,
- controlled reset after a session,
- recoverable return to attract screen,
- graceful handling of refresh/reload,
- prevention of accidental navigation outside the app.

Do not implement browser-locking hacks in the static phase; document them for deployment.

## Offline resilience

The static build should run with its bundled assets even if internet access is unavailable.

Later AI/email systems may require network access, but the UI shell and fixture mode should remain usable for exhibition testing.

## Failure states

Use the existing MUSE window style for errors such as:

- session not found,
- missing previous result,
- future camera unavailable,
- future printer unavailable.

The failure state should explain the recovery action in plain language. Do not expose stack traces or browser errors to visitors.

## Data/privacy UI

Registration/privacy copy is content and policy work that may evolve. Build a reusable notice component if needed, but do not invent retention commitments that are not approved.
