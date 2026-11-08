# Notes — read 2026-11-08 (America/Chicago date; crawls UTC 2026-11-08)
All sources via web index (browser_search/browser_open). Research window attempted for Flathub (tabs open) returned page_gone / no tabs — live-browser verification unavailable, so all flags = index.

## Tavily official
- https://docs.tavily.com/llms.txt — pip install tavily-cli (tvly login/search), pip install tavily-python, npm i @tavily/core, remote MCP https://mcp.tavily.com/mcp/
- https://pypi.org/project/tavily-cli/0.1.1/ — tavily-cli 0.1.1 Mar 17 2026, provides tvly, depends on tavily-python; also curl https://cli.tavily.com/install.sh
- https://pypi.org/project/tavily-python/0.7.24/ — tavily-python
- npm tavily-mcp: npx -y tavily-mcp@latest, official tavily-ai/tavily-mcp (via mcp.so search result)
- Deployment lists say no native apps: https://slashdot.org/software/comparison/Alpha-Inquire-vs-Tavily/ — Web-Based Yes, Android No, Windows/Mac/Linux No; https://sourceforge.net/software/compare/Apify-vs-Tavily/ similar
- WebCatalog wrapper unofficial: https://WebCatalog.io/en/apps/tavily — "not affiliated... officially connected to Tavily"

## Brave official
- https://brave.com/linux/?ref=sebday.dev (opened) — vendor apt repo: brave-browser-archive-keyring + brave-browser.sources, sudo apt install brave-browser; Flatpak from Flathub maintained by Brave but recommends native repos; Snap in Snapcraft maintained by Brave, recommends native; GitHub DEB/RPM/ZIP releases
- https://snapcraft.io/install/brave/ubuntu — snap brave, Brave Software verified, official, last updated 5 Nov 2026, sudo snap install brave
- Flathub com.brave.Browser (via brave page + distro.watch search result)

## SearXNG
- Official routes: Docker Compose from main repo container/docker-compose.yml (image docker.io/searxng/searxng), script git clone + sudo -H ./utils/searxng.sh install all — https://www.ssdnodes.com/learn/searxng-self-hosted-search and .../searx-vs-searxng (secondary, quoting official docs/repo); searx apt package deleted from 24.04, last in 23.10
- No Flathub/Snap client found in searches site:flathub.org / site:snapcraft.io (no results)
- WebCatalog SearXNG wrapper unofficial: https://webcatalog.io/en/apps/searxng disclaimer not affiliated

## Marginalia
- Official API only: https://about.marginalia-search.com/article/api/ (opened) — api2.marginalia-search.com, API-Key header, key 'public', curl + Python requests sample, no SDK package listed
- Self-host: x86-64 Linux, Docker/JDK, run/install.sh, modes incl Full Marginalia — DeepWiki of MarginaliaSearch repo (secondary summary of official repo)
- Third-party MCP: https://mcpservers.org/servers/bmorphism/marginalia-mcp-server — npm install / npm run build from source, MARGINALIA_API_KEY optional defaults public
- Firefox add-on (third-party NUH): https://addons.mozilla.org/en-US/firefox/addon/marginalia-search/ — "Easily add Marginalia as a search engine in Firefox", v2.0.0 Apr 1 2025, 258 users per author page
- pip name collision warning: https://pypi.org/project/marginalia/ is an Obsidian Markdown vault toolkit, NOT the search engine
- No Android/desktop app found: Play/F-Droid site searches returned no search-engine app; AppBrain "Marginalia" com.brulo.folio... is a reading/library app, unrelated

## Desktop GUI using Tavily/SearXNG (third-party)
- Newelle: Flathub https://flathub.org/en/apps/io.github.qwersyk.Newelle — GNOME AI chatbot; GNOME TWIG via https://discourse.gnome.org/t/198-two-more-weeks/28665.rss — "Implemented Web Search with SearXNG, DuckDuckGo, and Tavily" in 0.9.5; install flatpak install flathub io.github.qwersyk.Newelle

## Android
- searxist (SearXNG, not Tavily/Marginalia): https://f-droid.org/packages/xyz.linerly.searxist/ (opened) — v2026.10.10, wraps SearXNG/4get/Degoog WebView, Material You, system search widget
- WM Keyboard: https://f-droid.org/en/packages/com.wasimaster.wmkeyboard/ + https://wmkeyboard.app/tools/search/ — Android keyboard, web/image search backed by Brave by default, Tavily with own key from app.tavily.com, or SearXNG instance you name (F-Droid build emphasis)
- Tavily Android: site:play.google.com searches returned only unrelated TAVILI/Taviliro etc; site:f-droid.org Tavily = no results
- Marginalia Android: site:f-droid.org Marginalia search = no results

## pip/cargo general
- ddgs: https://pypi.org/project/duckduckgo-search/7.0.1/ etc — pip install -U duckduckgo_search, CLI ddgs; newer name pip install ddgs (via multiple skill docs referencing PyPI)
- cargo hodis: crates.io hodis — cargo install hodis, searches DuckDuckGo / SearXNG / Serper (Google), also installer script; third-party, recent/small
- cargo duckduckgo-search-cli, web-search crates exist (crates.io search results) — third-party
- ddgr PPA historical: ppa:twodopeshaggy/jarun cited in 2017-era articles (ubunlog/ucartz) — NOT verified current for Noble

## Q4 DE integration
- Ubuntu 26.04 (not 24.04): https://documentation.ubuntu.com/release-notes/26.04/changes-since-previous-interim/ — "Added a GNOME Shell search provider for snap applications" + "for web search: initiate a web search with your default browser"; https://www.omgubuntu.co.uk/2026/03/ubuntu-2604-gnome-search-extensions — Web Search Provider = Google via Firefox on explicit click, Snap Search Provider via snapd
- Epiphany provider pre-existing: OMG says GNOME Web has offered its own search provider for years; ZDNet trick: install org.gnome.Epiphany flatpak, enable Web in Settings>Search
- GNOME extensions (third-party, extensions.gnome.org):
  - Browser Search Provider https://extensions.gnome.org/extension/7454/browser-search-provider/ — g/d/b/y prefixes Google/DDG/Bing/YouTube, opens browser
  - Web Search Dialog https://extensions.gnome.org/extension/549/web-search-dialog/ — Ctrl+Space, DDG instant, choose/add engines, opens browser
  - DuckDuckGo Search Provider / Google Search Provider (review pages, DDGS IA API)
  - Search Does Search https://extensions.gnome.org/review/75841 — renders DDG/Google results page inside Overview, needs gir1.2-webkit2-4.1 on Ubuntu
- Unity scopes retired: https://www.theregister.com etc + ubuntu.com cleaning up scopes — shopping lens/scopes gracefully retired from 16.04 era
- No Tavily/Marginalia/SearXNG-specific GNOME provider found after variants: "GNOME search provider SearXNG Tavily Marginalia", "Tavily search provider GNOME Shell OR KDE OR Albert OR Ulauncher OR Rofi", "Marginalia search provider GNOME OR KDE OR Ulauncher OR Albert plugin" — all returned none for those engines
