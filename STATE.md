# STATE — flujo-landing

## 2026-09-23 — Cleared dead placeholders, confirmed GHL redirect done

Ran a full audit of flujo-landing for anything not-final (placeholders, empty configs, stale comments) and cleared what could be cleared: dead chat-widget/WhatsApp placeholder comments removed from index.html; onboarding.html's GHL redirect dependency confirmed configured by Mati (no longer open).
- **Still open (real, not code-fixable by me):** `[COMPLETAR: ...]` business identity (razón social/CUIT/domicilio/email) + refund claim-window days across privacy-policy.html/terms.html/refund-policy.html/cookie-policy.html — waiting on business formalization. `rueda-operaciones.html` CONFIG.leadWebhook is empty (leads go nowhere) and CONFIG.formSrc still uses the GHL widget instead of the local consent-checkbox form (rueda-formulario.html, whose own CONFIG.webhook is also empty) — Mati's call, tracked as the long-standing blocking question. confirmacion.html CONFIG.videoUrl is empty (shows "Video en camino" placeholder).
- **Next:** whenever Mati has the business formalized, fill the COMPLETAR spans; separately decide the rueda-operaciones formSrc/webhook question.
Detail: none — small cleanup, no separate log file needed.
