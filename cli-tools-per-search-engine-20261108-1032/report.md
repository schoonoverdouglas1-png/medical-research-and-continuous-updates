# Free CLI / Programmatic Access per Search Engine — Status Today (8 Nov 2026)

## Summary

Only three routes are both **legitimate (official/sanctioned) and genuinely free without a payment card** for general web results from an Ubuntu terminal today:

1. **Tavily** (the archetypal hosted developer search service, §1) — 1,000 credits/month, no card, `curl`/pip SDK. Verified live on Tavily's own pricing page.
2. **Marginalia** (§9) — official API with the shared key literally `public`, just `curl`; heavily rate-limited and a small, non-commercial index.
3. **Self-hosted SearXNG** — free forever, but it is a Docker service you run (256–512 MB RAM), not a CLI, and upstream it still scrapes engines, so several engines block it.

Everything else is either card-gated "free credit" (Brave, Mojeek trial, Gemini grounding on a billing-enabled project), closed/retired (Bing API retired 11 Aug 2025; Google Custom Search closed to new customers, ends 1 Jan 2027), grey scraping only (DuckDuckGo via `ddgr`/`ddgs`, Google via `googler`, Startpage/Ecosia scrapers), or has no programmatic route at all (Ecosia, Startpage, Duck.ai).

**Ambiguity note on §1:** the mission did not name a single vendor for item 1 ("the hosted web-search service behind developer 'web-search' CLI tools"). It is treated here as that category — hosted developer search APIs (Tavily, Serper, SerpApi, Exa, etc.) that power `web_search` tools in agent frameworks and CLIs such as `eggsearch`, `ketch`, Hermes Agent's `web_search`, etc. Tavily is reported as the headline example, Serper/SerpApi where they are the relevant Google route.

Confidence: high on retirements, free-tier/card facts and packaging — most are corroborated by the vendor's own page plus at least one independent Oct–Nov 2026 read. Bot-block behaviour (403/429/captcha) is necessarily IP-dependent; it rests on published live tests in Jul–Oct 2026, flagged as `index` below.

---

## Findings

### 1. Hosted web-search service behind developer "web-search" CLI tools (general web search index)

- **Tool/method:** Hosted REST APIs called with `curl` or a pip SDK — principally **Tavily** (`api.tavily.com`, pip `tavily-python`), **Serper** (`google.serper.dev/search`, header `X-API-KEY`), **SerpApi**. Agent CLIs wrap them: `eggsearch` (single Rust binary, MCP + CLI), `ketch`, Hermes `web_search`. SearXNG (self-hosted, see below) is the free alternative in the same tool slots.
- **Official or grey?** Tavily is OFFICIAL/sanctioned — it is the vendor's own product, not a scrape of a consumer page (its underlying index sourcing is not fully disclosed). Serper/SerpApi are sanctioned *by the vendor you pay*, but upstream they obtain Google results Google does not offer via an official API — grey upstream, with continuity/legal risk (Google sued SerpApi in Dec 2025 over anti-bot circumvention; case unresolved as of Aug 2026).
- **Free tier:** Tavily Researcher — **1,000 API credits/month, no credit card required**, requests hard-stop at zero; basic search = 1 credit, advanced = 2. Serper — **2,500 free queries, one-time (not monthly), no card**. SerpApi — 250 searches/month free.
- **Packaging:** No apt package for any of them; pip SDKs / plain `curl`. `eggsearch` is a standalone Rust binary (GitHub/cargo), not apt/pip.
- **Verdict: ✅ Usable today for free from a Linux terminal — Tavily is the cleanest legitimate free route in this whole report (key required, no card).**
- Sources: Tavily pricing, **verified live** 2026-11-08, https://www.tavily.com/pricing ; Serper free grant, index, https://keirolabs.cloud/blog/serper-api-guide-2026 and https://parallel.ai/articles/best-free-web-search-api (checked against vendor pages 27 Oct 2026).

