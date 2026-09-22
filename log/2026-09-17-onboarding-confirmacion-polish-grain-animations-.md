# 2026-09-17 — Onboarding/confirmacion polish: grain, animations, GHL theme gap

### Did
- onboarding.html: added missing `.grain` texture + `overflow-hidden` to panels (index.html has this on every panel; onboarding had it on none), added `.reveal`/`fade-in` scroll+load animations (index.html's exact CSS/JS, copied verbatim), added a new "Qué pasa después de esto" panel (3-bullet what-happens-next, reusing confirmacion.html's own real copy).
- confirmacion.html: added the same `.grain`/`overflow-hidden`/`reveal`/`fade-in` treatment to the 3 panels that lacked it (Qué vas a obtener, Cómo prepararte, FAQ) and the header/CTA.
- Verified both live via local http.server + Puppeteer screenshots (desktop + mobile) — grain, reveal, fade-in all confirmed rendering correctly, no layout breaks.

### Decisions
- Traced the "rounded top / square bottom" corner bug Mati reported: it's inside the GHL survey iframe (cross-origin, id HTHeZeXhnoH2MEcJzV9Y) — the widget is on GHL's default *light* theme, unlike the calendar widget on index.html which is already dark-themed. Can't be fixed from this HTML; needs a theme change inside GoHighLevel's survey builder. Added `overflow-hidden` to the wrapping panel anyway (matches index.html's identical calendar-panel pattern; confirmed inert/safe since the panel has no fixed height — the auto-resize script keeps wrapper minHeight in lockstep with iframe height at every step).
- Searched the whole workspace for real client testimonials (per Mati's ask to add a testimonials strip, referencing a since-deleted Kaizen funnel page for structure only, not colors). Found none anywhere (sales-flujo/records has one unfilled prospect stub, no captured quotes). Did not fabricate fake names/quotes for this live page — left testimonials out, pending real quotes from Mati.

### Open
- Testimonials strip: blocked on Mati supplying real quotes/screenshots, or explicit sign-off to skip it.
- GHL survey widget theme (light vs dark, and the internal rounded-top/square-bottom card) needs to be fixed inside GoHighLevel's own survey builder settings — outside this repo.

### Next
- Mati: fix the survey widget's theme in GHL to dark mode (matching the calendar widget) — likely resolves the corner mismatch too.
- Mati: decide on testimonials (supply real ones or confirm skip).
- Still pending from before: fill `CONFIG.videoUrl` in confirmacion.html, confirm the 2 flagged copy assumptions, then commit + push both files and set confirmacion.html as the GHL booking-confirmation redirect.
