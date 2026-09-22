# 2026-09-16 — Added onboarding.html form page

### Did
- Created `flujo-landing/onboarding.html`: post-payment onboarding page embedding the client's GHL survey iframe (`HTHeZeXhnoH2MEcJzV9Y`) + `form_embed.js` script, unmodified from what was supplied.
- Matched site styling: same `#171817` bg, Inter + Instrument Serif fonts, heading/eyebrow pattern copied from `rueda-formulario.html`, Flujo logo header (`brand_assets/Flujo Logo Principal.svg`).
- Added a 3-step progress strip ("1 Onboarding · 2 Kickoff call · 3 Automatización en 30 días") as framing copy — this wording is my own invention, not sourced from any Flujo process doc; Mati should confirm/edit it.
- Verified in-browser via local `python -m http.server` + puppeteer: GHL form loads live and renders correctly against the dark theme, desktop (900px) and mobile (390px) screenshots both clean, no horizontal scroll.
- Not committed/pushed — working tree still has this as an untracked file.

### Decisions
- Reused `rueda-formulario.html`'s CSS variables/structure rather than inventing a new visual system, since it's the closest existing "standalone form page" precedent in this repo.
- Left the GHL iframe's internal styling untouched (white input fields) rather than trying to reskin it — GHL survey widgets carry their own inline styles from the GHL builder, not overridable from the host page's CSS.

### Open
- The "Kickoff call" / "30 días" step labels are assumed marketing copy, not confirmed against Flujo's actual post-payment process — verify before shipping.
- Page not committed to git yet.