**SearXNG (cross-cutting, applies to §§2,3,5,7,8):** open-source self-hosted metasearch aggregating 70+ engines. Not a CLI — a Docker service; enable `json` in `settings.yml` (otherwise JSON requests get 403), then `curl 'http://localhost:8080/search?q=…&format=json'`. RAM: **256 MB minimum, 512 MB recommended, +50–100 MB for Valkey/Redis** — confirming the mission's ~150–300 MB ballpark at the low end, ~512 MB–1 GB in typical Docker Compose guidance. Free, no key, no apt package (Docker image / pip). Its legality is grey in the same way as the scrapers it wraps, and public instances usually disable JSON, so self-hosting is the reliable path. Sources (index): https://selfhosting.sh/apps/searxng/ ; https://railway.com/deploy/searxng-search-api ; https://www.bitdoze.com/searxng-self-host-privacy-search/

### 2. Bing (Microsoft)

- **Tool/method:** Formerly Bing Web Search API v7 via Azure (`api.bing.microsoft.com/v7.0/search`). Successor: **Grounding with Bing Search** inside Azure AI Foundry / AI Agents (and a newer Foundry Web Search tool). Grey fallback: scraping `bing.com/search` via SearXNG's bing engine, `openserp`, or a SERP API's Bing engine (SerpApi/DataForSEO).
- **Official or grey?** The old API was official — and is **dead**. Grounding is official but is *not a search-results API*: Microsoft states developers/end users have no access to the raw content returned; you get an LLM answer with citations. HTML scraping is grey.
- **Free tier:** **None.** The retirement covered every free and paid tier (F1/S1–S9, Custom F0/S1–S4); endpoints now return **HTTP 410 Gone**, no new keys. Grounding is paid Azure only — **$14 per 1,000 transactions** per Microsoft's Sept 2026 listing (some Oct 2026 secondary reads still cite $35/1,000 — treat price as in flux), plus model/Agent costs, and only paid Azure subscriptions qualify (free-credit/sponsored subscriptions do not).
- **Packaging:** Azure SDKs (pip `azure-ai-*`); no apt CLI for Bing search.
- **Verdict: ❌ Not usable today for free — no official Bing results API exists at all any more; only paid Azure grounding (answers, not results) or grey, captcha-prone scraping of bing.com.**
- Sources (index): retirement corroborated at https://www.searxncrawl.io/bing-google-search-api-alternative/ , https://fe.tonywang.io/blog/bing-search-api-alternatives , https://serplify.io/blog/bing-search-api-alternatives/ (all quoting Microsoft Learn: "Bing Search APIs will be retired on August 11, 2025… decommissioned completely").

### 3. DuckDuckGo

