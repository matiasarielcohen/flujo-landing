# 2026-09-23 — Cookie banner removed, back to a plain footer link

### Did
- Mati rejected the whole interactive-banner approach mid-session (tried floating card → bottom bar → tiny single-line bar, each with real bugs found and fixed along the way — see prior two log entries). Final call: no banner at all, just a plain "Cookies" link in the footer next to Privacidad/Términos, exactly like the other legal pages.
- Rewrote [flujo-landing/cookie-consent.js](flujo-landing/cookie-consent.js) down to a plain unconditional GTM loader — no banner, no localStorage consent gate, no accept/reject, no `window.flujoOpenCookieSettings`.
- Removed the "Configurar cookies" footer button/link from all 4 pages that had it (index.html, onboarding.html, confirmacion.html, rueda-operaciones.html — the last one also had a JS click-handler wired to `footCookieSettings`, removed too). The plain "Cookies" → cookie-policy.html link stays untouched on all of them.
- Rewrote [flujo-landing/cookie-policy.html](flujo-landing/cookie-policy.html) section 1 (previously described the Aceptar/Rechazar banner and had a "Configurar mis cookies" button) since it no longer matched reality — removed the banner description and the essential "cookie preference" row, renumbered sections 2–6 down to 2–5, updated the meta description. GTM's table row no longer says "solo con tu consentimiento."
- Updated stale HTML comments in index.html, onboarding.html, confirmacion.html, rueda-operaciones.html that said GTM loads "solo si el visitante acepta cookies."
- Puppeteer-verified across all 4 pages: no banner, GTM's script tag actually inserted into the DOM, no leftover "Configurar cookies" buttons, "Cookies" footer link intact. cookie-policy.html screenshot-checked and reads correctly.

### Decisions
- This reverses [[flujo-landing]]'s prior documented rule in `.claude/LEGAL-A11Y-BASELINE.md` ("gate GTM behind consent, don't fire the tag before the visitor accepts") — flagged that tradeoff to Mati explicitly before making the change; he'd already been clear he wanted the cookie mechanism gone entirely, not just restyled. Did not edit LEGAL-A11Y-BASELINE.md itself — that's a workspace-wide standard for *all* Flujo sites, not just this one page's current choice; worth revisiting if this becomes the permanent policy rather than a one-off.
