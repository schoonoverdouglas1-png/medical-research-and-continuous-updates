# Ubuntu Search Engine Integration Apps — Research Report
Scope: Ubuntu 24.04 (Noble), as of late 2026 (read 2026-11-08). Baseline given: apt carries only ddgr and googler, both unofficial scrapers.
Method note: All evidence is `index` (web search / page fetch). The live research browser failed to open Flathub (`page_gone`, no tabs retained), so no claim below is flagged `verified live`. Negative conclusions were tested with multiple variant phrasings (see each section).

## Summary — per-question verdicts

| Q | Verdict |
|---|---|
| Q1 Repository-style routes beyond apt | **EXISTS — many.** Strongest official ones: Tavily via PyPI/npm, Brave via vendor apt repo / Snap / Flathub, SearXNG and Marginalia via official Docker/install-script self-hosting (not a store package). No official PPA, Snap, or Flatpak was found for Tavily, Marginalia, or SearXNG itself. |
| Q2 Ubuntu desktop GUI for Tavily / Marginalia | **Official: DOES NOT EXIST for either.** Third-party: Newelle (Flathub, GNOME) uses Tavily (and SearXNG/DuckDuckGo) for web search inside a GUI assistant; WebCatalog offers unofficial web-wrappers for Tavily and SearXNG. For Marginalia there is no dedicated GUI app at all — only a third-party Firefox search-engine add-on and the web UI of a self-hosted instance. |
| Q3 Android apps for Tavily / Marginalia | **Official: DOES NOT EXIST for either** (no Google Play or F-Droid listing). Third-party Tavily complement exists: WM Keyboard (F-Droid / Play builds) with a Tavily-backed search tool using your own key. For Marginalia: no app — only manual custom-search-engine setup in Firefox for Android / the desktop Firefox add-on. As a contrast, SearXNG does have a credible Android client, searxist on F-Droid. |
| Q4 Lens/scope / GNOME Shell provider piping these engines into the OS | **For Tavily/Marginalia/SearXNG specifically: DOES NOT EXIST.** For web search generally: **EXISTS, generic only** — GNOME Web (Epiphany) provider, several third-party GNOME extensions for Google/DuckDuckGo/Bing, and — only from Ubuntu 26.04, not 24.04 — Ubuntu's own Web Search Provider (Google) and Snap Search Provider. Unity lenses/scopes are retired history. |

## Findings

### Q1: Beyond apt — repository-style routes (PPA, Snap, Flatpak/Flathub, vendor .deb, pip/npm/cargo)

