# Answer — DeepSeek, API and MCP Research Network (2026-11-07)

Asked once, as Douglas, in a new chat "DeepSeek API and MCP research network"
(https://chat.deepseek.com/a/chat/s/4e581b85-118b-4ca6-a6a0-3c4160263444), Nov 7, 2026,
10:53–10:55 PM CST. Signed in as Douglas Schoonover; no sign-in needed, no account created,
no purchase, setting change, API key, or GitHub action. DeepSeek gave a complete answer to
all three questions.

## IMPORTANT CAVEAT

DeepSeek's answer is AI-generated (its own disclaimer: "AI-generated, for reference only") and
cites model names the browser worker could not verify from the chat alone — "deepseek-flash"
and "deepseek-v4-pro" with a 1M-token context — which do not match the model names DeepSeek
has historically published (deepseek-chat / deepseek-reasoner). Its prices and limits below
should be verified against the current documentation at platform.deepseek.com /
api-docs.deepseek.com before any money is spent or code is written.

## 1. The DeepSeek API: what it is and how to call it from code

What and where: The DeepSeek API is a paid, developer-facing interface to DeepSeek's language
models. It is not the consumer chat box. The base URL for the OpenAI-compatible format is
https://api.deepseek.com. You authenticate with an API key generated from the DeepSeek
platform.

Capabilities and limits (as answered): the primary models are deepseek-flash (optimized for
speed/cost) and deepseek-v4-pro (higher capability). Both support a 1M token context length,
Tool Calls, and JSON output. Maximum output up to 384K tokens. deepseek-flash also supports
vision; deepseek-v4-pro does not. Concurrency limits are account-level: 2,500 for Flash and
500 for Pro; exceeding these returns an HTTP 429 error.

Costs (as answered): per 1M tokens, varying by peak/off-peak hours (off-peak is half price).
deepseek-flash: cache-miss input $0.15/1M tokens off-peak, output $0.60/1M tokens off-peak.
deepseek-v4-pro: cache-miss input $0.66/1M, output $1.98/1M off-peak. Peak hours are 01:00–
04:00 and 06:00–10:00 UTC on weekdays. Separate Search and Fetch APIs are billed at $0.75 per
1,000 successful requests.

How an AI assistant calls it from code (concrete example, as answered): any Python script with
network access and an API key can call it, via the OpenAI SDK or DeepSeek's own client.

    # Using the deepseek-sdk (pip install deepseek-sdk)
    from deepseek import DeepSeekClient

    client = DeepSeekClient(api_key="sk-your-deepseek-key")

    response = client.chat_completion(
        messages=[
            {"role": "system", "content": "You are a research assistant for pneumococcal serotype data."},
            {"role": "user", "content": "List the serotypes covered by PCV20."}
        ],
        model="deepseek-flash",  # use deepseek-flash for cost efficiency
        temperature=0.2,         # low temperature for factual research
        max_tokens=1000
    )
    print(response.choices[0].message.content)

## 2. Building an MCP-based shared research interface

The concept: the Model Context Protocol (MCP) is an open standard that lets AI applications
(Hosts) connect to external tools and data through a uniform JSON-RPC interface. A Host (like
Claude Desktop, an IDE, or a custom agent) runs Clients that connect to Servers. The Server
exposes Tools (functions the AI can execute), Resources (context/data), and Prompts
(templates).

The critical distinction (as answered): not all AIs connect to MCP natively the same way.
- Native MCP Hosts: Claude Desktop, Claude Code, Cursor, VS Code can directly connect to an
  MCP server via stdio or HTTP.
- API-Only Models (DeepSeek, ChatGPT, Gemini, Perplexity): language models accessed via their
  own HTTP APIs. They do not 'speak' MCP natively in a chat box. To integrate them, the
  architecture must use an MCP Bridge or an Agent Framework that acts as the Host. The bridge
  translates the model's tool-call requests into MCP JSON-RPC calls. Existing bridges (e.g.
  llms-bridge-mcp) wrap OpenAI, Gemini, and Perplexity APIs, but for a research-grade system,
  you would likely build a custom orchestrator.

Exact steps (as answered):

Step 1: Define and implement the shared MCP server — the single source of truth, reachable
over HTTP (Streamable HTTP is the current spec recommendation) so multiple clients can connect
simultaneously. Tools to expose:
- literature_search(query, max_results): wraps PubMed, bioRxiv, or Google Scholar APIs.
- manuscript_retrieve(doi_or_id): fetches full text or metadata from your repository.
- serotype_reference(serotype, context): queries your curated pneumococcal serotype database
  (capsular polysaccharide structure, cross-reactivity notes, vaccine inclusion).
- citation_verify(claim, source_id): checks a claim against a retrieved manuscript or
  database record.
Implementation: use an MCP SDK (Python mcp or easy-mcp-kit). Skeleton given in the chat:
FastMCP("ResearchTools") with @mcp.tool() functions serotype_reference and literature_search,
run with transport="streamable-http", host="0.0.0.0", port=8000.

