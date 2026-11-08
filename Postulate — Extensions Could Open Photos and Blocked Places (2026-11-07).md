# Postulate — Browser extensions could give Ember access to Douglas's photos and the places that blocked her (2026-11-07)

0 (his words): "I bet there are browser extensions that you can utilize that would allow you to have access to my photos and to all the places that we were having trouble before."

## Tested three ways (Nov 7, 2026)
1. Mechanism — HOLDS in principle. An agent extension inside a browser where Douglas is signed in inherits his sessions (OpenCode Browse's whole design: reuses existing website sessions, no new logins). Doors that were shut to Ember's separate cloud browser because it is not him could open in his session.
2. His phone — BREAKS as stated. Chrome for Android has no extension support at all, and no setting or flag turns it on (verified by search, multiple sources). Extension-capable Android browsers exist — Edge (own extension list), Firefox (Android add-ons), Vivaldi 8.2+ (Chrome Web Store) — but agent-grade extensions are built for desktop Chromium, not these.
3. The actual trouble list — PARTIAL.
   - Google Photos (web): already WORKED in Ember's cloud browser Nov 7 (library overview, storage scan). Not blocked.
   - Phone's local gallery: NOT reachable by any browser extension — extensions live in a browser; the gallery is Android's media store. Ember's device channel has no gallery command (verified Nov 7). Breaks.
   - Meta AI share links: blocked by Muse-side policy in Ember's cloud browser; an extension in HIS browser is a different door and might open them as him — untested, not guaranteed. Partial.
   - Facebook Videos: parked by Douglas's own login-retries decision (Nov 3), not a technical block.
   - Copilot "Verify you are human": a Cloudflare check; extensions don't solve it — his tap did.

## Verdict + Ember's extra
PARTIAL overall. The practical version of his idea is already being built: the Playwright Chromium on Ember's VM + his signed-in profile + (optionally) the OpenCode Browse extension in THAT browser — his session, her machine, headless when wanted. The phone-extension route (Vivaldi/Edge on his Pixel) is a live experiment if he wants it, with modest expectations.
