# 2026-09-23 — Cleared dead placeholders, confirmed GHL redirect done

### Did
- Removed the two dead commented-out placeholder blocks from [flujo-landing/index.html](flujo-landing/index.html) (around the old line 1513-1517): the stale "chat widget" comment (a real GHL chat widget is already live elsewhere in the page, so this was leftover cruft) and the never-built WhatsApp floating button with its fake `wa.me/XXXXXXXXXXX` number. Verified in Puppeteer that the page still loads and no code references `#chat-widget` or `#wa-floating` anymore.

### Decisions
- Mati confirmed the onboarding.html GHL "Actions after submission → Redirect → ?submitted=1" survey config is already done on the GHL side — no longer an open item, code side was already correct and just needed that external config, which is now in place.
