# Connection Audit — All Apps (2026-11-03)

**Audit date:** Tuesday, November 3, 2026, afternoon (America/Chicago).
**Method:** Read-only only. Each app was checked with its connector doc's documented status command and, where the status was connected, one small test read. No sign-in was attempted, no password was entered, no message, post, purchase, calendar event, playlist, or deletion was made, and nothing was sent anywhere.
**Rule applied throughout:** "Connected" means a status check returned connected. "Working" means a small read also succeeded. A connector doc alone was never treated as proof that an app works.

**Connected Google account on record:** schoonoverdouglas1@gmail.com (the only email address named in this report, because it is the already-known connected account).

## Per-app table

| App / service | Status label | One-line evidence |
|---|---|---|
| Gmail | Working | Status: connected; message list read returned data |
| Google Drive | Working | Status: connected; file list read returned data |
| Google Docs | Working | Status: connected; a known book document read returned its opening text |
| Google Sheets | Working | Status: connected; a spreadsheet read returned its properties |
| Google Slides | Working | Status: connected; Drive search found no presentations (empty, not an error) |
| Google Forms | Working | Status: connected; Drive search found no forms (empty, not an error) |
| Google Calendar | Working | Status: connected; event list read returned today's pickup reminder |
| Google Contacts | Working | Status: connected; contacts list read returned an entry |
| Google Tasks | Working | Status: connected; task-list read returned the existing task list |
| Google Keep | No connector | No Muse connector exists; see login-gated list |
| Google Photos | No connector | No Muse connector exists; see login-gated list |
| NotebookLM / Gemini | No connector | No Muse connector and no public NotebookLM API; see login-gated list |
| Facebook | Working | Profile read returned the account holder's name |
| Instagram | Working | Account list returned an account; profile read returned data |
| Messenger | Working | Connector check returned success with keys present |
| Threads | Not connected | Account list returned no accounts |
| Spotify | Working | Status: connected; device list returned the Pixel 7 Pro (inactive); now-playing: none |
| Pixel 7 Pro (paired device) | Working | Device describe: online; health, contacts, calendar, location, SMS, notifications and other permissions granted |
| Health Connect (Android) | Working | Status read: daily-metrics records synced, covering late October to November 3, 2026; sleep and workout counts zero |
| Apple HealthKit | Not connected | Status read returned zero records in every category; no iPhone source is paired (the paired phone is Android) |
| Duffel (flights) | Connected but limited | CLI help works; no user login is required by its doc; no live fare search was run in this audit |
| FlightAware | Working | Status: available via the managed service; no account to connect |
| Places | Connected but limited | CLI help works; no account to connect; no place lookup was run (none was needed for this audit) |
| Plaid (finances) | Not connected | Status: not connected, no institutions linked |
| Stripe (merchant) | Not connected | Status: not connected |
| Shop Pay (wallet) | Not connected | Connection status: not connected |
| Stripe Link (wallet) | Not connected | Connection status: not connected |
| Shopify (merchant) | Not connected | Status: not connected |
| Meta Ads | Connected but limited | Tool list returned successfully; no ad-account read was run in this audit |
| Meta Catalog search | Working | Test catalog search returned results |
| Ticketmaster | Working | Test event search returned successfully (no matching events in the test window) |
| Tailscale | Not connected | Status: not connected to a tailnet |
| 1Password | Not connected | Status: not connected |
| Secure Vault (saved website logins) | Connected but limited | Metadata only: exactly one website login is saved (see below) |

**Counts by status label:** Working: 18 · Connected but limited: 4 · Not connected: 9 · No connector: 3 · Login-gated (parked): counted separately below, not double-counted above.

## Per-app evidence notes

### Google — all nine connected apps verified working

- **Gmail** — `hatch_gws_cli gmail status` → connected. Small read (`users messages list`, 1 result) → returned data. Working.
- **Google Drive** — `drive status` → connected. Small read (`files list`, page size 1) → returned a document. Working.
- **Google Docs** — `docs status` → connected. Small read of the known Medical Elements book document → returned its opening heading and text. Working.
- **Google Sheets** — `sheets status` → connected. Small read (`spreadsheets get` on a spreadsheet found via Drive) → returned spreadsheet properties. Working.
- **Google Slides** — `slides status` → connected. No supported `presentations list` method exists in the bundled schema, so the test read was a Drive search for presentation files, which returned zero files. That is an empty account result, not a connection failure. Working (connected, no presentations found).
- **Google Forms** — `forms status` → connected. No supported `forms list` method exists in the bundled schema, so the test read was a Drive search for form files, which returned zero files. Empty result, not a failure. Working (connected, no forms found).
- **Google Calendar** — `calendar status` → connected. Small read (primary calendar, upcoming events) → returned today's Luther pharmacy pickup reminder. Working.
- **Google Contacts** — `people status` → connected. The first list attempt failed only because the API requires a fields mask (a request-format error, not an account problem); with the mask supplied, the contacts list read returned an entry. Working.
- **Google Tasks** — `tasks status` → connected. Task-list read returned the existing task list. Working.

No Google status check returned an auth error, a rate limit, or a lock signal in this audit. No Google sign-in was attempted.

### Meta / social

- **Facebook** — Profile read returned the account holder's name. Working. (This is the connector read only; it is not a browser sign-in, and no Facebook sign-in was attempted.)
- **Instagram** — Account list returned one account; a profile read returned data. Working.
- **Messenger** — Connector check returned success. No messages were read or sent in this audit. Working.
- **Threads** — Account list returned no accounts. Not connected. This matches the record that Douglas has said he has no Threads work.