| Tool / engine | Route | Package / command | Official? | Source |
|---|---|---|---|---|
| Tavily (search API for AI agents) | PyPI | `pip install tavily-cli` → `tvly login`, `tvly search "…"`; also `curl -fsSL https://cli.tavily.com/install.sh \| bash` | Official | https://docs.tavily.com/llms.txt ; https://pypi.org/project/tavily-cli/0.1.1/ |
| Tavily | PyPI (SDK) | `pip install tavily-python` (`TavilyClient`) | Official | https://docs.tavily.com/llms.txt ; https://pypi.org/project/tavily-python/0.7.24/ |
| Tavily | npm | `npm i @tavily/core` (JS/TS SDK) | Official | https://docs.tavily.com/sdk/javascript/quick-start |
| Tavily | npm / remote | `npx -y tavily-mcp@latest`, or remote `https://mcp.tavily.com/mcp/` | Official | https://mcp.so/servers/tavily-mcp |
| Brave Browser / Brave Search | **Vendor apt repository** (not a PPA) | Add `brave-browser-archive-keyring.gpg` + `brave-browser.sources`, then `sudo apt install brave-browser`; also one-liner `curl -fsS https://dl.brave.com/install.sh \| sh` | Official, Brave's recommended route | https://brave.com/linux/?ref=sebday.dev |
| Brave Browser | Snap Store | `sudo snap install brave` — Brave Software, verified publisher, "This package is official", updated 5 Nov 2026 | Official, but Brave says it is "not yet working as well" as native packages | https://snapcraft.io/install/brave/ubuntu ; https://brave.com/linux/?ref=sebday.dev |
| Brave Browser | Flatpak / Flathub | `flatpak install flathub com.brave.Browser` — maintained by Brave Software, same caveat / recommendation to prefer the apt repo | Official | https://brave.com/linux/?ref=sebday.dev |
| Brave Browser | Vendor .deb | (Pre-)releases for all channels on GitHub in DEB/RPM/ZIP formats | Official | https://brave.com/linux/?ref=sebday.dev |
| Brave Search API | npm (third-party wrappers) / Brave MCP | e.g. `npm install brave-search` — explicitly "not officially associated with Brave Software"; Brave's own agent route is its MCP server `@brave/brave-search-mcp-server` (per secondary cataloguing) | Mixed: wrapper third-party | https://jsr.io/@tyr/brave-search |
| SearXNG (self-hosted metasearch) | Docker (official image/compose) | Compose file now in main repo `container/docker-compose.yml`, image `docker.io/searxng/searxng`; `docker compose up -d` on Ubuntu 24.04 | Official project | https://www.ssdnodes.com/learn/searxng-self-hosted-search |
| SearXNG | Official install script (bare metal) | `git clone https://github.com/searxng/searxng.git && sudo -H ./utils/searxng.sh install all` | Official project | https://www.ssdnodes.com/learn/searx-vs-searxng |
| SearXNG in apt | — | **Gone in 24.04:** predecessor `searx` was deleted before 24.04 (last shipped 23.10); `apt install searx` fails on Noble. No SearXNG Snap or Flathub package was found (`site:flathub.org` / `site:snapcraft.io` searches returned no results). | — | https://www.ssdnodes.com/learn/searx-vs-searxng |
| Marginalia Search (self-hosted engine) | Git + install script / Docker | x86-64 Linux only tested, JDK 25 + Docker, `run/install.sh` with "Full Marginalia Search instance" mode; web UI at localhost:8080 | Official project (server, not a client) | https://deepwiki.com/MarginaliaSearch/MarginaliaSearch/11.1-setup-installation-and-configuration |
| Marginalia Search | HTTP API — **no SDK package** | `api2.marginalia-search.com`, header `API-Key: public` (shared/rate-limited) or a key by email; docs give only `curl` and Python `requests` samples | Official API, no pip/npm/cargo package | https://about.marginalia-search.com/article/api/ |
| Marginalia Search | npm-from-source (MCP server) | `marginalia-mcp-server` by bmorphism: clone, `npm install`, `npm run build`; `MARGINALIA_API_KEY` optional, defaults to public | Third-party | https://mcpservers.org/servers/bmorphism/marginalia-mcp-server |
| DuckDuckGo (multi-engine, modern ddgr alternative) | PyPI | `pip install ddgs` (current name; formerly `pip install -U duckduckgo_search`) → CLI `ddgs text -k "…"` | Unofficial scraper (same class as ddgr/googler) | https://pypi.org/project/duckduckgo-search/7.0.1/ |
| DuckDuckGo / SearXNG / Serper-Google | Cargo (crates.io) | `cargo install hodis` — terminal search for people and agents, DuckDuckGo with no setup, SearXNG (your instance or one it sets up), or Google via Serper key; also an MCP tool | Third-party, small/recent — treat as experimental | Crates.io `hodis` listing, via search result at https://www.facebook.com/AndroidWorld9/posts/pfbid0MLB2Vqb5Kd6ns4hsUXHtuD8ASV4UrdLBgzQHVB7P6oV4qSbdJCWJnzfyXnm5apgMl (index snippet; crates.io URL itself was not returned verbatim, so no direct crates.io link is cited) |
| DuckDuckGo | Cargo | `cargo install duckduckgo-search-cli`; also a `web-search` crate (`cargo install web-search`, 40 providers incl. Google/Bing/DDG/Searx/Brave/Mojeek) | Third-party | Search-index snippets only — no verbatim crates.io URL was returned, so these are named without a link rather than with a reconstructed one |
| ddgr | PPA (historical) | `ppa:twodopeshaggy/jarun` is cited in 2017-era guides as maintained by ddgr's developer | Third-party/developer PPA, **not verified as current for Noble (24.04)** — do not rely on it without checking Launchpad first | https://en.ubunlog.com/ddgr-looks-for-duckduckgo-terminal/ |

