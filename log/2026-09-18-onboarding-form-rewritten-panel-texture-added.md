# 2026-09-18 — Onboarding form rewritten, panel texture added

### Did
- Rewrote onboarding.html to reflect the true post-payment story: stepper now reads Onboarding (acá) → Llamada de onboarding → Arranque del proyecto (was wrongly "Llamada de auditoría"). Replaced the "3 números" audit pitch panel with real next steps (scheduling email → onboarding call closes the 30-day cronograma → D1-3 kickoff mapping flujos). Fixed two leftover lines (survey fallback text, footer note) that wrongly assumed the call was already booked.
- Added grey/white texture to the shared `.panel`/`.panel-soft`/`.chip`/`.outer-frame`/`.step-chip` design tokens (previously near-black-on-black) across index.html, onboarding.html, confirmacion.html, and rueda-operaciones.html (token-based: --surface, --surface-soft, --line). Lighter gradient top, more visible border, subtle inset white highlight.
- Verified all 4 pages live via puppeteer screenshots (file:// URLs) — hero, proceso cards, garantía on index.html; form + stepper on onboarding.html; video/FAQ panel on confirmacion.html; rueda cards on rueda-operaciones.html. No visual breakage.

### Decisions
- Scoped the grey/white texture change to all 4 files that share the panel design tokens (per their own "copiado literal de index.html" comments), not just onboarding.html, since Mati said "my web" generally. Skipped rueda-formulario.html/rueda-gracias.html — they don't use .panel/.panel-soft.
- Kept body background pure black per Mati's wording ("apart from the black background") — only lightened the block/panel surfaces, not the page bg.

### Open
- Nothing committed yet — Mati asked to eyeball first.
