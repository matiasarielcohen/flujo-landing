# 2026-09-23 — Cookie banner now outranks chat widget z-index

### Did
- Mati flagged (with a fresh mobile screenshot) that the chat widget's proactive greeting bubble was still painting over the cookie bar's text even after the pointer-events fix — visually it looked broken even though the buttons worked.
- Root cause: the GHL `<chat-widget>`'s internal popup uses `z-index: 99999999` on a fixed-position div deep in its shadow tree, far above the banner's old `z-index: 9999`. Fixed in [flujo-landing/cookie-consent.js](flujo-landing/cookie-consent.js) by bumping the banner to `z-index: 2147483647` (max), so it now paints fully on top of the widget's popup instead of underneath it.
- Puppeteer-reverified on mobile (375×812) and desktop (1280×800): banner now fully occludes the widget's greeting bubble, Aceptar/Rechazar still resolve to the correct button (not the widget) via elementFromPoint, and accept/reject still set localStorage + GTM correctly.

### Decisions
- Went with a max z-index rather than trying to suppress/delay the widget's popup, since that's a code fix we control; changing the widget's own display timing/position is a GHL config change (Mati's call, unrelated to this bug).
