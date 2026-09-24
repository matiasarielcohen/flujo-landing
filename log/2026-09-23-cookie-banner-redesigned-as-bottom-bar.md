# 2026-09-23 — Cookie banner redesigned as bottom bar

### Did
- Rebuilt the cookie-consent banner in [flujo-landing/cookie-consent.js](flujo-landing/cookie-consent.js) from a floating rounded card to a slim, full-width bottom bar (Mati's request: "una línea abajo" instead of the floating card, which he sent a mobile screenshot of).
- Found and fixed a real bug surfaced while testing the new layout: the GHL `<chat-widget>` element renders an invisible click-catching overlay near the bottom of the viewport (worst on mobile — spans full width) that was swallowing clicks on "Aceptar"/"Rechazar". Added a small injected stylesheet (`body:has(#flujo-cookie-banner) chat-widget{pointer-events:none}`) that disables the widget's hit layer only while the cookie banner is open.
- Puppeteer-verified on both mobile (375×812) and desktop (1280×800), on index.html and rueda-operaciones.html: banner renders correctly, Aceptar sets `flujoCookieConsent=accepted` + loads GTM, Rechazar sets `rejected` + skips GTM, and both buttons are actually clickable (elementFromPoint confirms the button, not the widget, receives the click) post-fix.

### Decisions
- Kept the bar's text+buttons left-anchored (`max-width:720px`, no `margin:0 auto`, `justify-content:flex-start`) instead of spreading them edge-to-edge with `space-between`. First attempt used `space-between` across a centered 1100px container, which placed Aceptar/Rechazar right under the chat widget's corner — that's what caused the click-through bug. Left-anchoring keeps the interactive controls away from the bottom-right corner where chat widgets conventionally live, independent of viewport width.
- Fixed the widget-overlay/click problem in-flow rather than treating it as a separate "Mati decides" GHL item — it directly broke the same feature being changed (consent buttons unclickable), unlike the pre-existing formSrc/webhook question which is a genuine external product decision.

### Open
- The chat widget's greeting bubble still visually overlaps the cookie banner's text on narrow mobile viewports (cosmetic only now — buttons are unaffected since the pointer-events fix). Not fixed because it requires either delaying the widget's proactive-message timing or repositioning it, both GHL-side config changes outside this script's scope.