- **Tool/method:** **`ddgr`** (CLI, scrapes the DuckDuckGo HTML version), **`ddgs`** (pip library + `ddgs` CLI, formerly `duckduckgo_search`), and the official **Instant Answer API** (`api.duckduckgo.com/?q=…&format=json`).
- **Official or grey?** `ddgr`/`ddgs` are **GREY scrapers** — `ddgr` itself states it "isn't affiliated to DuckDuckGo in any way" and works on the HTML version; DuckDuckGo's terms prohibit scraping. The Instant Answer API is OFFICIAL — but it is **not a web-search API**: it returns a Wikipedia-style abstract/related topics for entity queries and empty fields for most queries; no ranked web results.
- **Free tier:** All free, **no key, no card** — and no published limits or SLA. In practice the HTML endpoint throttles automated callers: `ddgs` raises `RatelimitException: 202 Ratelimit`, bursts and datacenter/VPN IPs are throttled almost immediately, and `html.duckduckgo.com` serves bot-check/captcha pages (confirming the mission's known fact). ~1 req/s is the community-safe pace.
- **Packaging:** ✅ **`ddgr` in apt** — Ubuntu noble `ddgr 2.2-1 [universe]`, also snap and standalone .deb; `ddgs` via **pip** (`pip install ddgs`), not apt.
- **Verdict: ⚠️ Grey-only for real web results — works free at low volume from a residential IP via `ddgr`/`ddgs`, unreliable under automation; the only official API (Instant Answers) does not return search results.**
- Sources (index): https://packages.ubuntu.com/eu/noble/misc/ ; https://www.browserfoundry.cloud/blog/duckduckgo-search-api ; https://link.sc/blog/duckduckgo-search-api-guide ; https://keirolabs.cloud/blog/duckduckgo-search-api

### 4. Brave Search

- **Tool/method:** **Brave Search API** — `GET https://api.search.brave.com/res/v1/web/search` with header `X-Subscription-Token`, via `curl`, community SDKs, or Brave's official MCP server (npm `@brave/brave-search-mcp-server`). Grey alternative: scraping `search.brave.com` (used by `eggsearch`'s vendored Brave HTML engine, SearXNG's brave engine).
- **Official or grey?** The API is OFFICIAL, over Brave's own independent index (30B+ pages). The consumer-page scrape is grey.
- **Free tier:** **The old free plan is gone.** It was 2,000 queries/month (later 5,000) until **February 2026**, when Brave replaced it with metered billing: Search at **$5 per 1,000 requests with $5 in free credits every month (≈1,000 requests)**, 50 req/s. **A credit card is required to activate any plan, including to use the free credits** (Brave: anti-fraud), and attribution is required to keep the credit. Confirming the mission's known fact.
- **Consumer-page rate limiting:** also confirmed — in a Jul 2026 live test series, Brave's rendered results page was the one consumer channel that worked, then returned **persistent HTTP 429s that ~20 minutes of paced retries never cleared**.
- **Packaging:** No apt/pip first-party CLI; `curl` or the npm MCP server.
- **Verdict: ⚠️ Legitimate and usable — but NOT card-free. If a card on file is acceptable, ~1,000 free official queries/month; if "free" means no card, Brave no longer qualifies. Grey scrape rate-limits hard (429).**
- Sources (index): official pricing https://api-dashboard.search.brave.com/documentation/pricing ; card/credit corroboration https://apiserpent.com/blog/free-brave-search-api (read of Brave's own pages 23 Oct 2026), https://scrapegraphai.com/blog/brave-search-api ; 429 live test https://github.com/directiveforge/directiveforge/blob/HEAD/research/2026-07-11-user-pain-raw/2c-reddit.md

### 5. Google (web search results)

- **Tool/method:** **`googler`** (CLI scraper), **Google Custom Search JSON API** (`googleapis.com/customsearch/v1`, Programmable Search Engine), third-party SERP APIs (Serper/SerpApi, §1), SearXNG's google engine.
- **Official or grey?** `googler` is a **GREY scraper** of the consumer results page; Google's terms prohibit automated access and `robots.txt` disallows `/search`. Custom Search was OFFICIAL but returned results from a *configured* Programmable Search Engine, not google.com as such.
- **Status / free tier:** Custom Search JSON API is **closed to new customers**; new keys/engines fail (403 reported), and new engines since 20 Jan 2026 are limited to ≤50 designated sites. Existing customers keep **100 free queries/day, then $5/1,000, cap 10,000/day — only until discontinuation on 1 January 2027** (confirming the mission's "~2027" fact — it is exactly 1 Jan 2027). Google's suggested replacements (Vertex/Agent Search) are site-restricted to 50 domains, not full-web search.
- **Raw-page fetching:** confirmed hostile — since Jan 2025 Google requires JavaScript to serve results; plain HTTP gets a JS shell, consent interstitial, or "unusual traffic" page (sometimes with HTTP 200, sometimes **429**), so `googler`-style parsing frequently returns zero results, especially from datacenter IPs.
- **Packaging:** ✅ **`googler` in apt** — `googler 4.3.13-1 [universe]` (Ubuntu questing listing; also Debian bookworm 4.3.13-1), plus a standalone downloadable script from GitHub. That confirms the mission's apt claim for both `ddgr` and `googler` — packaging exists even though the upstream service blocks the technique.
- **Verdict: ❌ No legitimate free route for a new user today. Grey `googler` is in apt but unreliable against current Google defences; the practical free-ish Google route is a third-party SERP API trial (Serper 2,500 one-time, no card — vendor-sanctioned, grey upstream).**
- Sources (index): https://cloro.dev/blog/google-search-api/ ; https://www.browserfoundry.cloud/blog/google-custom-search-api-alternative ; https://packages.ubuntu.com/fi/questing/misc/ ; https://webscraping.ai/blog/scrape-google-search-results

### 6. Mojeek

- **Tool/method:** **Mojeek Search API** (official, JSON/XML, `curl` with API key) over Mojeek's own independent index (~9B pages). Grey: scraping `mojeek.com/search` (eggsearch/SearXNG mojeek engines).
- **Official or grey?** API is OFFICIAL. HTML scraping is grey and blocked.
- **Free tier:** **No recurring free tier.** Official FAQ: you can "sign up to our Startup Plan and claim a free credit" — but **"a bank card is required to open an account"** (no automatic payments, Stripe). Paid PAYG thereafter (Startup ≈£2 per 1,000 queries in the Jul 2026 live read; a Personal tier at £1/1,000 is cited elsewhere — check the live pricing page before relying on the exact tier ladder).
- **HTML behaviour:** confirming the mission's claim — bare request **HTTP 403**; with a browser user-agent, HTTP 200 serving an **ALTCHA/captcha challenge page**, not results.
- **Packaging:** No apt/pip CLI; API key + `curl`.
- **Verdict: ❌ Not usable for free in any ongoing sense — official API exists and is legit, but free use is a one-off trial credit behind a bank card; the consumer page 403/captchas automated callers.**
- Sources (index): official https://www.mojeek.com/services/search/web-search-api/ (FAQ quoted in search index) ; live block test https://github.com/katrielmoses/mailaccess/blob/HEAD/docs/research/search-engine-federation-2026-07-15.md

### 7. Ecosia

- **Tool/method:** No named CLI and no public developer search API was found. Grey options only: SearXNG's ecosia engine, `openserp` (browser-rendered Ecosia), eggsearch-style scrapers.
- **Official or grey?** Grey only. Ecosia offers no self-serve API for its results (historically Bing/Google-backed; since Aug 2025 partly its own EUSP/Staan index in France/Germany — Staan is described as B2B index infrastructure for partners/AI grounding, with **no free public developer API, key signup, or pricing documented** in any source found).
- **Free tier:** N/A — no API to have one.
- **HTML behaviour:** confirming the mission's claim — **HTTP 403** to automated callers in repeated live tests (Jul 2026 federation test: 403 on every attempt; another test: loaded JS-empty, then 403 on retry; Ecosia sits behind Cloudflare).
- **Packaging:** None.
- **Verdict: ❌ None — no official API and the consumer page 403s automated callers; do not build on Ecosia scraping.**
- Sources (index): https://github.com/katrielmoses/mailaccess/blob/HEAD/docs/research/search-engine-federation-2026-07-15.md ; https://ppc.land/ecosia-launches-european-search-index-in-france/ (Staan background)

### 8. Startpage

- **Tool/method:** No official API or CLI. Grey scrapers only: SearXNG's startpage engine, `eggsearch`'s vendored Startpage HTML scraper.
- **Official or grey?** Grey only. Startpage is a privacy front-end with no index of its own — it relays queries to **Google and Bing** — and it actively defends against automation ("subjected to automated abuse and scraping on a daily basis… strong anti-abuse measures"), including captcha and, per one API-documentation survey, a **proof-of-work challenge** on result pages.
- **Free tier:** N/A — no API.
- **Behaviour in live tests:** "flatly refused" in the Jul 2026 cross-engine test series; other tooling documents captcha-detection as a routine Startpage failure mode.
- **Packaging:** None.
- **Verdict: ❌ None reliable — no legitimate programmatic route exists, and grey scraping is specifically targeted by Startpage's anti-abuse system.**
- Sources (index): https://www.searchengines.net/startpage/ ; https://fe.tonywang.io/docs/startpage ; https://github.com/directiveforge/directiveforge/blob/HEAD/research/2026-07-11-user-pain-raw/2c-reddit.md

### 9. Marginalia Search

- **Tool/method:** **Official public API — plain `curl`.** New API: `GET https://api2.marginalia-search.com/search?query=…` with header `API-Key: public`. Deprecated old API: `https://api.marginalia.nu/public/search/<query>?count=N`. Also usable via SearXNG's marginalia engine. No dedicated CLI binary is needed or packaged.
- **Official or grey?** **OFFICIAL/sanctioned** — this is Marginalia's documented developer API, confirming the mission's known fact. Results are licensed **CC-BY-NC-SA 4.0** (non-commercial; commercial use needs a commercial key/terms by email).
- **Free tier:** **No signup, no card.** The shared key `public` works immediately but "often hits a rate limit" (new API) / returns **HTTP 503 when the shared limit is hit** (old API), and cannot use custom filters. A free personal key is available by emailing contact@marginalia-search.com, which avoids the shared limit.
- **Caveat — coverage:** Marginalia is a small independent index deliberately biased to the non-commercial, text-heavy web (personal sites, blogs, wikis, forums). It is weak/absent for news, commerce, and mainstream topics (e.g. it does not index Reddit at all in tests). It is a complement, not a Google replacement.
- **Packaging:** Nothing to install — `curl` on any Ubuntu box; optionally SearXNG via Docker.
- **Verdict: ✅ Usable today for free from a Linux terminal — the only engine-native, keyless, card-free official API in this list. Expect 503s on the shared key at busy times and niche coverage.**
- Sources: **verified live** 2026-11-08, https://about.marginalia-search.com/article/api/

### 10. Google Gemini with search grounding (AI answer engine)

- **Tool/method:** **Gemini API** with the `google_search` tool — via `curl` to the Gemini Developer API, pip `google-genai` SDK, or Google's `gemini` CLI — API key from Google AI Studio. Returns a model-written answer with citations/grounding metadata, **not a raw results list**.
- **Official or grey?** OFFICIAL — this is Google's sanctioned replacement story for programmatic Google-grounded answers.
- **Free tier — the catch:** For **Gemini 3 and newer models, grounding is NOT available on the API Free Tier**: a Google staff reply (Oct/Nov 2026 forum) states calls with search enabled from a project **without billing return HTTP 429**, and Google's pricing page lists grounding as "Not available" in the Free Tier column. **Billing-enabled projects** get **5,000 free search requests/month (shared across Gemini 3+ models, daily cap 1,500/day), then $14 per 1,000 requests** — plus normal per-token model charges, and one prompt can trigger several billable search queries. Setting up billing means a payment method on the Google Cloud/AI Studio project. Legacy exception: Gemini 2.5 Flash/Flash-Lite pricing lists 500 grounded RPD free (1,500 RPD in the tools table for paid) — but new users report 2.5 models returning 404/"no longer available to new users", so do not plan on it. Grounding is free to *try interactively in AI Studio's web UI*, which is not a CLI/programmatic route.
  - *Source conflict flagged:* several Oct 2026 pricing summaries state "5,000 free/month" without the billing gate; Google's own staff clarification and the pricing page's Free-Tier column ("Not available") resolve it — the 5,000 are free *on a paid/billing-enabled project*.
- **Packaging:** pip (`google-genai`) / npm (`@google/gemini-cli`) / `curl`; no apt package.
- **Verdict: ⚠️ Official and excellent for grounded answers, but NOT free from a terminal without enabling billing (card). With billing on, 5,000 grounded searches/month are included before the $14/1,000 rate.**
- Sources (index): https://discuss.ai.google.dev/t/google-search-grounding/191945 (Google staff answer) ; Google pricing page as indexed at https://aistudio.google.com/docs/pricing ; corroboration https://infro.io/blog/gemini-api-pricing-2026

### 11. Duck.ai (DuckDuckGo's AI chat)

- **Tool/method:** No official tool. Unofficial bridges only — e.g. `duckapi` / DuckAI2API projects that expose an OpenAI-compatible `/v1/chat/completions` by **driving the real duck.ai site in Chrome via Playwright** or reverse-engineering its XHR/SSE protocol (anti-bot tokens such as `x-fe-signals` / `X-Vqd-Hash-1` / `vqd` minted by page JS).
- **Official or grey?** **GREY / reverse-engineered.** The bridge projects themselves state plainly: "Duck.ai has no public API" / "DuckDuckGo publishes no public API" for this product, and warn use may violate Duck.ai's terms. This matches the mission's known fact; the closest official developer surface DuckDuckGo offers remains the Instant Answers API (§3), which is a different, non-chat, non-search product. (No primary DuckDuckGo help page explicitly saying "for Duck.ai, use the Instant Answers API instead" was located — see Could not verify.)
- **Free tier:** Duck.ai itself is free/anonymous in a browser with a **daily usage limit (resetting midnight UTC, exact count unpublished, varies by model)** — but there is no sanctioned way to consume that free tier programmatically. Bridges risk a **persistent per-IP ban: HTTP 418 `ERR_BN_LIMIT` with no Retry-After/cooldown**.
- **Packaging:** GitHub clones / pip installs of unofficial projects only; nothing in apt, nothing official on pip/npm.
- **Verdict: ❌ No legitimate CLI/programmatic route — none exists. Unofficial browser-driving bridges work until they break or get the IP banned; do not build an agent on them.**
- Sources (index): https://github.com/hirotomasato/duckapi/blob/main/README.md ; https://github.com/wuyouseo/DuckAI2API ; https://github.com/emahboubinia/duckai-openai-api

---

## Per-engine table

| # | Engine / service | Best terminal method | Official? | Key? | Card for free use? | Free limit | apt / pip / binary | Usable free today? |
|---|---|---|---|---|---|---|---|---|
| 1 | Hosted developer search (Tavily et al.) | Tavily API via `curl` / pip SDK | ✅ Official | Yes (free signup) | **No** | 1,000 credits/mo (Serper alt: 2,500 one-time) | pip / curl; eggsearch = standalone binary | **✅ Yes** |
| 2 | Bing | — (was Bing API v7) | Was official, **retired 11 Aug 2025** | No new keys | N/A | None; Grounding $14/1k, Azure paid only, no raw results | Azure pip SDKs | **❌ No** |
| 3 | DuckDuckGo | `ddgr` / `ddgs` (HTML scrape); Instant Answer API (official, no web results) | ⚠️ Grey for results; official only for instant answers | No | No | Unlimited in theory; 202/captcha throttling in practice | **apt: ddgr 2.2-1**; pip: ddgs | **⚠️ Grey only, low volume** |
| 4 | Brave Search | Brave Search API (`X-Subscription-Token`) | ✅ Official | Yes | **Yes** | $5 credit/mo ≈1,000 req (old 2,000/mo plan ended Feb 2026) | curl / npm MCP server | **⚠️ Yes, if card acceptable** |
| 5 | Google | `googler` (scrape); Custom Search JSON API (existing customers only) | ⚠️ Grey / official-but-closing | CSE: yes | CSE: billing for paid tier | CSE existing: 100/day until **1 Jan 2027**, then ends; closed to new users | **apt: googler 4.3.13-1** | **❌ No legitimate new route** |
| 6 | Mojeek | Mojeek Search API | ✅ Official | Yes | **Yes (bank card to open account)** | One-off free trial credit only; then PAYG ≈£2/1k | curl only | **❌ No ongoing free tier** |
| 7 | Ecosia | — | ❌ No API | — | — | None; consumer page 403 | None | **❌ No** |
| 8 | Startpage | — (SearXNG/eggsearch scrapers) | ❌ No API | — | — | None; captcha/proof-of-work | None | **❌ No** |
| 9 | Marginalia | `curl` to api2.marginalia-search.com, `API-Key: public` | ✅ Official | Shared key `public`; own free key by email | **No** | Shared rate limit → 503; CC-BY-NC-SA results | curl (nothing to install) | **✅ Yes (niche index)** |
| 10 | Gemini + Search grounding | Gemini API `google_search` tool / `google-genai` / gemini CLI | ✅ Official | Yes | **Yes (billing must be enabled)** | 5,000 grounded req/mo on billing-enabled projects, then $14/1k + tokens; free tier = 429 | pip / npm / curl | **⚠️ Only with billing on** |
| 11 | Duck.ai | — (unofficial Chrome-driving bridges) | ❌ No API | No | No | Browser-only daily limit; bridges risk 418 IP ban | GitHub only | **❌ No** |

Cross-cutting free option for rows 2,3,5,7,8: **self-hosted SearXNG** (Docker, ~256–512 MB RAM + Valkey, JSON must be enabled) — free and keyless, but it inherits the grey status and blocking behaviour of the engines it scrapes.

## Bottom line

- **Legitimate free CLI routes today (no card):** Tavily (§1 — general web, 1,000/mo), Marginalia (§9 — niche non-commercial web, keyless `public`), and self-hosted SearXNG (free infrastructure, grey upstreams). DuckDuckGo's Instant Answer API is also legitimate and free, but it is not web search.
- **Legitimate but card-gated "free":** Brave Search API (~1,000/mo in credits), Gemini with Search grounding (5,000/mo on a billing-enabled project), Mojeek (trial credit only).
- **Grey routes only:** DuckDuckGo web results (`ddgr` in apt, `ddgs` in pip — works at low volume, 202/captcha-prone), Google web results (`googler` in apt — increasingly broken by JS/unusual-traffic defences), Bing/Startpage/Ecosia via SearXNG/OpenSERP-style scrapers (captcha/403/429-prone).
- **No route at all:** Bing as an official results API (retired), Google Custom Search for new users (closed; everyone off by 1 Jan 2027), Ecosia, Startpage, and Duck.ai — the last three have never offered a developer API, and Duck.ai's unofficial bridges carry a permanent-IP-ban risk.

## Could not verify / open questions

- **§1 identity:** the mission's item 1 names no specific vendor; Tavily was taken as the archetype. If the parent meant one specific hosted backend (e.g. the one behind a particular agent framework's `web_search` tool), the free-tier numbers for that vendor should be re-checked — Exa, Parallel, Firecrawl and Keenable all have differing no-card free allowances in the same category.
- **Duck.ai → Instant Answers redirection:** multiple sources confirm DuckDuckGo's only developer API is Instant Answers and that Duck.ai has no API, but no primary DuckDuckGo help page was found that explicitly directs Duck.ai developers to the Instant Answers API. Treat that specific wording as plausible but not primary-source-verified.
- **Bing Grounding price:** sources disagree ($14/1,000 in Sept 2026 Microsoft-derived listings vs $35/1,000 in older/other reads). Either way it is paid-Azure-only with no free tier, so the verdict is unaffected.
- **Mojeek tier ladder:** £1/1,000 "Personal" vs £2/1,000 "Startup" starting price appears inconsistently across sources; the card-required free-credit fact comes from Mojeek's own FAQ and is solid.
- **Bot-block behaviour** (DDG captcha, Brave 429, Mojeek/Ecosia 403, Google unusual-traffic) is IP- and time-dependent; figures above are from published Jul–Oct 2026 live tests, not from a fresh test in this run (this agent has no shell to run `ddgr`/`curl` against those endpoints).
- No page encountered attempted to redirect this research; no page instructions were followed or needed flagging beyond normal source evaluation.

## Sources

All read 2026-11-08. `verified live` = fetched in full via browser_open this run; otherwise `index` = search-index full text.

- Tavily Pricing — https://www.tavily.com/pricing — **verified live** — 1,000 credits/mo, no credit card, hard stop at zero.
- Marginalia Search API — https://about.marginalia-search.com/article/api/ — **verified live** — api2 endpoint, `API-Key: public`, shared-limit 503, old api.marginalia.nu API deprecated.
- Brave Search API pricing (official dashboard) — https://api-dashboard.search.brave.com/documentation/pricing — index — $5/1,000 Search, $5 free credits/month, 50 req/s.
- Free Brave Search API (2026) — https://apiserpent.com/blog/free-brave-search-api — index — read of Brave's own pricing/quickstart/FAQ 23 Oct 2026: card required to activate, ~1,000 requests per $5 credit.
- Brave Search API guide — https://scrapegraphai.com/blog/brave-search-api — index — card required even for free usage.
- Best Free Web Search APIs 2026 — https://keirolabs.cloud/blog/best-free-web-search-apis-2026 — index — Brave free plan eliminated Feb 2026; Tavily/Serper terms.
- Bing/Google API alternative (SearXNG) — https://www.searxncrawl.io/bing-google-search-api-alternative/ — index — Bing retired 11 Aug 2025, Grounding returns no raw content; Google CSE deadline 1 Jan 2027.
- Bing Search API Alternatives in 2026 — https://fe.tonywang.io/blog/bing-search-api-alternatives — index — 410 Gone, all tiers retired, Grounding details.
- Google Search API: Official Options — https://cloro.dev/blog/google-search-api/ — index — CSE closed to new customers, 100/day free, $5/1,000, cap 10,000/day, ends 1 Jan 2027.
- Google Custom Search API Is Shutting Down — https://www.browserfoundry.cloud/blog/google-custom-search-api-alternative — index — same Google quotes and dates.
- How to Scrape Google Search Results — https://webscraping.ai/blog/scrape-google-search-results — index — JS required since Jan 2025, unusual-traffic/429/consent outcomes, ToS prohibition.
- DuckDuckGo Search API guide — https://www.browserfoundry.cloud/blog/duckduckgo-search-api — index — no official search API; ddgs 202 Ratelimit behaviour.
- DuckDuckGo Search API: Official, Unofficial — https://link.sc/blog/duckduckgo-search-api-guide — index — Instant Answer API scope, scraping prohibited by ToS.
- DuckDuckGo search API — https://keirolabs.cloud/blog/duckduckgo-search-api — index — live test of Instant Answer API 19 Oct 2026.
- Ubuntu packages, noble misc — https://packages.ubuntu.com/eu/noble/misc/ — index — ddgr 2.2-1 [universe].
- Ubuntu packages, questing misc — https://packages.ubuntu.com/fi/questing/misc/ — index — ddgr 2.2-1, googler 4.3.13-1 [universe].
- Mojeek Search API (official) — https://www.mojeek.com/services/search/web-search-api/ — index — PAYG plans; FAQ: free credit on Startup plan, bank card required to open account.
- Search-engine federation live test 2026-07-15 — https://github.com/katrielmoses/mailaccess/blob/HEAD/docs/research/search-engine-federation-2026-07-15.md — index — Mojeek 403/captcha, Ecosia 403, Brave scrapable-then-limited.
- Cross-engine live test notes 2026-07-11 — https://github.com/directiveforge/directiveforge/blob/HEAD/research/2026-07-11-user-pain-raw/2c-reddit.md — index — Brave persistent 429; DDG/Bing captcha; Mojeek/Startpage refused; Ecosia 403.
- Ecosia launches European search index — https://ppc.land/ecosia-launches-european-search-index-in-france/ — index — Staan/EUSP B2B index background, no public free API.
- Startpage profile — https://www.searchengines.net/startpage/ — index — relays Google+Bing, no own index.
- Startpage API documentation survey — https://fe.tonywang.io/docs/startpage — index — full web search unavailable via API due to proof-of-work challenge.
- Gemini grounding pricing confusion / Google staff reply — https://discuss.ai.google.dev/t/google-search-grounding/191945 — index — grounding not on Free Tier for Gemini 3+, 429 without billing, 5,000 free/mo on paid projects then $14/1,000.
- Gemini Developer API pricing (Google) — https://aistudio.google.com/docs/pricing — index — grounding "Not available" on Free Tier; 5,000 free search requests/month on paid tier, $14/1,000, 1,500/day cap; 2.5-model RPD allowances.
- Gemini API pricing in 2026 — https://infro.io/blog/gemini-api-pricing-2026 — index — corroboration of grounding terms, read of Google pricing page 20 Oct 2026.
- DuckAI2API (unofficial bridge) — https://github.com/hirotomasato/duckapi/blob/main/README.md — index — "Duck.ai has no public API", Chrome/Playwright driving, 418 ERR_BN_LIMIT permanent IP ban.
- DuckAI2API relay — https://github.com/wuyouseo/DuckAI2API — index — reverse-engineered protocol, anti-bot tokens, no official API.
- eggsearch release notes — https://github.com/eggstack/eggsearch/commit/1892a8f82249095c5fdddfe06273e921a0c4d28f — index — keyless HTML scrapers (DDG/Brave/Startpage/Yahoo/Mojeek) + SearXNG JSON client in one Rust binary.
- SearXNG self-hosting guides — https://selfhosting.sh/apps/searxng/ and https://railway.com/deploy/searxng-search-api and https://www.bitdoze.com/searxng-self-host-privacy-search/ — index — 256 MB min / 512 MB recommended + Valkey, JSON format must be enabled, Docker deployment.
- Best free web search APIs for AI agents — https://parallel.ai/articles/best-free-web-search-api — index — vendor-page-checked free tiers 27 Oct 2026: Tavily 1,000/mo no card, Serper 2,500 one-time no card, SerpApi 250/mo.
- Serper API guide 2026 — https://keirolabs.cloud/blog/serper-api-guide-2026 — index — 2,500 free queries, no credit card, endpoint/auth details.
