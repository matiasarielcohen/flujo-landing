# 2026-09-23 — Legal, cookie consent, a11y baseline across all pages

### Did
- Added 4 legal pages: privacy-policy.html, terms.html, cookie-policy.html, refund-policy.html (dark-theme, matches site design, [COMPLETAR:] placeholders for legal name/CUIT/domicilio/email since the business isn't formalized yet).
- Added cookie-consent.js: gates GTM-M924S8XC behind Accept/Reject; wired into index.html, rueda-operaciones.html, onboarding.html, confirmacion.html (removed their unconditional GTM + noscript pixel).
- rueda-formulario.html: added required consent checkbox (linked to privacy-policy.html), validated on submit, recorded in the lead payload with a timestamp; added a legal-links footer hidden automatically in bare/embedded mode.
- Footers: added/extended on all 6 pages with Privacidad/Términos/Cookies/Garantía links + "Configurar cookies" + business-details placeholder line. onboarding.html and confirmacion.html had no footer before — now do.
- Marketing copy: fixed index.html's "sin preguntas" guarantee (contradicted the real proof-based refund policy — now says "si no cumplimos lo acordado" + links refund-policy.html), softened "número exacto" to "estimamos", labeled the "Sistema" metrics as illustrative, relabeled "En vivo" demo feed to "Simulación/Demo".
- Accessibility: fixed dead `href="#"` logo link in index.html, made rueda-operaciones.html's SVG wheel wedges keyboard-operable (tabindex/role/keydown mirroring click), bumped several rgba(255,255,255,0.35–0.45) text tokens to ~0.58–0.65 to clear WCAG AA on black.
- New standing doc: .claude/LEGAL-A11Y-BASELINE.md, linked from .claude/FACTORY.md, so future Flujo sites get this checklist applied before launch.
- Verified via a local node static server + puppeteer: cookie banner shows/hides correctly and gates GTM load, consent checkbox blocks/allows submit, wheel wedges are keyboard-focusable with correct aria-label, all 4 legal pages load, all 6 footers render their legal links.

### Decisions
- Softened the refund policy's "Flujo reserves the right to choose" into a good-faith, checklist/evidence-based evaluation clause — a pure unilateral-discretion clause is more exposed under Argentina's Ley de Defensa del Consumidor (24.240). Flagged this softening explicitly inside refund-policy.html itself.
- Did not fill business-details placeholders with invented data — user confirmed the business isn't formalized, so footers/legal pages carry visible [COMPLETAR:] markers instead.
- Did not touch rueda-formulario.html's actual wiring into the live funnel (see Open below) — switching CONFIG.formSrc is a business/CRM decision, not a copy fix.
- Left the site-wide sweep of every text-white/35–45 Tailwind utility incomplete (only bumped the ones in newly-touched sections + footers) — full pass flagged as a known follow-up, not silently dropped.

### Open
- **Important gap**: rueda-operaciones.html's lead-capture gate currently embeds the GoHighLevel-hosted form widget (`CONFIG.formSrc`), NOT rueda-formulario.html — so the new consent checkbox does not appear in the live funnel today. It only takes effect if CONFIG.formSrc is switched to `rueda-formulario.html?bare=1`, and doing that requires wiring CONFIG.webhook or CONFIG.leadWebhook (both currently empty) or leads will go nowhere. Needs a decision from Mati: add an equivalent consent checkbox inside the GHL form builder (can't be done from this codebase), or switch to the local form and wire the webhook.
- Placeholders `[COMPLETAR: ...]` for razón social, CUIT, domicilio legal, email de contacto still need real values before these pages are truly final.
- refund-policy.html's claim window ("15 días corridos") is a placeholder guess, marked [COMPLETAR/CONFIRMAR] — needs Mati's actual number.
- terms.html's jurisdiction/tribunales clause is a placeholder — needs real jurisdiction once formalized.
- Nothing committed yet — flujo-landing's own git repo still has this plus the prior uncommitted logo-swap/Tailwind-migration/WhatsApp-data changes sitting together.

### Next
- Decide the GHL-widget-vs-local-form question above (biggest open item) — that determines whether the consent checkbox actually reaches real users.
- Fill the [COMPLETAR] placeholders once business details exist, then have a lawyer glance at refund-policy.html/terms.html before calling them final.
- Decide whether/when to commit (or continue reviewing first).