### Music

- **Spotify** — `spotify-api status` → connected. Device list returned one device, the Pixel 7 Pro, marked inactive. Now-playing check returned none. No playback was started in this audit, per the task limits. Working as a connection; playback itself remains unverified (it needs an active session started in the Spotify app on the phone, as previously reported).

### Device and health

- **Pixel 7 Pro (paired device)** — Device describe returned connection state online, with permissions granted for contacts, location, calendar, SMS, call log, phone, health, photos, camera, notifications and related sources. Read-only status/permissions only; no dial, SMS, send, or dismiss action was taken. Working.
- **Health Connect** — Status read returned synced daily-metrics records covering late October to November 3, 2026, with sleep and workout counts at zero. Working (sync is flowing; sleep/workout simply have no synced records).
- **Apple HealthKit** — Status read returned zero records in every category. The paired phone is Android, so no iPhone Health source is expected. Not connected.

### Other connectors on file

- **Duffel** — Its doc states it needs no user login. CLI help works. No live fare search was run, so this is not claimed as a tested search. Connected but limited.
- **FlightAware** — Status returned available through the managed service; there is no account to connect. Working.
- **Places** — CLI help works; no account to connect. No place lookup was run. Connected but limited.
- **Plaid** — Status: not connected, no institutions linked. Not connected.
- **Stripe (merchant)** — Status: not connected. Not connected. (This is the merchant connector, separate from Stripe Link as a shopper wallet.)
- **Shop Pay** — Wallet connection status: not connected. Not connected.
- **Stripe Link** — Wallet connection status: not connected. Not connected.
- **Shopify** — Status: not connected. Not connected.
- **Meta Ads** — Tool list returned successfully, which shows the tooling is reachable through the linked Facebook account. No ad-account read was run, so no ad account is claimed as verified. Connected but limited.
- **Meta Catalog search** — Test search returned results. Working.
- **Ticketmaster** — Test event search returned successfully with no matching events in the test window. No purchase path was touched (Ticketmaster cannot buy through this connector). Working.
- **Tailscale** — Status: not connected to a tailnet. Not connected.
- **1Password** — Status: not connected. Not connected.

### Secure Vault — metadata only

The Secure Vault holds **exactly one website login: google.com** (username + password fields, shown as available). No password or username value was read, copied, or written anywhere in this audit.

**Important, unchanged from the record:** that saved google.com login is the one Google already rejected as "Wrong password" on November 2, 2026, for Keep/Photos. It was **not** retried in this audit, and it must not be silently retried — the route is for Douglas to replace it through the Secure Vault flow when he is ready. **Facebook has no saved login** in the Vault, so no Facebook autofill exists to claim.

### Browser tasks — on record only, no new windows opened

- **ChatGPT share link** — on record as readable without sign-in (November 3, 2026). Not re-opened in this audit.
- **Smule live-browser pass** — on record as completed November 3, 2026 (2:49–3:15 PM CST): 87 of roughly 1,600 profile recordings reached, ranked by plays; One Headlight not found in the portion reached and not claimed deleted. Not re-opened in this audit.

## Login-gated list — stays PARKED (do not attempt)

These items are **parked under tracked item goal_cf3cefc23093 ("Login-required retries — parked for later")** and must not be attempted, retried, or guessed until Douglas says he has remembered his logins and is ready:

1. **Google Keep note** — the "Table of Contents — All My Works" note was never created; the browser sign-in failed on the known-rejected saved login. The local text file remains as the fallback.
2. **Google Photos scan** — never entered; same rejected-login block. Connected-account-only scan when retried.
3. **Six NotebookLM short links** — contents never read; each landed on Google sign-in. No connector exists, so the retry route is the browser after Google access is restored.
4. **Facebook profile Videos listing** — no saved Facebook login exists; nothing to autofill.
5. **Microsoft Copilot chat read** — Microsoft sign-in required; no sign-in attempted.
6. **Meta AI share link (November 3)** — browser-policy blocked on the earlier attempt; content unread. Route is Douglas pasting the content or taking over the live browser himself, not a retry by Muse.
7. **Google password recovery reminder** — already scheduled separately (first run Friday, November 6, 2026, ~11:38 AM CST, every 72 hours). When Douglas confirms Google access, that reminder, its cron, and the matching recurring calendar event are to be removed, and only then are items 1–3 retried.

**No rate limit, 403, or account-lock signal was hit for any provider scope in this audit, so no scope was stopped short.** The only failed calls were request-format issues (Contacts fields mask; Slides/Forms list methods not in the bundled schema), each resolved by using the documented alternative read above.

## One next step per item that needs Douglas

- **Google (nine apps):** none — all working.
- **Facebook / Instagram / Messenger:** none — all working.
- **Threads:** none needed unless he wants Threads linked; he has said he has no Threads work.
- **Spotify playback:** open Spotify on the Pixel, press play in the app, and report what it shows; then playback can be taken over from the active session.
- **Plaid / Stripe / Shopify / Shop Pay / Stripe Link / Tailscale / 1Password:** connect only if he wants that service; none is needed for current work.
- **Login-gated items (above):** nothing until he says he has remembered his logins — then replace the saved google.com login via the Secure Vault flow first, never a password in chat, and retry Keep/Photos/NotebookLM in that order.
- **Duffel / Places / Meta Ads (limited):** no action unless he asks for a flight search, a place lookup, or an ad-account read.
