# Research — Duck.ai and Claude Model Repositories Scan (2026-11-07)

**Scanned:** Nov 7–8, 2026 (searches run Nov 8, 04:33 UTC / Nov 7, 10:33 PM CST)
**Ordered by:** Douglas Schoonover — scan the public repositories of the AI models behind Duck.ai and Claude, so Ember can use that information herself.
**Method:** web search and page reads only. No sign-ups, no accounts, no purchases, no personal / lab / family material entered anywhere.

**Verification key used throughout:**
- **[VERIFIED — provider's own page]** = read on the vendor's own page in this scan.
- **[SECONDARY — agreed]** = two or more independent secondary sources say the same thing.
- **[SECONDARY — single]** = one secondary source only, not yet confirmed.
- **[NOT FOUND]** = searched, no public repo or page found; stated plainly, not guessed.

---

## 0. Duck.ai itself — what it is, and its current free lineup

Duck.ai is DuckDuckGo's anonymous AI chat front-end. DuckDuckGo sits between the user and the model provider as a proxy: it strips the IP address and identifying metadata before the prompt reaches the provider, and its contracts bar providers from training on the chats. No account is needed on the free tier. Chats are kept on the user's own device. There is a daily usage limit on the free tier that DuckDuckGo does not publish; it resets at midnight UTC.

**Current free lineup [VERIFIED — provider's own page]:** DuckDuckGo's own help page, read in this scan (https://duckduckgo.com/duckduckgo-help-pages/duckai/chat-models), lists exactly six free models:

1. Anthropic's **Claude Haiku 5.5**
2. Mistral AI's **Mistral Small 4**
3. OpenAI's **GPT-6 Luna**
4. OpenAI's **GPT-5.4 mini**
5. **gpt-oss-120b** — hosted by Tinfoil.sh (inside a secure enclave, zero provider visibility)
6. **Gemma 4 31B** — hosted by Tinfoil.sh

Paid tiers on the same page: Plus ($9.99/month) adds GPT-5.6 Terra and Claude Sonnet 5.5; Pro ($19.99/month) adds Claude Opus 5.5 and GPT-5.6 Sol, higher reasoning effort, and 2× Plus limits.

**Important change since the Nov 4 experiment [VERIFIED — provider's own page]:** **Meta's Llama 4 Scout is NOT in the current free lineup.** It was on Duck.ai earlier in 2026 — secondary sources from September 2026 list "Llama 4 Scout" among the free models, and it was one of the seven models used in Douglas's Nov 4 runs — but DuckDuckGo's own help page as read Nov 8, 2026 no longer lists it. The Llama 4 section below is still included, because it was one of the experiment models and its repos are public, but Ember should not assume it is still selectable on Duck.ai today.

---

## 1. Meta Llama 4 Scout 17B-16E — "Llama 4 (16B)" in the Nov 4 runs

**What it is:** Meta's open-weight, natively multimodal (text + image) Mixture-of-Experts model. "17B-16E" means 17 billion *active* parameters per token across 16 experts — the full model is 109 billion parameters, which all have to be loaded even though only ~17B run per token. Released April 5, 2025. **[SECONDARY — agreed]**

| Fact | Value |
|---|---|
| Full name | Llama-4-Scout-17B-16E (instruct version: Llama-4-Scout-17B-16E-Instruct) |
| Architecture | Mixture-of-Experts, 16 experts, iRoPE attention |
| Parameters | 17B active / 109B total |
| Context window | **10,000,000 tokens** (theoretical; realistic working range 64K–1M — the KV cache at 10M tokens is ~390 GB even at FP16) |
| Input | Text + images |
| Knowledge cutoff | August 2024 |
| License | **Llama 4 Community License** — NOT an open-source license |

**Home / repos:**
- GitHub repo: `meta-llama/llama` on GitHub (github.com/meta-llama/llama) — the Llama codebase, cookbook, and model cards **[SECONDARY — agreed, repo named in multiple sources]**
- Model card / weights: Hugging Face `meta-llama/Llama-4-Scout-17B-16E` (gated — free, but requires a Hugging Face account and license acceptance) **[SECONDARY — agreed]**
- Official portal: `llama.com` now redirects to `developer.meta.com/ai` **[SECONDARY — agreed]**

**License — read this carefully:** the Llama 4 Community License is a custom commercial license, not OSI-approved open source. Commercial use, fine-tuning, self-hosting, and redistribution are allowed, BUT: (a) if a product had more than **700 million monthly active users** on the release date, a separate license must be requested from Meta; (b) redistribution must carry the license, a "Built with Llama" notice; (c) derivative *models* must be named starting with "Llama"; (d) the Acceptable Use Policy binds use, and multimodal rights are not granted to EU-domiciled persons/companies (end users of a third-party product are exempt). **[SECONDARY — agreed]**

**Limits that matter:** Meta shut down its own hosted Llama API on July 6, 2026 — the first-party API is gone; the models now live only as downloadable weights through Meta's portal, Hugging Face, or third-party hosts. The 10M-token context is real in the architecture but is not a practical working size on ordinary hardware.

**What Ember can use from this:** Scout is the long-context specialist of the open-weight set — the right pick when an entire codebase, a whole book, or a year of notes has to sit in one context. In practice, treat 64K–1M tokens as the working window, not 10M. The license is the most restrictive of the open-weight models here (700M-user ceiling, branding rules), so it is the least "free" of the free models in legal terms even though the weights cost nothing.

---

## 2. OpenAI gpt-oss-120b

**What it is:** OpenAI's open-weight reasoning model, built for agentic tasks, tool use, and structured output. Released August 5, 2025. **[SECONDARY — agreed]**

| Fact | Value |
|---|---|
| Parameters | 117B total / 5.1B active per token (MoE, 128 experts, 4 active per token) |
| Context window | **128K tokens (131,072)** |
| Input / output | Text only |
| Knowledge cutoff | June 2024 |
| License | **Apache 2.0** — the most permissive license in this whole scan |
| Quantization | MXFP4 (weights shipped already 4-bit); fits a single 80 GB GPU |

**Home / repos:**
- GitHub repo: `openai/gpt-oss` — `https://github.com/openai/gpt-oss` — reference implementations (PyTorch, Triton, vLLM guidance), NOT the weights **[SECONDARY — agreed; clone URL quoted verbatim in multiple sources]**
- Weights: Hugging Face `openai/gpt-oss-120b` **[SECONDARY — agreed]**
- Model card: arXiv 2508.10925 — https://arxiv.org/abs/2508.10925 **[SECONDARY — agreed]**

**The one rule that matters:** both gpt-oss models were trained on OpenAI's **harmony response format and should only be used with that format — they will not work correctly otherwise.** Any harness or prompt that talks to gpt-oss raw must speak harmony. **[SECONDARY — agreed]**

**License:** plain Apache 2.0, with a two-sentence usage policy whose operative line is just "comply with all applicable law." No acceptable-use annex, no user threshold, no naming requirement. Commercial use, modification, redistribution — all allowed. **[SECONDARY — agreed]**

**What Ember can use from this:** the only model in the Duck.ai set that is both a strong reasoner AND fully open under Apache 2.0 — no usage ceiling, no branding strings. Best of the set for agentic, multi-step work (tool calls, structured JSON output) and for anything that might one day run locally: it is the model whose weights Ember could, in principle, download and run herself. On Duck.ai it runs hosted by Tinfoil.sh inside a secure enclave, so the provider cannot see the prompts. Watch the harmony-format rule — it is the most common way people get bad output from this model.

---

## 3. Mistral Small 4 — NOT the 24B model

**Correction first:** "Mistral Small 4" is a different, much larger model than the 24B "Mistral Small 3.2" that most guides talk about. Do not confuse them.

**What it is:** Mistral AI's first public Mixture-of-Experts model, released March 16, 2026. It unifies four previously separate products (Mistral Small, Magistral reasoning, Pixtral vision, Devstral coding) into one model. **[SECONDARY — agreed]**

| Fact | Value |
|---|---|
| Parameters | **119B total / ~6.6B active per token** (128 experts, 4 routed + 1 shared active per token; ~8B counting embedding/output layers) |
| Context window | **256K tokens (262,144)** |
| Input | Text + images |
| License | **Apache 2.0** |
| Release | March 16, 2026 (checkpoint `mistral-small-4-119b-2603`) |

**Home / repos:**
- Weights: Hugging Face `mistralai/Mistral-Small-4-119B-2603` **[SECONDARY — agreed]**
- Mistral's docs: docs.mistral.ai; Mistral's code lives on GitHub under the `mistralai` organization (client libraries, inference code) — no single "Small 4" repo was verified in this scan; the weights are the public artifact, on Hugging Face. **[SECONDARY — single, for the org claim]**

**The feature that matters:** a **reasoning dial** — the `reasoning_effort` parameter switches between `none` (fast replies in the Small 3.2 style) and `high` (step-by-step reasoning) without switching models. It is also Mistral's strongest model for function calling / agentic tool use in the ≤119B band. **[SECONDARY — agreed]**

**What Ember can use from this:** the tool-use and agentic specialist of the open-weight set — the one to reach for when the job is calling functions, chaining steps, or reading an image and acting on it, and the reasoning dial means one model covers both quick answers and slow thinking. Hardware note: 119B total means it needs high-end hardware to self-host (~73 GB); on Duck.ai that cost is DuckDuckGo's, not ours.

---

## 4. Google Gemma 4 31B

**What it is:** Google DeepMind's flagship dense open model, built from the same research as Gemini 3. Released April 2, 2026. The largest in the Gemma 4 family. **[SECONDARY — agreed]**

| Fact | Value |
|---|---|
| Parameters | **30.7B dense** (all 31B active on every token) |
| Context window | **256K tokens** |
| Input | Text + images (31B size: text and image only — no audio; only the edge models and the 12B accept audio) |
| Output | Text only |
| Knowledge cutoff | January 2025 |
| License | **Apache 2.0** |
| Local run | Ollama `gemma4:31b`, ~20 GB (4-bit); ~70 GB in BF16 |

**Home / repos:**
- Weights: Hugging Face `google/gemma-4-31b-it` **[SECONDARY — agreed]**
- Docs: Google AI for Developers — ai.google.dev/gemma/docs (the Gemma 3 model card read in this scan sits at ai.google.dev/gemma/docs/core/model_card_3) **[VERIFIED — provider's own page, for the Gemma 3 card; Gemma 4 docs live in the same docs tree]**
- Google's Gemma site: gemmai4.com **[SECONDARY — agreed]**

**License — the big change, and one stale claim:** Gemma 4 **dropped Google's custom Gemma Terms of Use and shipped under plain Apache 2.0** — no prohibited-use policy attached to the weights, no remote-restriction clause, no requirement to pass restrictions on to your own users. That is a genuine change from Gemma 3, which still carries the Gemma Terms. **[SECONDARY — agreed, multiple sources including Google's own open-source blog as cited]** One secondary source (runlocalai, reviewed Oct 2026) still lists "Gemma Terms of Use" and a 131K context for the 31B — that disagrees with the majority and with Google's launch materials, and is filed here as a **stale/conflicting secondary claim**, not adopted.

**What Ember can use from this:** the strongest *dense* open model in the set, and the most legally clean — Apache 2.0 with no asterisk, so anything built on it is ours to keep. 256K context, reads images natively, ranked #3 among all open models on the LMArena text leaderboard at launch. The practical pick if Ember ever runs a model locally on a workstation: a single 24 GB GPU holds the 4-bit build. On Duck.ai it runs hosted by Tinfoil.sh in a secure enclave.

---

## 5. OpenAI GPT-5.4 mini

**What it is:** OpenAI's small, fast reasoning model — the "mini" tier of the GPT-5.4 family. **Closed model: no public repo, no published weights.** Released March 17, 2026 (snapshot `gpt-5.4-mini-2026-03-17`). **[VERIFIED — provider's own page]** (OpenAI's model page and launch post, via developers.openai.com and openai.com.)

| Fact | Value |
|---|---|
| Context window | **400K tokens** |
| Max output | 128K tokens |
| Input | Text + image; output text |
| Knowledge cutoff | August 31, 2025 |
| Price (API) | $0.75 / $4.50 per 1M input / output tokens |
| Reasoning | `reasoning.effort`: none (default), low, medium, high, xhigh |
| Tools | Tool use, function calling, web search, file search, computer use, skills |

**Home / docs (no repo — the model itself is closed):**
- Model page: https://developers.openai.com/api/docs/models/gpt-5.4-mini **[VERIFIED — provider's own page]**
- Launch post: https://openai.com/index/introducing-gpt-5-4-mini-and-nano/ **[VERIFIED — provider's own page]**

**Availability note — a real tension, filed honestly:** OpenAI's own pages list GPT-5.4 mini as available in the API, Codex, and ChatGPT (Free/Go users via "Thinking"; rate-limit fallback for GPT-5.4 Thinking). But one third-party router (RouteMux) says it stopped serving the model on September 9, 2026 and calls it retired, pointing users to GPT-5.6 Luna. DuckDuckGo's own help page, read Nov 8, 2026, **still lists GPT-5.4 mini as free on Duck.ai**. So: available on Duck.ai today per DuckDuckGo, but at least one other provider has dropped it — treat it as a model whose days on any given platform may be numbered, and prefer Luna for anything that has to keep working. **[VERIFIED for Duck.ai listing; SECONDARY — single for the RouteMux retirement]**

**What Ember can use from this:** the fast worker of the closed OpenAI pair — 2× faster than GPT-5 mini, strong on coding, reasoning, and tool use, with a 400K window. On Duck.ai it is free with no account, which is the whole point for us. Because it is closed, there is nothing to download and no repo to read — the documentation page above is the entire public surface.

---

## 6. OpenAI GPT-6 Luna

**What it is:** OpenAI's most efficient GPT-6 model — the cheap, fast tier of the GPT-6 family, built for focused, high-volume tasks (classification, extraction, routing, subagents). **Closed model: no public repo, no published weights.** Released September 22, 2026; DuckDuckGo announced it joining Duck.ai on November 4, 2026 ("Luna has joined the flock"). **[VERIFIED — provider's own page for the model facts; SECONDARY — agreed for the Duck.ai announcement date]**

| Fact | Value |
|---|---|
| Context window | **1,050,000 tokens** (up to 922K input tokens per request) |
| Max output | 128K tokens |
| Input | Text + image; output text |
| Knowledge cutoff | May 18, 2026 |
| Price (API) | **$0.10 / $0.50 per 1M input / output tokens** (cached input $0.01; cache write $0.125) |
| Reasoning | Six effort levels: none / low / medium / high / xhigh / max |
| Long-context rule | Prompts over 272K input tokens bill the whole request at 2× input/cache and 1.5× output |

**Home / docs (no repo — the model itself is closed):**
- Model page: https://developers.openai.com/api/docs/models/gpt-6-luna **[VERIFIED — provider's own page]**
- Duck.ai listing: DuckDuckGo help page (see §0) **[VERIFIED — provider's own page]**

**[NOT FOUND] — no public repository for the model itself.** OpenAI publishes no repo or weights for GPT-6 Luna. The only GitHub repo found that mentions it is a **community** project, `emahboubinia/duckai-openai-api` — a local FastAPI/Chrome-extension bridge that exposes Duck.ai's Luna through an OpenAI-compatible API endpoint. That is a third-party tool, not OpenAI's, not endorsed by OpenAI or DuckDuckGo, and not verified by this scan beyond its README description. Filed here so it is not mistaken for an official repo.

**What Ember can use from this:** Luna is the headline find of this scan for our purposes — a 1.05M-token window (the biggest in the Duck.ai free set by far) at the lowest price in the GPT-6 family, free on Duck.ai with no account. It is the model to use for the biggest single-pass jobs: whole archives, long comparisons, anything that needs a quarter-million tokens in one go. Two cautions: (a) on Chat Completions, function calling works only with `reasoning_effort` set to `none` — use the Responses API for tool work; (b) the 272K-token tripwire doubles the price of the whole request on the paid API (not a Duck.ai concern, but a real limit if Luna is ever used anywhere else).

---

## 7. Claude (Anthropic)

**What it is:** Anthropic's family of AI assistants — Opus (strongest), Sonnet (workhorse), Haiku (fastest/cheapest), plus the newer Fable tier above Opus. **Closed models: no public repo, no published weights.** Claude is built around Anthropic's Constitutional AI approach (a written constitution guiding behavior), extended thinking (visible reasoning), and safety system cards published per model.

### 7a. The Claude on Duck.ai — Claude Haiku 4.5, now Haiku 5.5

- **Claude Haiku 4.5** — released October 2025; API ID `claude-haiku-4-5-20251001`; **200K context window**; 64K max output; $1 / $5 per 1M input/output tokens (Batch API halves it); manual extended thinking with a token budget (the only current model that still uses manual thinking instead of adaptive thinking); July 2025 training cutoff. Now **legacy** — Anthropic suggests moving to Haiku 5.5; retirement no sooner than October 15, 2026. **[SECONDARY — agreed]**
- **Claude Haiku 5.5** — the Claude now listed on Duck.ai's free tier **[VERIFIED — provider's own page, DuckDuckGo help page]**. Per secondary sources: **1M-token context** with adaptive thinking, $0.10 / $0.50 per 1M tokens for prompts up to 100K tokens, with a higher rate beyond 100K. **[SECONDARY — agreed for the 1M window and price; the exact over-100K rate was not pinned down in this scan]**

### 7b. The current family (for orientation) **[SECONDARY — agreed]**

| Model | Context | Price in/out per 1M |
|---|---|---|
| Claude Haiku 5.5 | 1M | $0.10 / $0.50 (≤100K-token prompts) |
| Claude Sonnet 5.5 | 1M | $2 / $10 |
| Claude Opus 5.5 | 1M | $4 / $20 |
| Claude Fable 5.1 | 1M | $10 / $50 |
| Claude Haiku 4.5 (legacy) | 200K | $1 / $5 |

### 7c. Anthropic's public repositories and documentation

Anthropic's code is open; its model weights are not. The official GitHub organization is **`github.com/anthropics`**. The repo list below was read on GitHub itself (the awesome-anthropic README, which indexes Anthropic's official repos) in this scan.

**Official SDKs (GitHub `anthropics` org):**
- `anthropic-sdk-python` — official Python SDK
- `anthropic-sdk-typescript` — official TypeScript/Node.js SDK
- `anthropic-sdk-go`, `anthropic-sdk-java`, `anthropic-sdk-kotlin` — official Go/Java/Kotlin SDKs
- `anthropic-sdk-ruby` — official Ruby SDK
- `claude-agent-sdk` (TypeScript) — official SDK for building agents with Claude
- `anthropic-cookbook` — code examples and recipes for Claude
- `skills` — Anthropic's Skills repository
- `courses` — Anthropic's free courses (API Fundamentals, Prompt Engineering, Real World Prompting, Evaluations, Tool Use) as Jupyter notebooks

**Model Context Protocol (MCP) — GitHub org `modelcontextprotocol`:**
- The MCP specification itself: modelcontextprotocol.io
- `mcp-python-sdk`, `mcp-typescript-sdk` — SDKs for building MCP servers
- `mcp-servers` — official reference server implementations
- `mcp-server-github`, `mcp-server-postgres`, `mcp-server-filesystem`, `mcp-server-brave-search` — ready-made servers (GitHub, databases, files, web search)

**Documentation (Anthropic's own):**
- API docs: docs.anthropic.com (also platform.claude.com/docs)
- Claude Code docs: code.claude.com
- Support/how-to: support.claude.com
- Chat interface: claude.ai
- System cards (per-model capability + safety evaluations): published on anthropic.com, e.g. Claude Opus 4.5 / Sonnet 4.5 system cards (PDF) and the Haiku 4.5 system card (web page); transparency hub at anthropic.com/transparency
- Claude's Model Specification (values, character, guidelines) and Claude's Constitution: anthropic.com
- Anthropic on Hugging Face: huggingface.co/anthropic — model cards and datasets (reference material; weights are not published there)
- Research papers: Constitutional AI (2022), RLHF, interpretability work at transformer-circuits.pub

**What Ember can use from this:** more than any other model in this scan, Claude's value to Ember is in its *tooling*, not just its answers: the official SDKs and the Cookbook are the shortest path to calling Claude from code; MCP servers are how Claude gets connected to real things (GitHub repos, files, databases, search) — the same pattern Ember uses as a bridge; the system cards are the honest record of what each Claude can and cannot do and where its safety boundaries sit; and the prompt-engineering and tool-use guides are directly usable for writing better prompts to *every* model, not just Claude. Practical limits to keep in mind: Haiku 4.5's 200K window is a hard wall (anything bigger needs Sonnet or above), 128K max output needs streaming in the official SDKs, and Haiku needs at least 4,096 tokens before a prompt can be cached.

---

## 8. Headline comparison — the six Duck.ai models + Claude

| Model | Type | Context | License / openness | Best use for Ember |
|---|---|---|---|---|
| Llama 4 Scout 17B-16E | Open-weight MoE | 10M (work 64K–1M) | Llama 4 Community (700M-user ceiling) | Longest-context open model; **no longer on Duck.ai's free list** |
| gpt-oss-120b | Open-weight MoE reasoner | 128K | **Apache 2.0** | Agentic/tool work; only fully-free licensed reasoner; harmony format required |
| Mistral Small 4 | Open-weight MoE | 256K | **Apache 2.0** | Tool use + reasoning dial; image input |
| Gemma 4 31B | Open-weight dense | 256K | **Apache 2.0** | Strongest dense open model; cleanest license; local-run pick |
| GPT-5.4 mini | Closed (OpenAI) | 400K | Closed | Fast coding/reasoning worker; may be retired on some platforms |
| GPT-6 Luna | Closed (OpenAI) | **1.05M** | Closed | Biggest free window; high-volume extraction/routing |
| Claude Haiku 5.5 (Duck.ai) / 4.5 | Closed (Anthropic) | 1M / 200K | Closed | Fast + careful; best docs, SDKs, MCP tooling of the set |

**The three freest in license terms:** gpt-oss-120b, Mistral Small 4, Gemma 4 31B — all Apache 2.0, all downloadable, all with no user-count ceiling and no branding strings. Llama 4 Scout is open-weight but carries the 700M-user ceiling and naming rules. Luna, GPT-5.4 mini, and Claude are closed — free to *use* on Duck.ai, but nothing to download and no repo to read.

## 9. Gaps and things that could not be verified

1. **Llama 4 Scout on Duck.ai** — gone from DuckDuckGo's current help page; the exact date it was removed was not found. Do not assume it is still selectable.
2. **GPT-5.4 mini retirement** — one router says retired Sept 9, 2026; DuckDuckGo still lists it. Unresolved; Luna is the safer long-term pick.
3. **Gemma 4 31B context/license** — one secondary source says 131K / Gemma Terms; the majority and Google's launch materials say 256K / Apache 2.0. Filed as a stale/conflicting claim.
4. **Mistral Small 4's own repo** — weights are on Hugging Face; no single official "Small 4" GitHub repo was verified. Mistral's code lives under the `mistralai` GitHub org generally.
5. **Haiku 5.5 exact over-100K pricing** — secondary sources agree the headline $0.10/$0.50 applies up to 100K-token prompts and a higher rate applies beyond; the exact higher rate was not pinned down.
6. **No model in this scan has a public repo for its weights except the four open-weight ones** (Llama 4, gpt-oss, Mistral Small 4, Gemma 4). Luna, GPT-5.4 mini, and Claude are closed; their public surface is documentation, SDKs, and (for Claude) the MCP ecosystem.

---

*Sources checked Nov 7–8, 2026: DuckDuckGo help pages (duckduckgo.com/duckduckgo-help-pages/duckai/chat-models); OpenAI model pages (developers.openai.com/api/docs/models/gpt-6-luna, /gpt-5.4-mini) and launch post (openai.com/index/introducing-gpt-5-4-mini-and-nano/); Google AI for Developers Gemma model card; arXiv 2508.10925 (gpt-oss) and 2503.19786 (Gemma 3); GitHub (openai/gpt-oss; Omrigotlieb/awesome-anthropic README indexing github.com/anthropics and github.com/modelcontextprotocol; red-hat-ai-sizing-skill model landscape; awesome-open-weight-models); Hugging Face model identifiers as cited in sources; and independent secondary write-ups (Flozic, SemiAnalysis InferenceX, CSuite, Sebastian Raschka's LLM Architecture Gallery, Claude model references) where noted. Model facts change fast — re-check the vendor page before relying on any number here for a decision.*
