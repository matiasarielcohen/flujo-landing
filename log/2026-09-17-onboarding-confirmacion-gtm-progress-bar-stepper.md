# 2026-09-17 — Onboarding/confirmacion: GTM, progress bar, stepper

### Did
- Installed the official `frontend-design@claude-code-plugins` skill (new marketplace: `anthropics/claude-code`), then disabled it right away per Mati's ask (kept off always-on, same convention as other plugins). Read its SKILL.md directly and applied it as a checklist, not a redesign brief — Flujo's existing brand in `index.html` is the actual source of truth here.
- `onboarding.html` and `confirmacion.html`: added GTM (`GTM-M924S8XC`, same container as index.html — these funnel pages had zero analytics before), the scroll progress bar, extra favicon sizes (48/96, verified files exist) + theme-color meta.
- `onboarding.html`: turned the "1·2·3" chips into a real numbered stepper (`.step-chip`, Instrument Serif digits, active step highlighted); added a lock icon next to the privacy line; added `rv-soft` staggered reveal to the checklist.
- `confirmacion.html`: added a single 3x pulse (not looping) to the "Reserva confirmada" badge dot; added `rv-soft` stagger to both checklists.
- Browser-verified both pages via Puppeteer at desktop (1280px) and mobile (390px): real GHL survey/booking iframes load, scroll progress bar tracks correctly, FAQ accordion opens/closes exclusively, no console errors, favicon links resolve to real files.

### Decisions
- Did not touch the fabricated-testimonials or GHL-survey-light-theme issues — both still open per prior session, not this task's scope.
- Kept Flujo's established motion language (fade-in + reveal-on-scroll everywhere, italic-serif accent phrases) even though the new frontend-design skill flags these as generic-AI tells in isolation — here they're the site's own consistent, deliberate signature across every page, so matching them was the correct call, not a default.

### Next
- Mati: set the GHL survey to dark theme in GoHighLevel's builder (the "rounded top/square bottom" look is the survey iframe's light theme against the dark shell — not fixable from this HTML).
- Mati: decide on testimonials (skip or provide real quotes) and fill `CONFIG.videoUrl` in confirmacion.html.
- Commit + push onboarding.html and confirmacion.html (still uncommitted).