Warnings / name collisions:
- PyPI `marginalia` (`pip install marginalia`) is **not** Marginalia Search — it is an unrelated Obsidian/Markdown-vault toolkit: https://pypi.org/project/marginalia/
- npm `tavily-cli` is reported by a third-party install guide to be a squatter — the official CLI is the **PyPI** `tavily-cli`. The guide: https://github.com/elnora-ai/elnora-websearch-tools/blob/HEAD/INSTALL_FOR_AGENTS.md
- No official PPA was found for any of Tavily, Marginalia, SearXNG, or Brave (Brave uses its own apt repo, which is the vendor-repo equivalent, not a Launchpad PPA).

### Q2: Ubuntu desktop (GUI) apps for Tavily or Marginalia Search

**Verdict: No official desktop GUI exists for either engine. Plainly: Tavily ships only API/SDK/CLI/MCP; Marginalia ships only a website, an API, and self-hostable server code.**

Evidence for the negative: Tavily deployment listings classify it as Web-Based Yes, Windows No, Mac No, Linux No, Android No — https://slashdot.org/software/comparison/Alpha-Inquire-vs-Tavily/ and https://sourceforge.net/software/compare/Apify-vs-Tavily/ . Variant searches tried: "Tavily desktop app Linux Ubuntu GUI", `"Tavily" app Linux download deb snap flatpak`, `"Tavily" graphical user interface GUI client desktop`, `"Marginalia Search" Linux install PPA snap flatpak`, `"Marginalia Search" GUI client app download`, `"SearXNG" desktop app Linux GUI client download` — none returned a dedicated official GUI for either engine.

Credible third-party GUI options that do exist:

