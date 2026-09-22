# 2026-09-17 — 5-agent audit + fixes: a11y, perf, mobile, design, content

### Did
- Ran 5 parallel Plan-agent reviews of onboarding.html/confirmacion.html (index.html excluded, reference-only): conversion/UX copy, accessibility, performance/technical, mobile/responsive, design-consistency-vs-index. Combined all findings and applied ~25 concrete fixes directly to both files (user pre-authorized auto-correction, no confirmation asked).
- Found two reference files at workspace root Mati had saved (`stp-call-confirmed.htm`, `The Kaizen Inner Circle...htm` — a different business's booking-confirmation and sales pages) and used their *structural* patterns (explicit prep steps, calendar-reminder nudge, no-penalty reassurance) in Flujo's own voice — did not copy their fabricated testimonials or unrelated coaching-program content.
- Accessibility: FAQ `aria-expanded`/`aria-controls`/ids (confirmacion.html), `<main>` landmark (both), `aria-hidden` on grain/decorative SVGs (both), fixed 3 failing contrast values (eyebrow/footnote/step-n alphas → 0.6), restored a visible focus ring on the survey iframe (removed a blind `outline:none`), extended `prefers-reduced-motion` to cover `.fade-in` and the badge pulse (previously only the reveal system was covered).
- Performance: added an origin allowlist to onboarding's postMessage resize listener, added a survey-iframe fallback message + 8s timeout (ad-blocker/offline case), made the scroll-progress rAF loop stop when idle instead of running forever, added a `<noscript>` reveal-system fallback (both files).
- Mobile: fixed video-placeholder text clipping at ≤375px in confirmacion.html (was clipped by a strict 16:9 box while `CONFIG.videoUrl` is empty), lowered the survey iframe's mobile default height (660→420px) to kill the blank-gap/landscape-scroll issue, shortened step-chip labels on ≤400px screens so they no longer always force 3 stacked rows, bumped the logo tap target to 44px+.
- Design consistency: `.panel` now gets index.html's 20px mobile border-radius, outer gap 7→6 to match index's real rhythm, `.rv-soft` now sets `--rv-step:70ms` (was silently falling back to a slower 90ms default), `.step-chip.is-active` border alpha 0.3→0.22, `.badge-ok` letter-spacing 0.1em→0.18em (index's actual uppercase-label constant).
- Conversion/UX: confirmacion.html's video panel no longer exposes internal dev instructions (`CONFIG.videoUrl`) to real visitors — replaced with clean "video en camino" copy, dev note moved to an HTML comment; renamed onboarding's "Kickoff call" step to "Llamada de auditoría" (was inconsistent with the rest of the funnel's terminology); demoted confirmacion's sole CTA ("Volver a flujo.com.ar") from a primary button to a plain text link since it was the only clickable thing on the page and sent leads *away* from the funnel; added a calendar-reminder nudge and a no-penalty reassurance line on onboarding.

### Decisions
- Did not fabricate: a WhatsApp contact link (no real number exists anywhere in the repo — index.html itself has it as a commented-out placeholder), a reschedule URL, or a live date/time + working "add to calendar" button (would need real GHL booking data/merge fields this session doesn't have). Flagged these to Mati instead of guessing.
- Did not switch `cdn.tailwindcss.com` → a compiled static CSS file, despite the performance agent flagging it as a real prod-safety issue. That's a build-process change affecting all 3 pages' shared design system (index.html is out of scope for edits), not a contained correction — needs Mati's call, not an autonomous one.
- Installed `frontend-design@claude-code-plugins` (prior turn) stayed disabled; only referenced its checklist, did not let it override Flujo's own established visual identity.

### Open
- Tailwind CDN→static-build migration (flagged, not done).
- No real WhatsApp number/reschedule URL/booking date data available — confirmacion.html still can't show a working calendar-add button or a real reschedule link.
- `CONFIG.videoUrl` still empty; no real testimonials exist anywhere in the workspace (unchanged from before).

### Next
- Mati: decide on the Tailwind build-step migration; provide a real WhatsApp number/link if he wants that fallback wired in; wire GHL's booking redirect params if he wants a real date/time + calendar-add button on confirmacion.html.
- Commit + push onboarding.html and confirmacion.html (still uncommitted).
