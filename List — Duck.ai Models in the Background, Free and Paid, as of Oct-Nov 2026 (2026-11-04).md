# List — Duck.ai Models in the Background, Free and Paid, as of Oct–Nov 2026

**Direct answer:** Duck.ai is not one model. DuckDuckGo sits between you and the model provider as an anonymizing proxy — it strips your IP and identifying metadata before forwarding the prompt, and contracts with providers prohibit them from training on or retaining the conversation beyond the stated window. You pick one model per chat from a menu, and you can switch mid-task. The model list changes as DuckDuckGo updates it, so the picker on duck.ai is the final check on the day you use it.
**Source:** DuckDuckGo Duck.ai help pages, as summarized in Oct 2026 guides, plus the Nov 4, 2026 Duck.ai share in this workspace (final response named as Gemma 4 31B).
**Method note, Research Logic & Evidence Framework §6:** Model name, provider, and hosting are three separate fields. A model name alone does not prove the provider, and a provider name alone does not prove the hosting. Tinfoil-hosted open models are a different hosting field from direct provider infrastructure.

## How it works in the background

- DuckDuckGo acts as an anonymizing proxy, stripping your IP before your prompt reaches the model provider, and its official privacy page says chats are not used for AI training by DuckDuckGo or the underlying model providers.
- Per DuckDuckGo help pages, providers agree to Zero Data Retention in the dev.to summary: prompts and responses deleted immediately after the reply is generated, with documented exceptions — prompt caching by OpenAI/Anthropic holding a chat in short-term memory for up to an hour is noted as an exception in that guide, and DuckDuckGo's own terms, in another guide, say providers do not train on prompts and delete them within 30 days, with limited exceptions. Those two wordings differ — treat the exact retention window as "check DuckDuckGo's current privacy page," not as a single settled number in this file.
- Recent chats are saved on your own device, not on DuckDuckGo's servers, per the guides.
- Free tier has a daily cap, resetting at midnight UTC per one guide. Paid tiers raise it.

## Free models — current list, Oct 2026 help pages

| Model | Provider / hosting | Best for, per guides |
|---|---|---|
| GPT-6 Luna | OpenAI | Default, best for everyday use, per DuckDuckGo help-page summary |
| GPT-5.4 mini | OpenAI | Quick and light |
| GPT-5.4 nano | OpenAI | Listed in several Oct 2026 guides as a free option, alongside mini — the help-page summary above lists Luna + mini, other guides list nano + mini. Model picker on the day is the check. Do not treat nano vs. Luna as settled from guides alone. |
| Claude Haiku 4.5 (Claude 4.5 Haiku) | Anthropic | Careful writing and summaries |
| Mistral Small 4 (Mistral Small) | Mistral AI (French company) | General chat, EU-hosted research in other guides |
| gpt-oss-120b | Open model, hosted by Tinfoil.sh in sealed / confidential hardware, provider no view of chats per DuckDuckGo description | Open-weight, larger reasoning |
| Gemma 4 31B | Google Gemma open model, hosted by Tinfoil.sh, same sealed-hardware note | Open-weight. **This is the model named in the final response of Douglas's Nov 4, 2026 Duck.ai share** — so that particular chat was a Gemma 4 31B chat, not a GPT or Claude chat. |

Total free, per guides: six models to switch between, no account, no server-side chat history in the dev.to summary.

## Paid models — DuckDuckGo Plus and Pro, Oct 2026 guides

| Tier | Price, per guides | Adds, per guides |
|---|---|---|
| Plus | $9.99 / month or $99.99 / year | GPT-5.6 Terra (OpenAI) and Claude Sonnet 5.5 in the official help-page summary; another guide lists Claude Sonnet 4.6 — version number differs by guide, check picker. Higher usage than free. |
| Pro | $19.99 / month or $199.99 / year | Everything in Plus, plus Claude Opus 5.5 in the help-page summary (Opus 4.8 in another guide — version differs by guide), and GPT-5.6 Sol (OpenAI), higher reasoning effort than Plus, and 2x higher usage limits than Plus. |

## Older / historical models — NOT current free list, do not cite as current

- GPT-4o mini (OpenAI), Claude 3.5 Haiku (Anthropic), Meta Llama 3.3, Mistral Mixtral — listed in older DuckDuckGo AI Chat lineups. Model availability can change as providers update offerings. If a guide from early 2026 lists these, it is describing an older lineup, not the Oct 2026 free list above.

## What this list does NOT prove

- It does not prove which model answered any given Duck.ai chat, except where the page itself names the model — as it did for Gemma 4 31B in Douglas's Nov 4 share.
- It does not prove that a model name in a guide is still live today — DuckDuckGo's picker is the authoritative check.
- It does not treat "DuckDuckGo" as a model maker. DuckDuckGo makes the privacy proxy and the interface; OpenAI, Anthropic, Mistral, Google (Gemma), and the open-weight hosts make the models.
