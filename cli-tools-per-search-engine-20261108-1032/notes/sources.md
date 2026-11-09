# Sources read 2026-11-08 (index unless noted)

- Tavily pricing VERIFIED LIVE via browser_open https://www.tavily.com/pricing — Researcher Free: 1,000 credits/mo, no credit card required; requests stop when exhausted.
- Marginalia API VERIFIED LIVE via browser_open https://about.marginalia-search.com/article/api/ — new API api2.marginalia-search.com, header API-Key, key `public` usable, often rate-limits; old api.marginalia.nu/public/ deprecated, shared limit -> HTTP 503.
- Brave official pricing via search index https://api-dashboard.search.brave.com/documentation/pricing — Search $5/1,000, includes free $5 credits every month, 50 req/s. Card-required corroborated by multiple Oct 2026 reads of Brave quickstart/FAQ (apiserpent, scrapegraphai, apidog).
- Brave free plan removed Feb 2026: multiple sources (keirolabs, softbrixai, parallel) agree old 2,000/mo (later 5,000) free plan replaced Feb 12 2026 by $5 metered credit, card required, attribution required.
- Bing retired: Microsoft quote repeated across sources: retired Aug 11 2025, decommissioned, no new signup; endpoints 410 Gone; replacement Grounding with Bing Search in Azure AI Agents/Foundry, no raw results access, $14/1,000 transactions per Sept 2026 Microsoft listing (older/alternate listings $35/1k — discrepancy noted).
- Google CSE: Google overview quoted: closed to new customers, existing until Jan 1 2027, 100 free/day then $5/1,000 cap 10k/day; new engines since Jan 20 2026 limited to 50 sites.
- Gemini grounding: Google staff on discuss.ai.google.dev — NOT available on Free Tier for Gemini 3+, 429 without billing; paid projects get 5,000 free search req/mo shared, then $14/1,000. Google pricing page via aistudio.google.com/docs/pricing corroborates 5,000 free on paid tier, 'Not available' in Free Tier column. Gemini 2.5: 500 RPD free shared Flash/Flash-Lite in pricing-for-tools, but new users report 404 for 2.5 models.
- DDG: no official web search API; Instant Answer API api.duckduckgo.com free no key, abstracts only. ddgs (pip, formerly duckduckgo_search) scrapes, RatelimitException 202. ddgr scrapes DDG html version, states not affiliated.
- Ubuntu apt: packages.ubuntu.com noble misc lists ddgr 2.2-1 universe; questing lists ddgr 2.2-1 and googler 4.3.13-1 universe. Debian bookworm ddgr 2.1-1, googler 4.3.13-1.
- Google scraping: plain HTTP mostly fails, JS required since Jan 2025, unusual traffic / 429 / consent; ToS prohibits automated access.
- Mojeek official https://www.mojeek.com/services/search/web-search-api/ — PAYG plans, FAQ: free credit on Startup plan but bank card required to open account. Live tests: bare HTML 403, browser UA -> captcha/ALTCHA page.
- Ecosia: no self-serve developer search API found; live tests 403 (MailAccess 2026-07-15, directiveforge). Staan/EUSP is B2B index infrastructure, no free public API documented.
- Startpage: front-end relaying Google+Bing, no API; strong anti-abuse/captcha, proof-of-work; live tests flatly refused.
- SearXNG: self-hosted metasearch, Docker, JSON format must be enabled (else 403), 256 MB min / 512 MB recommended + 50-100 MB Valkey, aggregating 70+ engines; public instances usually disable JSON.
- eggsearch: single Rust binary/MCP, keyless HTML scrapers for DDG/Brave/Startpage/Yahoo/Mojeek + SearXNG JSON client.
- Duck.ai: unofficial bridges (duckapi, DuckAI2API) state explicitly 'Duck.ai has no public API', drive real Chrome/Playwright, anti-bot tokens, per-IP permanent ban 418 ERR_BN_LIMIT, free tier anonymous daily limit.
- Serper: 2,500 free queries one-time, no card, google.serper.dev/search X-API-KEY; SerpApi 250 searches/mo free.
