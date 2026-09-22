# 2026-09-17 — Onboarding + confirmacion rebuilt to match real design system

### Did
- Fully rebuilt `onboarding.html` and `confirmacion.html` to use Flujo's actual design system, not an approximation. Extracted the real CSS classes/values verbatim from `index.html` (`.panel`, `.page-bg`, `.chip`, `.section-eyebrow`, `.section-title`, `.dim`, `.font-serif italic`, `.btn-white`, `.cal-embed`, `.faq-item`/`.faq-q`/`.faq-a-wrap`/`.faq-icon` + its accordion JS, Tailwind CDN) instead of the hand-rolled `#171817`-based palette used previously.
- Verified fidelity by screenshotting both the live `flujo.com.ar` and local `index.html` side-by-side against the new pages (FAQ section, panel gradients, eyebrow/title/dim treatment) — confirmed match, not just "close."
- Read the two reference files Mati dropped in the workspace root (`stp-call-confirmed.htm`, `The Kaizen Inner Circle...htm` — via local puppeteer screenshots, not full-text reads, since they're 600-700KB saved pages) for confirmation-page *structure* ideas only (video → confirm-the-logistics → what-you-get → FAQ). Did not copy their red/black sales-page visual style, per instruction to use them only as content reference.
- Re-verified both pages live: onboarding's GHL survey iframe still loads and auto-resizes inside the new `.cal-embed` wrapper; confirmacion's FAQ accordion toggles correctly (native site JS, single-open behavior); video placeholder→iframe swap re-tested with a real YouTube embed URL.
- Confirmed via `git diff --stat index.html` that index.html was never touched, per instruction.

### Decisions
- Reused the site's real accent tone (`rgba(225,232,220,x)`, the same sage tone used in the hero glow / A-B table's "good" dot) for the "Reserva confirmada" badge instead of inventing a green — matches the site's actual (small) accent palette rather than a generic UI-green.
- Kept FAQ question text at 16px in confirmacion.html vs the site's 20px, since this page's container (760px) is much narrower than the site's full-width panels (820-920px) — same font/weight/color system, just a proportional type-scale adjustment for the narrower layout.

### Open
- Same two content-accuracy flags as prior sessions, unresolved: onboarding's "3-step" copy (Kickoff call → 30 días) and confirmacion's FAQ specifics (rescheduling, who-attends) are reasonable copy, not confirmed against Flujo's real process.
- `confirmacion.html`'s `CONFIG.videoUrl` is still empty — placeholder state only.
- Neither file committed/pushed yet.