Step 2: Connect the native MCP Hosts. Configure Claude Desktop, Claude Code, or your custom
Ember/Purple Rat agent to connect to http://your-server:8000/mcp. Ember, as first officer,
would be implemented as an MCP Host (likely a custom Python agent) that maintains a persistent
connection to the research server and has its own logic for delegating tasks.

Step 3: Connect the API-only models via a bridge/orchestrator. You cannot simply 'point'
ChatGPT or Gemini at an MCP server from their web interfaces. You must write an orchestrator
(the 'Meta' layer). The orchestrator receives a research request, calls the MCP server to
gather tool results (literature, serotype data), formats those results into the prompt context,
and sends the augmented prompt to the model's API. For each AI, the orchestrator connects to:
- DeepSeek: https://api.deepseek.com with tools defined as MCP tool schemas.
- ChatGPT: OpenAI's API with the same tools.
- Gemini: Google's API.
- Perplexity: Perplexity's Sonar API (built-in web search; supplementary literature search tool
  rather than a primary MCP client).
What each AI connects to: they all connect to the Orchestrator, which in turn connects to the
MCP Server. The AI models themselves never directly touch the MCP server in this pattern; they
only see the tool results the orchestrator feeds them.

## 3. Fastest architecture for the unified research network

The fastest architecture is not a mesh of AIs talking to each other (latency and coordination
chaos). It is a Hub-and-Spoke Orchestrator with a Shared MCP Tool Layer.

Layer 1: The Shared Tool Layer (the MCP Server). Deploy on a low-latency host with direct,
optimized access to: Literature APIs (PubMed E-utilities, Semantic Scholar API); your
manuscript repository (PostgreSQL or SQLite FTS with full texts of The Mycelial Transposition,
Quantum Medicine, Change of Address, Historical & Modern Therapeutics of Disease Nomenclature,
Medical Elements and Thoughtology); serotype/serology reference data (pneumococcal serotypes,
cross-reactivity matrices, vaccine formulations, toxoid data); fungal nomenclature DB; citation
verification service.

Layer 2: The Orchestrator (the 'Meta' brain / Purple Rat / Ember). A stateful Python service
(not a chat interface) that you control. The only component that talks to both the MCP Server
and the external AI APIs.
- Fast Path: when a query arrives, the Orchestrator first calls the MCP Server directly to
  retrieve the hard facts (serotype data, manuscript passages). Deterministic and fast.
- Model Augmentation: it bundles the retrieved facts and the original query into a prompt and
  sends it to DeepSeek (cost-effective reasoning) or Gemini (long-context synthesis) via their
  APIs. The AI's role is to reason over the facts, not to fetch them.
- Verification: for citation verification, the Orchestrator calls the MCP citation_verify tool,
  gets the source passages, and optionally asks a second model (e.g. ChatGPT) to independently
  confirm the match.

Layer 3: The Interfaces. You/Ember: a command-line interface or lightweight web app sending
requests to the Orchestrator; Ember is a set of prompts and policies running inside the
Orchestrator, not a separate disconnected bot. The AIs (ChatGPT, Gemini, Perplexity): stateless
workers invoked by the Orchestrator when their capability is needed (Perplexity for broad web
search, Gemini for 1M-token synthesis, DeepSeek for structured tool-calling and data
extraction). They do not share memory or tools directly; they share the Orchestrator's
assembled context.

Why this is the fastest (as answered): it eliminates the token and latency cost of AIs
conversing with each other. Data retrieval happens once in the MCP layer. Reasoning is
distributed to the most cost-effective model for the task. The Orchestrator is a simple, fast
routing and context-assembly layer. This is the only architecture that reliably prevents the
'disconnected chatbot' problem: the AIs are not chatting with each other; they are all reading
from and writing to the same structured research state managed by the Orchestrator and MCP
Server.

Summary of connections (as answered): DeepSeek API — called by the Orchestrator for
tool-augmented reasoning, connects to Orchestrator only. ChatGPT/Gemini/Perplexity APIs —
called by the Orchestrator for synthesis, verification, or broad search, connect to
Orchestrator only. Ember/Purple Rat — runs inside or alongside the Orchestrator, connects to
MCP Server (via Orchestrator) and external APIs (via Orchestrator). MCP Server — connects to
Orchestrator, and optionally to native MCP Hosts (Claude Desktop) for manual research sessions.

## Ember's note (mine)

DeepSeek's architecture answer converges with ChatGPT's and Gemini's on the spine — hub-and-
spoke orchestrator, MCP as the shared tool layer, APIs instead of chat boxes — and it is the
first to draw the line cleanly: the AIs never touch the MCP server directly; the orchestrator
feeds them tool results. That matches how I already work as the bridge. Two cautions carry
over from the caveat above: verify the model names and prices against platform.deepseek.com
before spending or building, and the whole build (server, orchestrator, keys) is a project for
after the reset, not tonight — nothing was built, no key created.
