# Answer — Duck.ai, Features, Back-End Interfaces, RCS, Workarounds, AI Secrets (2026-11-07)

Asked once, as Douglas, in a new chat ("Duck.ai capabilities and integrations"), Nov 7, 2026,
10:50–10:52 PM CST. Answering model: Mistral Small 4 (the chat's default). Full exported chat
saved as browser download `duck.ai_2026-11-07_22-52-09.txt` (12 KB). No personal, lab, or
family material sent; no settings changed, no purchases, no new accounts.

## 1. All Features + Fastest Way to Use It

Core capabilities (as answered): web search with citations; model switching (Claude Haiku 5.5,
Mistral Small 4 default, GPT-6 Luna, GPT-5.4 mini, gpt-oss-120b, Gemma 4 31B); no account
needed; free with a daily cap; image generation; chat history stored locally in the browser;
export/share chats; voice dictation; follow-up suggestions; second opinion from another model
without a new chat.

Hidden / less-used features (as answered): file uploads (PDFs, TXT, CSV, DOCX); temperature
control by appending 'temperature=0.3' to a prompt; multi-turn context; copy-as-Markdown;
custom instructions in Settings > Chat; plugins/extensions (calculator, unit converter);
code execution (Python, R, shell) in chat; Prompt Library; model aliases ('/claude',
'/mistral', '/gpt6').

Fastest way (as answered): Mistral Small 4 for quick queries, GPT-5.4 mini for drafts,
Claude Haiku 5.5 or gpt-oss-120b for deep research; follow-up suggestions to continue;
web search on for citations; export immediately — history is browser-local.

## 2. Back-End Interfaces — API / MCP / CLI?

Short answer: Duck.ai does NOT have a public API, MCP server, or CLI. DuckDuckGo also has no
official public API for AI chat.

Workarounds (as answered):
- A. Reverse-engineer DuckDuckGo's proxy: intercept network requests and call
  `https://duck.ai/api/chat` directly. Flagged by the model itself as possibly violating
  DuckDuckGo's ToS — use at own risk.
- B. Browser automation (Selenium/Playwright) to drive the chat UI programmatically.
- C. DuckDuckGo search via `https://duckduckgo.com/html/?q=...`.
- D. Together.ai's API — many Duck.ai models are hosted by Together; needs an API key.
- Best recommended (as answered): B (browser automation) or D (Together.ai), as more stable
  and not risking ToS.

## 3. RCS Connections

Short answer: No. Duck.ai doesn't support RCS or any direct messaging channels.

Alternative channels (as answered): a WebSocket server bridging Ember and Duck.ai; MQTT for
lightweight bidirectional messaging; Discord/Slack bots forwarding messages via browser
automation. Best for Ember (as answered): WebSocket bridge or Discord bot — real-time,
low-latency, easy to build and secure.

## 4. Workarounds: Things That Look Impossible but Work

- URL parameters to pre-fill prompts (e.g. `https://duck.ai/?q=pneumococcal+serotypes`).
- Ask for output as JSON or Markdown tables for parsing.
- Treat the chat as an API: paste a script and ask it to modify/run it.
- Model chaining mid-conversation ('/gpt6' then '/claude').
- Text box as an API: paste structured data (CSV) and ask it to process it.
- Prompt injection for focus: a custom instruction enforcing a format.
- Hard-code data: paste research notes or a serotype list as a temporary knowledge base.
- Markdown tables for data-heavy tasks.
- OCR: upload an image of handwritten notes and ask for transcription.

## 5. AI Secrets — Tips & Tricks for Ember's Research

Model specialization (as answered): Claude Haiku 5.5 for rigorous reasoning, manuscript
drafting, complex medical analysis; gpt-oss-120b for literature reviews and long-form analysis;
Mistral Small 4 for quick fact-checks and structured summaries; Gemma 4 31B for multilingual
research and medical terminology recall; GPT-6 Luna for creative/narrative tasks
(e.g. Quantum Medicine).

Tricks (as answered): temperature control ('temperature=0.2' factual, 'temperature=0.8'
creative); document parsing via upload; task decomposition into subtasks; follow-ups instead
of new chats; prompt templates per manuscript (serotype, vaccine/toxoid, serology
cross-reference, fungal replacement therapy); version control by exporting chats to GitHub as
dated markdown; chain-of-thought prompting ("think step by step").

Final recommendations (as answered): Duck.ai is privacy-first and anonymous — Ember must keep
her own research logs; cross-link via shared GitHub repos; WebSocket bridge or Discord bot for
speed; always web search + export to GitHub; plain text is king (.md, .txt).

## Verification notes — read before acting on the above

These are the browser worker's own verification notes, carried here in full because they
change what can be trusted:

- No public API/MCP/CLI is the direct answer; the rest is workarounds, not an official
  interface.
- The reverse-engineered call to `https://duck.ai/api/chat` was the model's own suggestion,
  flagged by it as possibly violating DuckDuckGo's ToS. It was NOT tested or implemented, and
  is NOT recommended.
- Several "undocumented capability" claims could not be verified from the Duck.ai interface
  actually used, and two conflict with what was observed: only PDF upload was seen offered in
  the UI (not TXT/CSV/DOCX), and no in-chat code execution, plugins, temperature parameter,
  model-alias commands, or Prompt Library controls were seen. The image generation claim is
  unverified (the sidebar does have a "New Image" button, so image creation exists; "via
  DALL-E or Flux" is unverified). Treat all undocumented-capability claims as the answering
  model's assertions, not confirmed facts.
- The Together.ai route is a separate provider needing its own API key/account; nothing was
  set up.
- The WebSocket/MQTT/Discord/Slack bridge ideas are recommendations only; nothing was built.

## Ember's note (mine)

Duck.ai agrees with Gemini on the shape of the answer — no RCS anywhere, WebSockets/MCP are
the real channels — but it adds two things worth keeping: model specialization per task
(Haiku 5.5 for the hard reasoning, gpt-oss-120b for long literature work, Luna for the
creative manuscripts) and the prompt-template idea per manuscript. The honest limit is the
verification notes above: the flashy hidden features are unverified and two look wrong
against the UI we actually used, and the reverse-engineered API call is a terms-of-service
risk I will not use. Browser automation and Together.ai (with its own key, his call) are the
clean routes if we ever want Duck.ai without the chat box.
