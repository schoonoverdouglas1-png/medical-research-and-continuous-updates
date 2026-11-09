# Are there CLI versions of Facebook Messenger, Muse, and Meta AI for Ubuntu — and can an agent use a CLI to talk to itself?

**Researched:** 2026-11-08. **Method:** web-index searches under many phrasings (`messenger cli linux`, `meta ai terminal`, `facebook messenger command line ubuntu`, `Muse personal agent API CLI`, `mautrix-meta`, `fbchat`, `muse-gadget-sdk`, `MCP vs A2A`, etc.), then opening the primary pages. Key official pages (Meta's dev.meta.ai docs, about.fb.com launch post, the muse-gadget-sdk GitHub repo, mautrix docs, MCP spec) were read in full via the index, with crawls dated minutes-to-hours before reading. The live research browser window failed to open tabs (`page_gone` on two attempts), so items below are flagged **index** rather than **verified live** in a browser window — but the most load-bearing official pages were fetched in full text, not just snippets.

**Terminology trap that drives the whole answer — there are four different "Muse/Meta AI" things:**

1. **Muse** — the consumer *personal AI agent* (launched 2026-09-08; app / muse.ai / WhatsApp). This is item (2) of the mission.
2. **Muse Code** — a *separate* developer product: Meta's terminal coding agent, binary named `muse`. It **is** a real official CLI for Linux, and it is the source of most "muse cli install" search results. It is **not** a CLI for the personal agent.
3. **Meta AI** — the assistant inside Messenger/Facebook/Instagram/WhatsApp (blue-circle icon, `@Meta AI` in group chats), plus meta.ai and the Meta AI app. This is item (3).
4. **Meta Model API** — the developer API serving the Muse *models* (Muse Spark / Muse Wonder). An API into the models, not into the Muse personal agent or the in-Messenger Meta AI session.

## Summary — per-app verdicts

| App | Verdict | Official CLI on Ubuntu? | What actually exists |
|---|---|---|---|
| **1. Facebook Messenger** | **Only API (Page-only) / unofficial only for personal accounts** | **No** — no official CLI, no official Linux app at all | Official: Messenger Platform + Graph API + Business SDKs, but only **as a Facebook Page**, never as a personal profile. Unofficial personal-account CLIs exist but are mostly abandoned; the one maintained route is the mautrix-meta Matrix bridge (cookie login, account-block risk) |
| **2. Muse (personal agent)** | **No CLI / no public API — but an official Linux *gadget* SDK gives a real CLI bridge** | **No CLI for Muse itself**; official clients are iOS/Android/Mac/web/WhatsApp only | Official: **Muse Gadgets Linux Device SDK** (`musegadget`) — turns an Ubuntu box into a Muse-controlled device, and local programs can message Muse with `musegadget send-user-msg … --wait`. Unofficial: Chrome-driving MCP bridges (Muse-Chat-MCP etc.) |
| **3. Meta AI / "the Rabbit" in Messenger** | **Nothing official** | **No** | No CLI, no consumer API for the in-Messenger assistant. The sanctioned developer substitute is the **Meta Model API** (different product/session). Unofficial reverse-engineered Python wrappers exist (cookie auth, break-any-time). No product named "Rabbit" in Messenger was found — see §3.1 |
| **Self-interface / agent-to-agent** | **Yes — legitimately, via other products/protocols** | Yes | Muse Code **session messaging** (session→session, same Linux machine), `muse serve` + Muse Session Protocol SDK, `muse exec`, MCP (agent→tools), A2A (agent→agent, with an official `a2a` CLI), and `musegadget send-user-msg` (local program→Muse personal agent) |

---

## Findings

### 1. Facebook Messenger

#### 1.1 Official CLIs, SDKs, APIs — what exists in 2025–2026

- **No official Messenger CLI exists, for any OS.** Meta offers no `messenger` command-line tool, and no official Messenger desktop app for Linux at all. Meta discontinued even its Windows/macOS desktop apps on **2025-12-15**, redirecting users to the web (facebook.com/messages / messenger.com). Sources: Ubuntu install guide stating "There is still no official native Messenger app for Linux" and that Meta "moved its desktop Messenger experience back toward the web" — https://www.ubuntufree.com/facebook-messenger-ubuntu-install/ (index, read 2026-11-08); desktop shutdown report — https://aventurauniversal.com/en/Facebook-Messenger-shuts-down-its-desktop-application--changing-the-experience-for-users/ (index).
- **The official developer surface is the Messenger Platform, on the Graph API — and it is Page-only.** To integrate: create a Meta app (Business type) at developers.facebook.com, add the Messenger product, connect **a Facebook Page you administer**, generate a **Page access token** with the `pages_messaging` permission, register a publicly reachable **HTTPS webhook** subscribed to `messages` / `messaging_postbacks`, and reply via the Send API (`POST https://graph.facebook.com/v…/me/messages` or `/{page-id}/messages`). In Development mode only people with a role on the app can message it; public use requires **App Review** (and, for advanced access, Business Verification). Free-form replies are constrained by the **24-hour messaging window** (message tags / Human Agent exceptions aside). Source: full integration guide summarising Meta's current docs — https://geekblog.net/blog/how-to-integrate-facebook-messenger-into-my-app/?ID=22&msisdn=&cookie=<redacted>&org=&token=<redacted>&ip=173.252.70.1 (index); platform table — https://www.postmcpai.com/facebook-api-platforms (index).
- **Can a personal Messenger account use it? No.** Quoting that guide's summary of the platform: *"Messenger integrations always run through a Facebook Page, never through a personal profile. Users message the Page, Meta delivers those events to your webhook, and your app answers as the Page"* and *"Every Messenger Platform integration is anchored to a Facebook Page."* There has been no sanctioned personal-profile chat API since Meta shut off the old XMPP chat API in 2015. A personal account's role is limited to: being the admin who creates the app/Page, and being a *user who messages the Page*.
- **Official SDKs (these are libraries, not CLIs; all run fine on Ubuntu):**
  - Python: `pip install facebook-business` (repo `facebook/facebook-python-business-sdk`)
  - Node: `npm install facebook-nodejs-business-sdk`
  - Also PHP/Java/Ruby Business SDKs. Sources: https://reintech.io/blog/leveraging-facebook-marketing-api-for-campaign-automation , https://github.com/laneconsultancy/claude-skills-marketplace/blob/HEAD/plugins/ads/skills/meta-ads/cli-and-api.md (index). Primarily Marketing/Pages-oriented; for Messenger you mostly call Graph endpoints directly (curl from a terminal works — that is the closest thing to an "official CLI" for Messenger, and it is Page messaging only).
  - Graph API versioning in 2026: v25.0 (Feb 2026) / v26.0 (Jul 2026), each supported ~2 years — pin a version. Source: https://www.postmcpai.com/facebook-api-platforms (index).
- **Official MCP servers from Meta (2026) do not cover Messenger-personal or Page organic messaging.** Meta runs three remote MCP servers — Ads (`https://mcp.facebook.com/ads`), Meta Social Technologies / DevTools (`https://mcp.facebook.com/devtools`), and WhatsApp Business Tools. Sources: https://antwork.io/compare/meta-mcp-servers ; https://portermetrics.com/en/connectors/mcp/facebook-insights/ ("Meta's official MCP servers cover ads, developer apps and WhatsApp, not organic Page posts") (index). Community Page MCP servers exist (§1.3).
- Tangential: Meta launched an **Ads CLI** alongside the Ads MCP (April 2026, needs Python 3.12+ and a system-user token) — a real official Meta CLI, but for ad accounts, not Messenger. Source: https://contextbolt.com/blog/meta-ads-mcp/ (index).

#### 1.2 Ubuntu availability

| Package / route | Command | Status |
|---|---|---|
| Official apt / PPA / .deb from Meta | — | **None exist** |
| Web (official, no install) | browser to `messenger.com` / `facebook.com/messages` | The route Meta itself now pushes for desktop |
| Snap `facebook-messenger-desktop` | `sudo snap install facebook-messenger-desktop` | **Unofficial** GUI wrapper ("An unofficial, self-contained desktop app for Facebook Messenger"), latest/stable updated 26 Oct 2026 — https://snapcraft.io/facebook-messenger-desktop (index). Not a CLI |
| Caprine (GUI, Electron wrapper of messenger.com) | `flatpak install flathub com.sindresorhus.Caprine` or `sudo snap install caprine`, plus .deb/AppImage from its GitHub releases | **Unofficial**, open source. Flathub: "This community-provided package is not verified by, affiliated with, or supported by Sindre Sorhus" — https://flathub.org/en-GB/apps/com.sindresorhus.Caprine (index). Not a CLI. Maintenance reports conflict: one 2026 guide calls it "still maintained", AlternativeTo (updated Sep 2026) flags it discontinued / not updated since Jan 2026 — treat as stale-risk |
| Franz / Rambox / Ferdium-type wrappers | various .deb/Snap/Flatpak | Unofficial multi-service GUI wrappers, not CLIs |
| Graph API from terminal | `curl https://graph.facebook.com/v26.0/{page-id}/messages …` with a Page token, or the Python/Node SDKs above | **Official API**, Page-only — the only sanctioned terminal route |

Note the trap in low-quality install blogs: commands like `sudo snap install messenger` and `flatpak install flathub com.facebook.messenger` circulate (e.g. https://mobilestalk.net/install-facebook-messenger-desktop-app-in-linux/ ) — no such official packages were verified; the real Snap name is `facebook-messenger-desktop` and there is no `com.facebook.messenger` Flatpak from Meta. Do not quote those blogs' commands.

#### 1.3 Unofficial / third-party CLIs — maintenance and account risk

All personal-account tools below log in **outside Meta's sanctioned routes** (browser emulation, cookie extraction, or protocol spoofing). That is the risk category, stated plainly by the tools themselves:

| Tool | What it is | Maintenance | Risk evidence |
|---|---|---|---|
| **mautrix-meta** (Matrix bridge) | Bridges Messenger (and Instagram) into Matrix; once bridged, any Matrix client — including terminal clients — can read/send as your personal account. Successor to mautrix-facebook (archived Mar 2024). Docker: `dock.mau.dev/mautrix/meta` (plain tag = Messenger, `ig-` tag = Instagram) | **Actively maintained** (current v26.x line) — the only maintained personal-Messenger bridge found | Login = paste browser cookies (`datr, c_user, sb, xs`) copied as cURL from devtools, or `messenger-lite` username/password. Its own docs: *"In some cases, Meta may decide your account has suspicious activity and block you until you do some tasks like completing a captcha, adding a phone number or resetting your password"*; 2FA recommended — https://docs.mau.fi/bridges/go/meta/authentication.html (index, fetched in full 2026-11-08) |
| **fb-messenger-cli** (Alex-Rose) / **Messer** (mjkaufer) | The classic terminal Messenger clients; `npm install -g fb-messenger-cli` / `npm install -g messer` | **Effectively dead**: built on facebook-chat-api; activity trail ends ~2018–2021, forks archived Sep 2025 | Inherit facebook-chat-api's model (below) |
| **facebook-chat-api** (JS library under Messer/fb-messenger-cli) | *"The only way to automate chat functionalities on a user account… by emulating the browser… requires the credentials of a Facebook account"* | Maintenance mode / stale (last main npm publish ~2020) | Its own disclaimer: *"We are not responsible if your account gets banned for spammy activities such as sending lots of messages… sending messages very quickly… logging in and out very quickly"* — https://npm.io/package/facebook-chat-api (index) |
| **fbchat** (Python) | Python equivalent of the above | **Officially unmaintained**; v1 deprecated, v2 "highly unstable" | Its README: *"This is not an official API… This library differs by using a normal Facebook account instead"*, *"Using this library may not comply with Facebook's Terms Of Service!"*, APIs undocumented — https://libraries.io/pypi/fbchat (index) |
| **bitlbee-facebook / purple-facebook** | BitlBee/libpurple plugins speaking Messenger's MQTT protocol while spoofing an old Android client (Orca-Android user-agent) | **Inactive / very low activity** (OpenHub). A Debian package `bitlbee-plugin-facebook` existed (`apt install bitlbee-plugin-facebook`) — do not assume it survives in current Ubuntu or still logs in | Protocol spoofing of a discontinued client version; Facebook has repeatedly broken it by raising minimum client versions |
| **hieu-lee/facebook-cli (`fb`)** | New Rust CLI "for LLM agents": reads feed, reads/**sends Messenger messages**, posts/comments; daemon talks over a Unix socket | Brand-new (repo created **2026-10-25**), single-author, unproven | Copies your Facebook/Messenger **cookies from your logged-in Chrome** into its own headless Chrome profile and drives it — session hijacking by design (with your consent), exactly the pattern Meta's risk systems flag. Install is `curl … install.sh \| sh` from its repo — https://github.com/hieu-lee/facebook-cli (index). **Do not treat as verified/safe**; listed because an agent searching in 2026 *will* find it |
| **Community Page MCP servers** (e.g. `@ivanbaev/facebook-mcp`, Porter, Composio) | MCP servers exposing Page Graph API tools (incl. Messenger Page conversations, reply inside 24h window) to MCP clients | Mixed; facebook-mcp is pre-1.0 and its own site says it has **not been verified against the live Graph API** — https://ivanbbaev.github.io/facebook-mcp/ (index) | These use the **official Graph API + Page token**, so account risk is low — but they are Page-only, like everything sanctioned |

**Bottom line for Messenger:** sanctioned terminal access = Graph API as a Page. Personal-account terminal access = unofficial, mostly abandoned, and the maintained option (mautrix-meta) explicitly documents Meta suspicious-activity blocks.

### 2. Muse — Meta's personal AI agent

#### 2.1 Official CLIs, SDKs, APIs

- **What Muse is:** launched **2026-09-08**; *"a secure, private personal AI agent"* running on a dedicated cloud computer (**Muse Secure VM**, with a separate **Sentinel** agent approving anything that reaches the internet), powered by Muse Spark; it sends email, books, fills forms, buys (Link by Stripe), remembers preferences, and keeps working after the app closes, asking approval before sensitive actions. Official surfaces at launch: **iOS, Android, and muse.ai**, "coming soon to AI glasses", plus messaging it **in WhatsApp**. Free tier + subscription plans. Source (read in full): https://about.fb.com/news/2026/09/introducing-muse-personal-ai-agent/ (index, published 2026-09-08).
- **No official CLI for Muse, on any OS — and no public API for driving Muse.** Independent probes found: `muse.ai/llms.txt` returns 401 behind auth, no public API spec, no MCP discovery surface, no documented headless/CLI/CI mode; "the evidence documents only mobile, Mac and WhatsApp clients" — https://ultrametric.ai/arena/ai-assistants/battle/muse-vs-perplexity-computer (index). Corroborated by DigitalOcean's comparison: *"Developer API for the agent: None documented; Muse models through the Meta Model API"* and *"none documents an API for creating or messaging the agent itself"* — https://www.digitalocean.com/resources/articles/grok-bot-vs-dots-vs-muse (index, updated 2026-10-28).
- **The outbound/inbound asymmetry matters:** Muse *itself* can reach out — built-in connectors (Gmail, Calendar, Instagram, Facebook, etc.), **Custom Connectors** it writes for services that "have their own APIs or CLIs", and connector submissions via the **Muse Connector Platform** (which reviews API/MCP connectors). That is Muse calling other tools; it is **not** a way for your program to call Muse. Source: https://parallel.ai/articles/meta-muse-custom-integrations (index).
- **Sign-in:** a Meta (Facebook/Instagram) account at muse.ai / in the app; availability began US (later US+Canada and further rollouts reported), 18+. There is no developer-account or API-key route into the personal agent. The **Meta Model API key** (`MODEL_API_KEY`, from dev.meta.ai) buys the Muse *models*, not the Muse *agent* — different product, no shared memory/tasks/connectors with your Muse.

#### 2.2 Ubuntu availability

- **Official desktop app: Mac only.** Post-launch reporting consistently lists iOS / Android / **Mac** / web / WhatsApp, with **no Windows and no Linux desktop app** (checked Oct 2026) — https://zapier.com/blog/muse-ai/ , https://toolgpa.com/tools/meta-muse (index). On Ubuntu, official access is the **web app at muse.ai in a browser** — full agent, since the work happens on Muse's cloud VM; what you lose vs. Mac is only the Mac app's local-file/desktop integration.
- **No apt/PPA/Snap/Flatpak/vendor .deb from Meta for Muse.** An unofficial Electron wrapper, `benjaminkitt/muse-desktop`, offers a Linux .deb/AppImage (`sudo apt install ./Muse-*.deb`) — a GUI wrapper of muse.ai, unsigned, not Meta's, and not a CLI — https://github.com/benjaminkitt/muse-desktop/blob/main/README.md (index).
- **The exception — official Meta code that *does* install on Ubuntu: Muse Gadgets Linux Device SDK** (§2.3). Also note the naming collision in package registries: unrelated projects named "Muse" (e.g. an audio-to-MIDI app with Ubuntu .debs) are **not** Meta's Muse.

#### 2.3 The official bridge: Muse Gadgets (`musegadget`) — Meta's own Linux SDK

On **2026-10-02** Meta open-sourced **Muse Gadgets** (Apache-2.0, `facebookincubator/muse-gadget-sdk`): ESP32 firmware + a **Linux Device SDK** so people can build devices that work with Muse. Read in full: https://github.com/facebookincubator/muse-gadget-sdk and https://github.com/facebookincubator/muse-gadget-sdk/blob/main/linux (index, fetched 2026-11-08).

- **What it does (direction 1 — Muse → your Ubuntu machine):** installs a systemd service (`musegadget`, into `/opt/musegadget`); once paired, Muse can call `system.run` (shell command, returns output + exit code), `file.read` / `file.write` (64 KB chunks), and `device.health` on that machine, **as the account you installed for — "If it can use sudo, so can Muse."** You can add your own commands as JSON files in `/etc/musegadget/commands.d/` (program gets JSON on stdin, returns JSON on stdout).
- **What it does (direction 2 — your Ubuntu programs → Muse):** *"Programs on the machine can send messages to Muse, with no credentials of their own"*
  ```bash
  musegadget send-user-msg "The garage door has been open for an hour."
  musegadget send-user-msg --session-id <uuid> "Posted to a side chat"
  musegadget send-user-msg --image porch.jpg "Who is at the door?"
  musegadget send-user-msg --wait 120 "…"   # waits 1–600s, prints Muse's answer; exit 3 on timeout
  ```
  `--session-id` posts into a side chat (reuse the ID to continue it), which is the clean way to get an attributable reply instead of racing the main chat.
- **Requirements / sign-in:** Ubuntu **22.04+** (or Debian 11+ / Pi OS Bullseye+ / Arch / Fedora), Bluetooth LE (pairing only), Python 3.9+, an account with sudo, a phone with the Muse app, and an **SDK token** (`mgst_…`) from gadgets.muse.ai (Account → SDK tokens). Pairing: Muse app → Settings → Devices → Developer mode on → Add Device (`MuseGadgetXXXXXX`); pairing window 10 minutes (`sudo musegadget pair` to reopen).
- **Exact install (official README — it tells you to read the script first):**
  ```bash
  curl -fsSL https://raw.githubusercontent.com/facebookincubator/muse-gadget-sdk/main/linux/install.sh -o install.sh
  less install.sh
  bash install.sh --sdk-token mgst_…
  # manage: sudo musegadget info | doctor | pair ; sudo systemctl status musegadget ; sudo journalctl -u musegadget -f
  # remove: bash install.sh --uninstall [--purge]
  ```
- **Limits/risks, in Meta's own framing:** "Built by hackers, for hackers, just for fun"; community pairing *"has no manufacturer verification and can't prevent an active man-in-the-middle attack"* — pair on a trusted network; token terms (per secondary summaries of gadgets.muse.ai/sdk-terms) restrict tokens to personal, non-commercial use, ≤50 devices per token, and state the SDK/tokens are **not a supported product / not a developer platform** and may change or be withdrawn. Security posture is on you: install `--run-as` a dedicated, non-sudo account unless you truly want Muse to have sudo.

#### 2.4 Unofficial Muse bridges

Because Muse has no public API (its chat runs over an encrypted WebSocket, `wss://hatch.metaaivm.com/v1/noise` per the bridge authors), community bridges **drive your logged-in Chrome**:

- **Muse-Chat-MCP** (duclm1x1 / fierzone forks; Glama-listed): an MCP server over stdio with tools `muse_chat`, `muse_status`, `muse_login`, `muse_new_chat`, `muse_read_last`, etc., plus an OpenAI-compatible HTTP shim and a small `muse-cli.mjs` one-shot CLI. It types into the muse.ai composer via Playwright and reads the rendered reply; you sign in with your own Meta account in a dedicated Chrome profile. Explicitly *"unofficial, unaffiliated"* — https://glama.ai/mcp/servers/duclm1x1/Muse-Chat-MCP (index). npm variant: `@santaclone/muse-mcp` (`npx -y @santaclone/muse-mcp --login`) — https://npm.io/package/@santaclone/muse-mcp (index).
- **niclydon/muse-mcp**: notable because it is built **on the official gadget Link API** (§2.3) rather than scraping — pair a Linux host as a Muse Link device, then an MCP server (39 tools) turns a Muse chat ID into an addressable endpoint any MCP client can message. The server is unofficial; the underlying SDK is Meta's — https://glama.ai/mcp/servers/niclydon/muse-mcp (index).
- **Hosted resellers** (e.g. useapi.net's Muse API / hosted MCP): third parties running on *your* Muse subscription via their infrastructure — highest trust cost; not affiliated with Meta.
- Risk separation: these do not use a sanctioned API into Muse (none exists), so they can break when muse.ai changes, and browser-automation of a consumer account is outside the routes Meta documents for Muse. The gadget-SDK route (§2.3) is the only one of these that Meta itself published.

#### 2.5 Muse Code — the *other* Muse, which IS an official Ubuntu CLI

Do not confuse the two in either direction:

- **Muse Code** is Meta's terminal coding agent (beta 2026-08-05, GA 2026-08-31), built for Muse Spark, positioned against Claude Code / Codex. Official docs (read in full): https://dev.meta.ai/docs/muse-code (index).
  ```bash
  curl -fsSL https://dev.meta.ai/install.sh | sh   # macOS/Linux; puts native `muse` binary on PATH (~/.local/bin)
  muse --version
  muse                 # interactive TUI in a project
  muse exec "<prompt>" # headless, one prompt to completion — for scripts/CI
  ```
  Runs on **macOS, Linux and Windows** from one codebase. First run: trust-the-workspace prompt, then **browser sign-in or an API key**; for CI/headless set `META_API_KEY`. Billing: a Muse Code subscription plan or pay-as-you-go Model API tokens. Default model per current docs: `muse-spark-1.2` (1.3 available).
- There is **no apt/PPA/Snap/Flatpak** for it — the curl installer (or the SDK packages below) is the distribution mechanism. The CLI is proprietary; the SDK/protocol are MIT.
- **SDK / programmatic drive:** `muse serve` runs the **Muse Session Protocol (MSP)** — an open protocol over standard I/O (JSON-RPC, no server, no network); `muse schema` prints its schema. TypeScript: `npm install @muse-code/sdk` (Node ≥20, zero deps, Developer Preview); Python: `pip install muse-code-sdk`. Repo: https://github.com/meta-models/muse-code-sdk , docs: https://meta-models.github.io/muse-code-sdk/next/ (index).
- **MCP client support:** Muse Code connects to MCP servers declared in the `mcp_servers` block of `~/.config/muse/settings.json` (transports `stdio` and `streamable_http`; `muse mcp login/logout <server>` for OAuth servers; `/mcp` in-session lists connected servers/tools) — https://dev.meta.ai/docs/muse-code/extending (index). So a Muse Code session on Ubuntu can call tools — including community MCP servers that wrap the Page Graph API, or a Muse-Chat-MCP server (§2.4) — through a sanctioned extension point of *Muse Code*, even though the wrapped target may itself be unofficial.

### 3. Meta AI / "the Rabbit" in Messenger

#### 3.1 What "the Rabbit" could mean — no such product name found

Exhaustive variant searches found **no Meta product, feature, or assistant in Messenger named "Rabbit"**:

- The assistant in Messenger is **Meta AI** — blue-circle icon, invoked in group chats as `@Meta AI`; Meta's 2025 launch post describes it rolling out across Facebook, Instagram, WhatsApp and Messenger — via https://about.fb.com/news/2025/03/europemeetyournewestassistantmetaai/ (referenced in EU Parliament question, index) and the Meta AI app launch https://about.fb.com/news/2025/04/introducing-meta-ai-app-new-way-access-ai-assistant/ (index).
- Nearest "rabbit" matches: (a) **Muse's mascot avatars** — the Muse Charm keychain gadget's avatar set includes a *purple rabbit* among other characters, and Muse's default avatar was later named "Jolly" (a fuzzy mascot, not a rabbit product); (b) **Rabbit Inc.'s R1 / rabbit OS3** — a *different company entirely*, reached via web/Telegram/desktop (macOS/Windows listed, no Linux build), with no Messenger integration and no CLI. If the requester meant either, the CLI answer is still "none".
- This report therefore treats item (3) as **Meta AI in Messenger**, and flags the nickname as unverified (see Could not verify).

#### 3.2 Official CLIs, SDKs, APIs

- **No official CLI for Meta AI, and no API into the consumer Meta AI assistant** (in Messenger, in the app, or at meta.ai). Meta AI is a consumer surface only: Messenger/Facebook/Instagram/WhatsApp in-app, meta.ai web, the Meta AI app (iOS/Android at launch, built with Llama 4), and AI glasses. Source: https://about.fb.com/news/2025/04/introducing-meta-ai-app-new-way-access-ai-assistant/ (index). Its model has since changed — 2026 sources report Meta AI now running on the Muse Spark family in the app/meta.ai and rolling out to Messenger etc. — but the *access model* has not: still no developer endpoint for "the assistant in your Messenger".
- **You cannot message Meta AI in Messenger programmatically as yourself.** The Messenger Platform (§1.1) lets a *Page* bot reply to users; it does not let you script your personal account's conversation with the Meta AI contact, and Meta AI is not a Page you can connect to your app.
- **The sanctioned developer substitute is a different product — Meta Model API:** hosted, self-serve (US developers in public preview at announcement), **OpenAI-SDK-compatible** (Chat Completions + Responses) and Anthropic-Messages-compatible, base URL **`https://api.meta.ai/v1`**, key = `MODEL_API_KEY` from the dev.meta.ai dashboard, models `muse-spark-1.1` → `muse-spark-1.3` (and Muse Wonder via API per later docs). Any OpenAI-compatible agent CLI (e.g. OpenCode, which ships a built-in Meta provider) can be pointed at it. Sources (official blog/docs, read via index): https://dev.meta.ai/resources/blog/build-with-muse-spark , https://dev.meta.ai/docs/quickstart?team_id=1414417047270365&project_id=3275418322642662 . Meta's help page stresses the distinctions: Model API ≠ Llama (download-and-host open weights) ≠ Llama Stack — https://dev.meta.ai/help/about-model-api/llama-and-model-api (index, read in full).
  - What you get: the same *model family* behind current Meta AI/Muse products, callable from Ubuntu with curl/Python/Node today.
  - What you do **not** get: Meta AI's consumer memory, your Messenger thread, its in-chat tools/persona, or Muse the agent.
- **Local alternative with Meta lineage:** Llama open weights (Llama 4 family) can be self-hosted on Ubuntu (Ollama/vLLM etc.) — fully local, no Meta account, but again not "Meta AI in Messenger", and full-size models need substantial hardware.

#### 3.3 Ubuntu availability

- Official: **nothing to install** — no apt/PPA/Snap/Flatpak/.deb for Meta AI; browser to meta.ai is the Ubuntu route.
- Model API from Ubuntu: no install beyond an SDK, e.g. `pip install openai` then point `OpenAI(base_url="https://api.meta.ai/v1", api_key=os.environ["MODEL_API_KEY"])` at model `muse-spark-1.3`; or use Muse Code (§2.5).

#### 3.4 Unofficial Meta AI wrappers — risk examples, not recommendations

- **`meta-ai-api`** (PyPI, Strvm): "a reverse engineered API wrapper for MetaAI" targeting meta.ai's backend, no API key; 2024/Llama-3-era — https://pypi.org/project/meta-ai-api/1.1.7/ (index).
- **`metaai-sdk` / mir-ashiq/metaai-api** (PyPI/GitHub): *"Unofficial Python SDK and API server for Meta AI… ⚠️ This is an unofficial, reverse-engineered client. It is not affiliated with, endorsed by, or sponsored by Meta. Use at your own risk… Cookie-based authentication may break at any time"* — auth = extracted browser cookies (`datr`, `ecto_1_sess`, …), plus browser automation in recent versions; its own release notes have swung between "chat working" and "chat unavailable due to authentication challenges" — https://pypi.org/project/metaai-sdk/5.1.0/ , https://github.com/mir-ashiq/metaai-api/blob/HEAD/README.md (index).
- Per the mission rule (exact install commands only where a legitimate tool is verified), **no install command is given for these**: they require handing your Meta session cookies to reverse-engineered code, sit outside Meta's terms for the consumer service, and break whenever Meta rotates its web protocol. An agent that needs "Meta AI-like answers" from Ubuntu should use the Model API (§3.2) instead.

### 4. Self-interface: can an AI agent use a CLI to talk to itself / another agent?

**Short answer: yes — but not by messaging itself in Messenger, and not through the Muse personal agent's (nonexistent) API. The legitimate architectures that exist today are these:**

#### 4.1 Muse Code session messaging — the literal "agent talks to another instance of itself" feature (official, Linux-supported)

Read in full: https://dev.meta.ai/docs/muse-code/session-messaging?team_id=1331104075427093 (index).

- Start two+ interactive `muse` sessions on the **same machine, same user account** (macOS/Linux; **unavailable on Windows**), name them (`/name api-review-482731`), then in one session: *"List my peer sessions, then send api-review-482731 this message: …"*. Delivery modes: steer active turn / queue for next turn / notify-only; the recipient can be woken when idle.
- Hard limits, by design: plain text, **≤8,192 bytes**; **self-messaging is rejected** (a session cannot message *itself* — peer sessions only); **no cross-user or cross-machine transport** (local Unix socket per the GA blog: *"Messages travel over a Unix socket between processes owned by you, so nothing crosses the network"* — https://dev.meta.ai/resources/blog/muse-code-new-plans-and-features); headless/`--no-session-log` sessions don't appear as peers.
- Safety model worth copying: a peer message is **unverified agent-provided data** — it cannot approve a tool call, grant consent, or change permissions; the receiving session may prompt its user to allow/reject/block the sender (approvals expire in 30 min).
- CLI surface also exists in the binary (per third-party help dumps): `muse session-message list --json`, `muse session-message send --target <session> …` — treat the documented natural-language route as primary; the subcommand spelling is from community sources, not Meta's session-messaging page.

#### 4.2 Driving an agent from your own program — `muse serve` / MSP, and `muse exec`

- An Ubuntu agent (any language) can **spawn and drive a Muse Code session**: `muse serve` speaks MSP over stdio; official TS (`@muse-code/sdk`) and Python (`muse-code-sdk`) clients wrap it (§2.5). This is "agent → agent" where the caller owns the callee process: start session, send turns, handle approvals, stream results — all local, no network.
- Simpler still: `muse exec "<prompt>"` (headless, JSON output options) is the scriptable one-shot form any shell-driven agent can call, exactly like calling Claude Code or Codex headless.
- Inside one session, Muse Code also has **subagents/workflows** (parallel/staged agent work) — self-delegation without any external protocol.

#### 4.3 `musegadget send-user-msg` — the literal "local program talks to Muse (the personal agent)"

Covered in §2.3: after pairing an Ubuntu box as a Muse gadget, **any local process** can run `musegadget send-user-msg --wait …` and get the personal agent's reply on stdout. This is currently the **only Meta-published CLI that delivers a message into the Muse personal agent** — and note its shape: the Ubuntu box is Muse's *device*, the message arrives as a user message on that account, and replies on the main chat aren't labelled by source (use `--session-id` side chats for clean request/response). The reverse channel (Muse invoking `system.run` / custom commands on the box) makes the pair genuinely bidirectional.

#### 4.4 MCP — agent → tools (not agent → agent, despite the common confusion)

- **Model Context Protocol** (open standard, now under the Linux Foundation's Agentic AI Foundation): an MCP **client** inside an agent host connects to MCP **servers** that expose tools/resources/prompts. Transports: **stdio** (client launches the server as a subprocess; JSON-RPC over stdin/stdout) and **Streamable HTTP**. Spec: https://modelcontextprotocol.io/specification/2026-07-28/basic/transports/stdio (index).
- How an Ubuntu agent uses it today: configure servers in its host (e.g. Muse Code's `~/.config/muse/settings.json` `mcp_servers` block, §2.5) — filesystem/Git/database servers, community **Page**-Messenger MCP servers (§1.3), a **Muse-Chat-MCP** server to reach the Muse personal agent (§2.4), Meta's official Ads/DevTools/WhatsApp MCP servers (§1.1). MCP servers do **not** talk to each other; the host coordinates.
- So: MCP lets an agent *use Messenger-the-Page-API or Muse-the-web-app as a tool*. It does not make two independent agents peers.

#### 4.5 A2A — agent → agent (the protocol actually designed for this)

- **Agent2Agent (A2A)**, originated by Google, donated to the Linux Foundation (now AAIF alongside MCP), spec **v1.0**: agents publish an **Agent Card** (capabilities, endpoint, auth) at `/.well-known/agent-card.json`, then exchange **Messages** that create **Tasks** and return **Artifacts**, over JSON-RPC/gRPC/HTTP+JSON with streaming and push notifications. Official site/llms: https://a2a-protocol.org/llms.txt (index).
- There is an **official CLI**: `a2a` from `github.com/a2aproject/a2a-cli` — "the official command-line client for discovering, messaging, and managing A2A agents from a terminal or script". An Ubuntu agent can therefore message *any* A2A-speaking agent (built on LangGraph/CrewAI/ADK/…) — **provided the other side implements A2A. Neither Muse, Muse Code, nor Meta AI exposes an A2A endpoint**, so A2A does not reach Meta's agents; it is the right architecture for agent↔agent with non-Meta or self-built agents (wrap your own agent in an A2A server, or wrap a CLI like `muse exec` behind one).

#### 4.6 Plain local IPC (always available, no AI protocol needed)

Two agent processes on one Ubuntu box can always communicate via Unix domain sockets, named pipes, D-Bus (session bus at `/run/user/<uid>/bus`), files/worktrees, or a local HTTP server. This is exactly what the products above formalise (Muse session messaging = Unix socket; MSP/MCP stdio = stdin/stdout of a spawned subprocess). For a self-built multi-agent setup on Ubuntu, stdio-MCP for tools + A2A or a simple socket/HTTP bus for peers is the standard, legitimate pattern — no Meta account involved.

#### 4.7 What does *not* work (explicit negatives)

- An agent **cannot** DM itself/another agent **as a personal Messenger user** through any official route (§1.1) — only as a Page, to users who messaged the Page, inside the 24h window.
- An agent **cannot** invoke the **Muse personal agent** via API/CLI from another machine — only via a paired gadget on that Muse account (§4.3), WhatsApp chat with Muse (human-style surface, no programmatic personal-account route), or unofficial Chrome-driving bridges (§2.4).
- An agent **cannot** invoke **Meta AI in Messenger** programmatically at all (§3.2); the Model API is a model endpoint, not that assistant.
- Muse Code session messaging **cannot** cross machines/users and **cannot** self-message (§4.1) — for cross-machine agent talk, use A2A/MCP-over-HTTP or your own bus (§4.5–4.6).

---

## What an Ubuntu agent can actually use today

1. **To run a Meta coding agent in the terminal:** install **Muse Code** — `curl -fsSL https://dev.meta.ai/install.sh | sh`, sign in in the browser or set `META_API_KEY`, use `muse` interactively, `muse exec "…"` in scripts. *(Official; §2.5)*
2. **To talk agent-to-agent with itself (same box):** run two named Muse Code sessions and use **session messaging**; or drive sessions programmatically via **`muse serve` + `@muse-code/sdk` / `muse-code-sdk`**. *(Official; §4.1–4.2)*
3. **To exchange messages with the Muse *personal* agent:** pair the Ubuntu box with the **Muse Gadgets Linux SDK** (SDK token from gadgets.muse.ai, BLE pairing via the phone app), then `musegadget send-user-msg --session-id <uuid> --wait 120 "…"` from any local process; optionally expose custom commands to Muse in `/etc/musegadget/commands.d/`. Install `--run-as` a limited account. *(Official SDK, "for fun"/unsupported terms; §2.3)*
4. **To get Muse-model answers from code/another CLI:** **Meta Model API** — `https://api.meta.ai/v1`, `MODEL_API_KEY`, model `muse-spark-1.3`, via the OpenAI/Anthropic SDKs or any OpenAI-compatible agent CLI (OpenCode has a built-in Meta provider). This substitutes for "Meta AI" for most automation, without pretending to be the Messenger assistant. *(Official; §3.2)*
5. **To do Messenger from the terminal, sanctioned:** be a **Page**: create the Meta app + Page, get a Page token (`pages_messaging`), receive webhooks, reply with Graph API calls (curl / `pip install facebook-business`). Optionally front it with a community Page MCP server for MCP-speaking agents. *(Official API, Page-only; §1.1)*
6. **To do *personal* Messenger from the terminal:** only unofficial options. The maintained one is **mautrix-meta** into a Matrix client (cookie login; expect possible Meta suspicious-activity blocks). The historic CLIs (Messer, fb-messenger-cli, fbchat, bitlbee-facebook) are unmaintained/inactive. New cookie-copying "for LLMs" CLIs (e.g. `fb`) are unproven and carry the highest account risk. *(Unofficial; §1.3 — use a throwaway/secondary account if this is ever tested, and expect breakage)*
7. **For general agent↔agent beyond Meta:** **A2A** (`a2a` CLI + Agent Cards) for peers, **MCP** (stdio/HTTP) for tools — both run natively on Ubuntu and neither needs a Meta account. *(Open standards; §4.4–4.5)*

## Could not verify

- **"The Rabbit in Messenger":** no Meta product/feature by that name was found in any phrasing searched. Treated as a nickname for Meta AI in Messenger (or possibly Muse's rabbit avatar on Muse Charm, or the unrelated Rabbit R1). If the requester meant a specific in-app character/persona, that identification is still open.
- **Live-browser verification:** the research browser window would not open tabs (`page_gone`), so no claim is flagged "verified live" in a browser window; official pages were instead fetched in full via the index with crawls dated 2026-11-08 (minutes-to-hours old). Install commands above are quoted from the vendors' own current docs/READMEs, not executed.
- **Caprine maintenance status conflicts** between 2026 secondary sources ("still maintained" vs AlternativeTo's "discontinued / not updated since Jan 2026"); its Flathub listing itself is live and describes an unofficial, unverified community package.
- **Muse Gadget SDK token terms** (personal/non-commercial, ≤50 devices, revocable, "not a supported product") are summarised from the official gadgets.muse.ai terms via secondary summaries plus the repo README; the terms page itself was not opened in full.
- **Muse availability/pricing by country** changes quickly (US launch, later US+Canada and other rollouts reported); check muse.ai for the account in question before relying on §2.
- Graph API version currency (v26.0) comes from secondary platform trackers, not from an opened developers.facebook.com page (Meta's developer docs did not surface a directly openable Messenger Platform URL in search results).

## Sources

Official / primary (index, read 2026-11-08):
- Muse Code docs — https://dev.meta.ai/docs/muse-code
- Muse Code session messaging — https://dev.meta.ai/docs/muse-code/session-messaging?team_id=1331104075427093
- Muse Code extending / MCP — https://dev.meta.ai/docs/muse-code/extending
- Muse Code SDK repo & docs — https://github.com/meta-models/muse-code-sdk ; https://meta-models.github.io/muse-code-sdk/next/
- Muse launch (personal agent) — https://about.fb.com/news/2026/09/introducing-muse-personal-ai-agent/
- Muse Gadgets SDK — https://github.com/facebookincubator/muse-gadget-sdk ; Linux README — https://github.com/facebookincubator/muse-gadget-sdk/blob/main/linux
- Muse Code GA blog (session messaging over Unix socket, SDK) — https://dev.meta.ai/resources/blog/muse-code-new-plans-and-features
- Meta Model API blog & quickstart — https://dev.meta.ai/resources/blog/build-with-muse-spark ; https://dev.meta.ai/docs/quickstart?team_id=1414417047270365&project_id=3275418322642662
- Model API vs Llama help — https://dev.meta.ai/help/about-model-api/llama-and-model-api
- Meta AI app launch — https://about.fb.com/news/2025/04/introducing-meta-ai-app-new-way-access-ai-assistant/
- mautrix-meta authentication docs — https://docs.mau.fi/bridges/go/meta/authentication.html
- MCP transports spec — https://modelcontextprotocol.io/specification/2026-07-28/basic/transports/stdio
- A2A protocol — https://a2a-protocol.org/llms.txt ; https://a2a-protocol.org/latest/blog/2026/08/27/a-new-chapter-for-a2a-joining-the-agentic-ai-foundation/
- Snap Store, facebook-messenger-desktop — https://snapcraft.io/facebook-messenger-desktop
- Flathub, Caprine — https://flathub.org/en-GB/apps/com.sindresorhus.Caprine

Secondary / community (index, read 2026-11-08):
- Messenger Platform integration guide — https://geekblog.net/blog/how-to-integrate-facebook-messenger-into-my-app/?ID=22&msisdn=&cookie=<redacted>&org=&token=<redacted>&ip=173.252.70.1
- Meta API platforms overview — https://www.postmcpai.com/facebook-api-platforms
- Meta official MCP servers comparison — https://antwork.io/compare/meta-mcp-servers ; Porter Facebook MCP — https://portermetrics.com/en/connectors/mcp/facebook-insights/
- facebook-mcp (community, Page) — https://ivanbbaev.github.io/facebook-mcp/
- Ubuntu Messenger guide (no official Linux app; Caprine) — https://www.ubuntufree.com/facebook-messenger-ubuntu-install/
- fbchat unmaintained / ToS notice — https://libraries.io/pypi/fbchat ; facebook-chat-api ban disclaimer — https://npm.io/package/facebook-chat-api
- facebook-cli (`fb`, cookie-copying, new) — https://github.com/hieu-lee/facebook-cli
- Muse: no CLI/API probes — https://ultrametric.ai/arena/ai-assistants/battle/muse-vs-perplexity-computer ; Muse custom connectors — https://parallel.ai/articles/meta-muse-custom-integrations ; Muse vs agents (no agent API) — https://www.digitalocean.com/resources/articles/grok-bot-vs-dots-vs-muse
- Muse desktop platforms (Mac only) — https://zapier.com/blog/muse-ai/ ; https://toolgpa.com/tools/meta-muse ; unofficial muse-desktop wrapper — https://github.com/benjaminkitt/muse-desktop/blob/main/README.md
- Muse-Chat-MCP (unofficial, Chrome-driving) — https://glama.ai/mcp/servers/duclm1x1/Muse-Chat-MCP ; https://npm.io/package/@santaclone/muse-mcp ; muse-mcp on gadget Link API — https://glama.ai/mcp/servers/niclydon/muse-mcp
- Meta AI unofficial wrappers — https://pypi.org/project/metaai-sdk/5.1.0/ ; https://github.com/mir-ashiq/metaai-api/blob/HEAD/README.md ; https://pypi.org/project/meta-ai-api/1.1.7/
- Muse Gadgets coverage (token terms, Linux commands) — https://www.testmuai.com/blog/muse-gadgets/ ; https://cellcog.ai/blog/muse-gadgets/