| App | What it is | Tavily/Marginalia relevance | Source |
|---|---|---|---|
| **Newelle** — `flatpak install flathub io.github.qwersyk.Newelle` | GNOME AI assistant/chatbot GUI on Flathub | Web Search implemented **with SearXNG, DuckDuckGo, and Tavily** (v0.9.5, per GNOME's This Week in GNOME). This is the closest thing to a "Tavily GUI" on Ubuntu — an assistant that can call Tavily, not a Tavily search client. No Marginalia backend was listed. | https://flathub.org/en/apps/io.github.qwersyk.Newelle ; https://discourse.gnome.org/t/198-two-more-weeks/28665.rss |
| **WebCatalog wrapper — Tavily** | Turns the Tavily website into a desktop-app window on Linux | Explicitly unofficial: "WebCatalog is not affiliated, associated, authorized, endorsed by or in any way officially connected to Tavily." | https://WebCatalog.io/en/apps/tavily |
| **WebCatalog wrapper — SearXNG** | Same wrapper treatment for a SearXNG instance/site | Same not-affiliated disclaimer for SearXNG. Included as the analogous SearXNG GUI route; there is no native Flathub SearXNG client. | https://webcatalog.io/en/apps/searxng |
| **Marginalia Search — Firefox add-on** (by NUH) | Browser add-on, not a standalone app: "Easily add Marginalia as a search engine in Firefox", v2.0.0, updated 1 Apr 2025 | The only named Marginalia "client" for the desktop found. On Ubuntu this is the practical GUI integration: Marginalia becomes a Firefox address-bar search engine. | https://addons.mozilla.org/en-US/firefox/addon/marginalia-search/ |
| Self-hosted Marginalia / SearXNG web UI | If you install the engine itself (Q1), its own web interface serves locally (Marginalia install docs put the web interface at `http://localhost:8080`) | Official web UI, but it is a server you run, not a client app | https://deepwiki.com/MarginaliaSearch/MarginaliaSearch/11-deployment-and-configuration |

### Q3: Android apps complementing Tavily or Marginalia

**Verdict: No official Android app exists for either engine, and no dedicated third-party Tavily or Marginalia search app was found on Google Play or F-Droid.**

Evidence / variants tried: "Tavily Android app Google Play", `site:play.google.com Tavily search AI` (returned only unrelated apps: TAVILI wholesale food ordering, Taviliro medication tracker, TAV Mobile airports), `site:f-droid.org Tavily` (no results), "Marginalia Search Android app F-Droid", `"Marginalia" search engine app Android`, `site:f-droid.org Marginalia search` (no results). Every Android app actually named "Marginalia" found is an unrelated reading/library app (e.g. AppBrain's Marginalia, a book/library tracker) — https://www.appbrain.com/app/marginalia/com.brulo.folio.aveni.reader . Tavily's deployment listings also say Android App: No (Slashdot/SourceForge links in Q2).

What does exist (third-party, credible):

| App | Store | Relevance |
|---|---|---|
| **WM Keyboard** (`com.wasimaster.wmkeyboard`) | F-Droid (also other builds) | An Android keyboard whose Web/image search tool is backed by **Brave by default, Tavily with a key of your own (from app.tavily.com, free plan 1,000 credits/month), or a SearXNG instance you name**. This is a genuine Tavily complement on Android — search from any app's text field — but it is a keyboard with a search tool, not a Tavily app, and no build ships a Tavily key. Sources: https://wmkeyboard.app/tools/search/ ; https://f-droid.org/en/packages/com.wasimaster.wmkeyboard/ |
| **Firefox for Android — manual custom search engine** | Browser, not an app store listing for Marginalia | Firefox for Android's Default-search-engine screen has **Add search engine** taking a name and a search-string URL with `%s` — the documented way to add engines like Marginalia that "rarely appear preinstalled". No Marginalia-specific Android add-on compatibility was verified (the NUH add-on in Q2 is listed for Firefox generally). Source: https://www.searchengines.net/how-to/change-default-search-engine-android/ |
| **searxist** — *for comparison, SearXNG only* | F-Droid, v2026.10.10 | Shows what a real client looks like when one exists: wraps SearXNG (and 4get/Degoog) in a WebView with Material You, system search-bar widget and popup text action, public or own instances, Android 5+. **It does not support Tavily or Marginalia.** Source (opened): https://f-droid.org/packages/xyz.linerly.searxist/ |

### Q4: Ubuntu lens/scope, GNOME Shell search provider, or DE integration

**Verdict for Tavily / Marginalia / SearXNG specifically: DOES NOT EXIST.** Variant searches — "GNOME search provider SearXNG Tavily Marginalia extension", "Tavily search provider GNOME Shell OR KDE OR Albert OR Ulauncher OR Rofi", "Marginalia search provider GNOME OR KDE OR Ulauncher OR Albert plugin" — returned no provider, lens, scope, runner, or launcher plugin for any of those three engines.

**Verdict for web search generally on Ubuntu: EXISTS, but generic (Google/DuckDuckGo/Bing), and the first-party Ubuntu one is 26.04-only:**

| Integration | Ubuntu version | Behaviour | Official? | Source |
|---|---|---|---|---|
| GNOME Web (Epiphany) search provider | 24.04-available (install Epiphany: apt `epiphany-browser` 46.x in Noble, or `flatpak install flathub org.gnome.Epiphany`) | GNOME Web "has offered its own search provider for years" — enable "Web" in Settings → Search and results/a web-search entry appear in the Overview. Engine is whatever Epiphany is configured with (DuckDuckGo/Bing/Google presets), not Tavily/Marginalia. | Upstream GNOME | https://www.omgubuntu.co.uk/2026/03/ubuntu-2604-gnome-search-extensions ; https://www.zdnet.com/article/6-hidden-gnome-search-tricks-every-linux-user-should-try/ |
| **Web Search Provider** (Ubuntu) | **26.04 only — NOT in 24.04** | Ubuntu release notes: "Added a GNOME Shell search provider for web search — You can now initiate a web search with your default browser from the GNOME Shell global search". OMG! Ubuntu clarifies: it only *initiates* a Google search — on explicit click it opens Firefox with the pre-filled query (with Ubuntu referral parameters); the query is not sent anywhere by typing alone. | Official Ubuntu | https://documentation.ubuntu.com/release-notes/26.04/changes-since-previous-interim/ ; https://www.omgubuntu.co.uk/2026/03/ubuntu-2604-gnome-search-extensions |
| **Snap Search Provider** (Ubuntu) | **26.04 only** | Matches Overview typing against uninstalled Snap Store apps via `snapd`, opens App Center on click. App discovery, not web search. | Official Ubuntu | Same two sources as above |
| Browser Search Provider (GNOME extension) | 24.04-compatible extension model | Adds a provider to open links / search Google (`g`), DuckDuckGo (`d`), Bing (`b`), YouTube (`y`) in the default browser straight from Shell search. Opens the browser — does not render results in the Shell. | Third-party | https://extensions.gnome.org/extension/7454/browser-search-provider/ |
| DuckDuckGo / Google Search Provider (GNOME extensions) | — | Uses DuckDuckGo's Instant Answer API (`api.duckduckgo.com`) to show an instant-answer result in the Shell, linking out to the engine. | Third-party | https://extensions.gnome.org/review/17658 |
| Web Search Dialog (GNOME extension) | — | Ctrl+Space dialog, DuckDuckGo instant result/definition inside the dialog, choose/add multiple search engines with keywords, Enter opens the result in the default browser. Custom engines can be added, which in principle could point at a Marginalia/SearXNG URL — but that is user configuration, not a shipped Marginalia/SearXNG provider. | Third-party | https://extensions.gnome.org/extension/549/web-search-dialog/ |
| Search Does Search (GNOME extension, in review) | Needs `gir1.2-webkit2-4.1` on Debian/Ubuntu | The most "piped-in" design found: the engine's own results page **renders right there in the GNOME Overview search list** — read/scroll/click without leaving the Overview. Engines offered in settings: **DuckDuckGo or Google only**. | Third-party, still in review at time of the review page | https://extensions.gnome.org/review/75841 |
| Unity Lens / Scope (historical) | Pre-GNOME Ubuntu (Unity 7/8) | Scopes were "gracefully retired"; the Amazon shopping lens and online scopes were turned off by default / removed from 16.04 onward. There is no current Unity lens for these engines on 24.04's GNOME desktop. | Retired Canonical tech | https://ubuntu.com/blog/cleaning-up-scopes-settings (via search snippet) and The Register's scopes-retirement coverage found in search |

Practical implication for a 24.04 user: to get OS-level web search today you either (a) install Epiphany and enable its Web provider, (b) install one of the third-party extensions above (Google/DuckDuckGo only), or (c) upgrade to 26.04 for Ubuntu's built-in Google Web Search Provider. None of these routes delivers Tavily, Marginalia, or SearXNG results into the Shell out of the box.

## Could not verify
- Whether the ddgr PPA `ppa:twodopeshaggy/jarun` still publishes Noble (24.04) builds — only 2017-era articles cite it; Launchpad was not opened.
- Direct crates.io URLs for `hodis`, `duckduckgo-search-cli`, and `web-search`: the search tool did not return verbatim URLs for those listings (it suppressed some result URLs), so they are named without links rather than with reconstructed URLs. Their existence and `cargo install` commands come from index snippets.
- Whether the NUH "Marginalia Search" Firefox add-on installs/works on Firefox for Android specifically — its AMO page does not state Android compatibility in the fetched text.
- Flathub/Snap storefront pages could not be checked in the live research browser (window returned `page_gone`); Brave/Newelle store claims rest on the vendors' own pages plus index fetches of the store listings, which agree with each other.
- Penguin Mail (a Linux GTK mail GUI whose assistant can web-search via Brave or your own SearXNG, distributed via its own Flatpak repo/.deb/snap per its README at https://github.com/c9dev/penguin-mail/blob/HEAD/README.md) was found incidentally; it was not fully vetted and is not counted as a search client — it is a mail app with a search-using assistant, and it does not use Tavily/Marginalia.

## Sources
All read 2026-11-08, all `index` (none `verified live` — see method note):
- Tavily docs index — CLI, Python/JS SDKs, MCP — https://docs.tavily.com/llms.txt
- Tavily CLI on PyPI — https://pypi.org/project/tavily-cli/0.1.1/
- Tavily Python on PyPI — https://pypi.org/project/tavily-python/0.7.24/
- Tavily JS SDK quickstart — https://docs.tavily.com/sdk/javascript/quick-start
- Tavily MCP (official, npm/remote) — https://mcp.so/servers/tavily-mcp
- Brave on Linux (vendor apt repo, Snap, Flatpak, GitHub .deb; recommendations) — https://brave.com/linux/?ref=sebday.dev
- Brave Snap (Ubuntu) — https://snapcraft.io/install/brave/ubuntu
- Brave Search npm wrapper (third-party disclaimer) — https://jsr.io/@tyr/brave-search
- SearXNG self-hosting / Docker Compose (secondary, quoting official repo) — https://www.ssdnodes.com/learn/searxng-self-hosted-search
- SearXNG vs Searx, apt removal in 24.04, install script — https://www.ssdnodes.com/learn/searx-vs-searxng
- Marginalia API (official) — https://about.marginalia-search.com/article/api/
- Marginalia self-host setup (DeepWiki summary of official repo) — https://deepwiki.com/MarginaliaSearch/MarginaliaSearch/11.1-setup-installation-and-configuration
- Marginalia MCP server (third-party) — https://mcpservers.org/servers/bmorphism/marginalia-mcp-server
- Marginalia Firefox add-on (third-party, NUH) — https://addons.mozilla.org/en-US/firefox/addon/marginalia-search/
- PyPI `marginalia` name collision — https://pypi.org/project/marginalia/
- Newelle on Flathub — https://flathub.org/en/apps/io.github.qwersyk.Newelle
- Newelle web search with SearXNG/DuckDuckGo/Tavily (GNOME TWIG) — https://discourse.gnome.org/t/198-two-more-weeks/28665.rss
- WebCatalog Tavily (unofficial disclaimer) — https://WebCatalog.io/en/apps/tavily
- WebCatalog SearXNG (unofficial disclaimer) — https://webcatalog.io/en/apps/searxng
- Tavily deployment = no native apps — https://slashdot.org/software/comparison/Alpha-Inquire-vs-Tavily/ ; https://sourceforge.net/software/compare/Apify-vs-Tavily/
- Unrelated Android "Marginalia" reading app — https://www.appbrain.com/app/marginalia/com.brulo.folio.aveni.reader
- WM Keyboard search tool (Brave/Tavily/SearXNG) — https://wmkeyboard.app/tools/search/
- WM Keyboard on F-Droid — https://f-droid.org/en/packages/com.wasimaster.wmkeyboard/
- searxist on F-Droid (SearXNG Android client) — https://f-droid.org/packages/xyz.linerly.searxist/
- Firefox/Android custom search engine — https://www.searchengines.net/how-to/change-default-search-engine-android/
- DuckDuckGo search on PyPI (ddgs) — https://pypi.org/project/duckduckgo-search/7.0.1/
- ddgr PPA (historical) — https://en.ubunlog.com/ddgr-looks-for-duckduckgo-terminal/
- Ubuntu 26.04 release notes (web + snap search providers, 26.04-only) — https://documentation.ubuntu.com/release-notes/26.04/changes-since-previous-interim/
- Ubuntu 26.04 Web/Snap Search Providers explained — https://www.omgubuntu.co.uk/2026/03/ubuntu-2604-gnome-search-extensions
- GNOME Browser Search Provider — https://extensions.gnome.org/extension/7454/browser-search-provider/
- GNOME Web Search Dialog — https://extensions.gnome.org/extension/549/web-search-dialog/
- GNOME DuckDuckGo Search Provider (review) — https://extensions.gnome.org/review/17658
- GNOME Search Does Search (review; DDG/Google rendered in Overview) — https://extensions.gnome.org/review/75841
- GNOME search tricks / Epiphany Web provider — https://www.zdnet.com/article/6-hidden-gnome-search-tricks-every-linux-user-should-try/
