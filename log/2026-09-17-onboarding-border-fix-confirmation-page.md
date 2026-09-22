# 2026-09-17 — Onboarding border fix + confirmation page

### Did
- Fixed `onboarding.html`'s form embed: replaced the ad-hoc `.form-panel` (its own border+bg+padding) with a two-layer structure matching index.html's real pattern (`.panel` outer shell + borderless `.cal-embed`-style inner wrapper), plus the same robust `[iFrameSizer]`/`highlevel.setHeight` postMessage auto-resize listener the calendar embed uses.
- Verified in-browser: the outer shell now reads as a single card like the site's calendar section. The remaining visible border around the survey fields is the GHL survey widget's own internal card styling (drawn inside the cross-origin iframe) — not fixable from this page's CSS; would need changing in the survey's own theme settings inside GHL if Mati wants it borderless like the calendar.
- Built `flujo-landing/confirmacion.html`: the post-booking confirmation page for people who complete the calendar (auditoría) booking. Sections: confirmed-badge header, video block (placeholder + `CONFIG.videoUrl` swap — tested live with a real YouTube embed URL, confirmed the JS swap works), "qué vas a obtener" (reused the real 3-numbers copy from index.html's CTA), "cómo prepararte" checklist, FAQ accordion (native `<details>`, no JS, verified toggle), CTA back to flujo.com.ar.
- Researched confirmation-page best practices via WebSearch before building (video top + written info + FAQ below is the validated pattern — source: Roezan "How To Increase Sales Call Show Up Rate").
- Decided not to install playwright-cli or any design-focused repo Mati offered — puppeteer MCP (already available) fully covered navigate/screenshot/click/evaluate verification needs this session; no gap it would have filled.
- Neither file committed yet (both still untracked, plus `onboarding.html` from last session).

### Decisions
- Video is a placeholder only — no real video link was supplied, so `CONFIG.videoUrl` in `confirmacion.html` is empty and shows a "video pendiente de cargar" state instead of an empty/broken iframe. Mati needs to paste his own embed link.
- FAQ answers about rescheduling/who-attends are reasonable generic copy, not confirmed against Flujo's actual ops — same caveat as the "kickoff call" copy flagged last session.

### Open
- `onboarding.html`'s "3-step" copy still unconfirmed (carried over from last session).
- `confirmacion.html`'s video is empty — needs a real link before this page is usable as a redirect target.
- Neither new/changed file is committed or pushed.
