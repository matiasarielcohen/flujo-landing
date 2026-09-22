# 2026-09-18 — Ported hero glow, shimmer, accent panels to funnel pages

### Did
- Added index.html's animated hero treatment to onboarding.html and confirmacion.html's top hero-text block: drifting `.hero-cloud` blobs (reused index.html's `cloudDrift1/2/3` keyframes, scaled down for the narrower 760px column), the breathing `::before` radial glow (`heroBreathe`), and `.shimmer-word` applied to the key italic phrase in each H1 — all reused verbatim/adapted from index.html, not reinvented.
- Wrapped the hero text in `.hero-glow-wrap` (`overflow:hidden`, bleed padding via negative margin so layout position doesn't shift) to contain the glow — first pass caused real horizontal page overflow (scrollWidth 968 vs 900px viewport, confirmed via puppeteer `document.documentElement.scrollWidth`), fixed and reverified at 0 overflow on desktop (900px) and mobile (390px).
- Applied the accent radial-gradient wash index.html uses on its `#garantia` panel (`rgba(225,232,220,0.14)` radial + `#151515→#0a0a0a` linear) to each page's flagship panel: onboarding's "Qué pasa después de esto" and confirmacion's "Qué vas a obtener" — so not every block is flat grey, matching Mati's "colours and grading, not only the basics" ask.
- Lightened confirmacion.html's `.video-frame` nested box (was flat `#050505`) to match the new panel gradient treatment — the one flat-black box left over from the prior pass.
- Live-verified all changes via puppeteer screenshots (file:// URLs) at desktop and mobile widths on both pages; no layout breakage, no horizontal scroll.

### Decisions
- Did not transplant index.html's full 760px fixed-height `.hero-panel` (with its floating icon-bubble stat cards, play button) — it's built for the marketing hero's specific content and doesn't fit a form/confirmation page's simpler structure. Ported the ambient glow/animation *treatment* (clouds, breathe, shimmer) instead of the literal component.
- Used the bleed-padding trick (padding balanced by negative margin) on `.hero-glow-wrap` so the glow gets room to render without a hard clip edge, while keeping visible text position unchanged.
