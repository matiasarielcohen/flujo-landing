# 2026-09-23 — Onboarding post-submit confirmation message

### Did
- Added a post-submission confirmation panel to onboarding.html (`#onboardingDone`, lines 316-320): tells the visitor they'll get an email to pick a day/time for the onboarding call.
- Two detection paths wired into the existing auto-resize IIFE: guaranteed `?submitted=1` URL-param check (puppeteer-verified end-to-end: survey hides, confirmation shows, focus moves to it), and a best-effort `looksLikeSubmit()` postMessage heuristic (unit-tested in isolation, not verifiable end-to-end without live GHL infra — origin-checked so it can't be spoofed same-origin).
- Answered user's follow-up: confirmed 8/9 pages (index, rueda-operaciones, rueda-formulario, onboarding, confirmacion, + the 4 legal pages) link Privacidad/Términos/Cookies/Garantía in their footers.
- Found rueda-gracias.html has no footer/legal links at all — it's a hidden iframe bridge page (GHL redirect target), but its `#fallback` direct-visit state also has none. Flagged to user; user said it's fine as-is, no change made.

### Decisions
- Did not modify rueda-gracias.html's fallback state — user explicitly declined the offered fix, page is rarely seen directly (only via fallback link if someone loads it outside the iframe).
- Kept the postMessage heuristic as best-effort rather than presenting it as guaranteed — GHL's actual "survey submitted" postMessage contract isn't documented/confirmed for this widget type.

### Open
- rueda-operaciones.html's `CONFIG.formSrc` still points at the GHL-hosted widget, not the local rueda-formulario.html (which has the new consent checkbox) — webhook (`CONFIG.webhook`/`CONFIG.leadWebhook`) still empty either way. Unresolved, needs Mati's call.
- `[COMPLETAR: ...]` placeholders (razón social, CUIT, domicilio, email, refund claim-window days) still unfilled across all 4 legal pages + footers.
- For the guaranteed onboarding confirmation path to fire in production, GHL's onboarding survey needs "On Submit → Redirect URL" set to `https://flujo.com.ar/onboarding.html?submitted=1` — a GHL-dashboard action item for Mati, not something doable from this codebase.
- Nothing in flujo-landing has been committed yet (still all local changes).
