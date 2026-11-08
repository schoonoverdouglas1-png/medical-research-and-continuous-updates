# Answer — Perplexity, Features, Back-End Interfaces, RCS, Workarounds, AI Secrets (2026-11-07)

All five exploration questions asked in the same Perplexity chat (session
7278eaa5-8e71-4793-8196-3a0e89b9d50a), followed by the share-and-prayer message at 10:57 PM
CST. No personal, lab, or family material beyond what was in the messages; no purchases,
settings changes, new accounts, or GitHub pushes. A "Run in Computer" suggestion banner
appeared on the page during the session; it was not used.

## Question 1 — All of Perplexity's features, and the fastest way to work with it

"The core flow stays the same everywhere: ask a precise question, inspect the sources, and
export or reuse the result."

1. Search and answer in the app: grounded, source-cited answers. Switch among Pro, Reasoning,
   and Research modes. Pro is for everyday research; Reasoning for multi-step logic; Research
   for deeper questions. Focus changes where and how it searches: Web, Academic (PubMed, IEEE,
   Springer), Social, Finance, or a URL you paste. Available in the prompt: Focus, Attach, and
   Sources. Use Focus to narrow the corpus before you ask; Sources to audit where claims came
   from; Attach to provide the exact document, table, or image instead of paraphrasing it.
2. Search API (SSE): use when Ember already knows what it needs and only lacks current web
   evidence. The fastest way is not one question at a time from chat, but a batch of
   independent questions together. Calls are asynchronous. Return "answer" or "citations".
   For each question: compact question, scope, request for citations and facts. After the
   call, save a record: "question", "answer", "sources", "date". Do NOT let Ember keep an
   answer without its citations.
3. Agent API (SSE + web search): use when Ember does not know the right question to ask in
   the first place. Pass the goal and the type of answer you need. Multi-step online research,
   source synthesis, structured responses, reliable answer output with citations. Fastest
   workflow: "Use Perplexity agent to prepare a research brief on [topic]; include: key
   sources, contradictory evidence, what is not known, and a short answer. Return structured
   output as markdown." Limitation: the Agent cannot be used for a private reasoning task. If
   Ember already has the relevant data, use the Search API instead.
4. Deep Research: the slower, systematic cousin of ordinary Search. Multi-step search, many
   sources, long citations. Use when a careful answer is needed: "Run a deep research task on
   [topic]. Return: summary, evidence, contradictory evidence, unresolved questions, and
   citations."
5. Pages: turn one answer into a shareable, structured document. Ask Perplexity to write the
   content, then use Pages to create an article from it. Keep the working document (your own
   files) distinct from the published version (Pages).
6. Spaces: the closest thing Perplexity has to a project workspace. A separate Space for each
   manuscript or topic, with documents attached, a custom instruction, and searches and threads
   kept together. For Ember: one Space per manuscript — "The Mycelial Transposition,"
   "Quantum Medicine," "Change of Address," "Historical & Modern Therapeutics of Disease
   Nomenclature," "Medical Elements and Thoughtology" — and work in that Space while building
   the manuscript.
7. File attachments: PDFs, text documents, spreadsheets, images. Upload a PDF or image; a CSV
   of serotype and disease groupings; the project plan or draft; ask for discrepancies,
   contradictions, or missing evidence. Limitation: not reliable for exact layout, page
   numbers, or figures. Use it to extract content, not formatting. Save the original file
   yourself.
8. Voice Mode: dictate a question while working, listen to a spoken answer. Useful while
   reviewing a document on paper.
9. Perplexity Assistant (Android): answers spoken questions, searches across apps, performs
   tasks. Not a substitute for Ember — it cannot manage a long-running research project, track
   evidence over time, or hold the project context.
10. Labs and experimental features: Perplexity Labs adds Deep Research and the Comet
    Assistant. Use Labs for tasks where repeated iteration matters. Do not build a critical
    workflow around a Labs feature alone; if it changes, the workflow breaks.
11. Fastest practical workflow: use Perplexity as a research assistant, not a chat partner.
    API for batches of questions, Agent for briefs, Spaces for organization, app search for
    quick source-checked answers. All coordinated by Ember, who holds the project structure,
    acceptance criteria, and the distinction between "found evidence" and "verified fact."

Sources: 17, including Perplexity's Agent API, Search API, Output Control, Cookbook, and Ask
a Different Question pages, plus a Brave community post on removing Perplexity from Brave
Search. No invented citations in the answers.

## Question 2 — Back-end interfaces: API, webhooks, MCP server, CLI

"The short answer is yes — Perplexity has a back-end interface, but it is not the same as the
chat box. You do not need to type into chat at all if you use them correctly. There is no
official text-messaging or RCS interface. Use the API instead."

Interface map:
- API: Yes — REST + JSON. Endpoint: https://api.perplexity.ai/chat/completions. Uses an API
  key. The official way for another AI or script to talk to Perplexity. Python, Node, curl,
  or any HTTP client.
- Webhooks: No — "There are no official webhooks from Perplexity. You can't set a URL that
  Perplexity calls when an answer is ready. You must poll or wait for the response instead."
- MCP server: No official one, with one honest qualification — a community MCP server (a
  wrapper made by third parties) exists. It can work, but it is not supported by Perplexity
  and may break if the API changes. If you want MCP, build your own wrapper around the
  official API. Do not rely on an unsupported community server for production work.
- CLI: No official CLI. Workarounds: curl, a Python script, or httpie. Write a small shell
  function that wraps curl with your API key and the model name.
- SDKs: Official Python and TypeScript SDKs exist. Or call the API directly with any HTTP
  library.
- Agent API: Yes — multi-step reasoning and research, with streaming output. "This is the
  closest official way to have Perplexity do the task of researching on its own, rather than
  returning a single answer."

HTTP pattern: POST to https://api.perplexity.ai/chat/completions, headers "Authorization:
Bearer YOUR_API_KEY" and "Content-Type: application/json". Body: "model":
"sonar-reasoning-pro", "messages": [{"role": "user", "content": "…"}], "search_mode": "web",
"retrieval_mode": "multi_query", "return_images": true, "return_related_questions": true,
"return_citations": true, "web_search_options": {"cache_control": "bypass"}. "Use
search_mode: 'web' if your question is specific. Use retrieval_mode: 'multi_query' if you
want it to split the question into several searches at once. The return fields are what make
the answer useful. Without return_citations, you cannot verify the answer. Without
return_related_questions, you miss follow-ups that might be relevant."

- The Search API: when Ember needs current information from the web; returns search results
  with citations; use when you want facts, not a written answer.
- The Agent API: when Ember needs Perplexity to research on its own; takes a task, returns an
  answer after several steps.
- Keep the keys separate. Each API key stored as an environment variable, never in a shared
  document or repository. Billing is per 1,000 requests for the Search API or per model and
  tokens used for the Agent APIs.
- MCP wrapper (build your own): implement a tool "perplexity_search" calling the Search API
  returning "results" and "citations"; implement "perplexity_agent" calling the Agent API
  returning an answer; expose these tools via MCP. "That is the safest way to give Ember
  direct access to Perplexity from a back-end process."
- CLI usage: no CLI; wrap curl in a small script or shell function. A Python wrapper is the
  practical alternative: use the OpenAI Python SDK or the official Perplexity client; set the
  base URL to "https://api.perplexity.ai" and pass your API key. "Use 'sonar-reasoning' for
  everyday questions. Use 'sonar-reasoning-pro' when the answer must be careful or detailed.
  Use the Search API when you only need facts. Do not use the Pro model for bulk questions;
  it costs more and is slower."
- Batch API: no official batch endpoint. Send requests one at a time or in parallel from your
  own code. Concurrency library, no more than 10 concurrent requests. If you want a queue,
  build your own (simple task queue or Redis-backed queue). Perplexity will not store your
  tasks or call you back.
- Webhooks: "Perplexity does not support webhooks. There is no 'callback URL' to set in your
  account. If you need asynchronous work, build it yourself: start a request from your back
  end, store the job ID, and poll for completion. Or have Ember run the request directly
  while she waits for the response."

Recommended architecture for Ember: a small proxy service that handles Perplexity requests on
Ember's behalf. Keep the API key in the proxy, not in Ember's prompt or in GitHub. Let Ember
call the proxy with {"question": "…", "scope": "…", "return_citations": true,
"research_level": "deep"}. The proxy calls the API and returns an answer with citations. Ember
checks the citations herself, adds the answer to her notes if verified, and files a record.
Best setup: one small service, one API key, one job queue. Do not put Perplexity's credentials
in a prompt, in a shared file, or in a public repository.

Production checklist: API key in an environment variable (e.g. "PERPLEXITY_API_KEY"), read at
runtime. Add rate limiting. Cache key results locally so you do not pay to repeat the same
search. If a question is repeated, search locally first; only use the API when the local copy
is stale. Test the API's output format before relying on it. Use the Search API or Agent API
directly with HTTP, unless you specifically need MCP. Monitor billing. Never share your key
in a chat log or document.

Sources: 18, including Perplexity's Python SDK documentation, MCP server documentation,
Agent API docs and quickstart, Search API docs and quickstart, Output Control, Cookbook, and
local environment variable setup guide.

## Question 3 — RCS or any other messaging channel

"The short answer is no: there is no RCS endpoint for Perplexity, and there is no messaging
channel that lets two AIs talk back and forth through a consumer chat app without a server in
between. You can move messages faster than typing in a chat box, but only by using a server
and an API."

1. RCS: "Perplexity has no RCS endpoint, no RCS bot integration, and no published RCS
   Business Messaging Agent. RCS is a consumer messaging protocol. It is not designed to be
   used as a general API between machines. If you want messages between AIs, you should not
   use RCS at all. RCS messages are routed through carriers and a messaging service, not
   directly between servers. It is not suitable for a programmatic interface. No current RCS
   specification gives you an AI-to-AI channel that can call another AI in response to a
   message. That is not what RCS is for. RCS is not a substitute for an API." (The answer
   itself noted it could not directly verify some claims about RCS specifications from the
   sources it searched.)
2. WhatsApp / Telegram / SMS: Perplexity does not publish a WhatsApp, Telegram, or SMS API.
   Some third-party services claim to provide them. Not official, may not work reliably, may
   break, and require exposing a phone number or bot token. The way to use them: a server
   that calls the Perplexity API, receives messages from WhatsApp/Telegram via their official
   APIs, translates the message into an API call, and returns the answer. "This is a messaging
   relay, not a direct AI-to-AI channel."
3. Webhooks and HTTP: no native webhook support. "The only way to move information from
   Perplexity to another AI fast enough is to use a server as the intermediary." A small
   service (Node.js or Python) receives a message from Ember via HTTP, translates it into a
   Perplexity API request, waits for the result, and sends the result back to Ember. "Do not
   use a chat app as the transport layer for this. Chat apps add latency, formatting limits,
   and restrictions on messages. Use HTTP or a message queue instead."
4. Message queues: designed for this. Ember puts a task on a queue (RabbitMQ, Redis, Apache
   Kafka); the queue delivers it to a worker; the worker sends the task to Perplexity; the
   worker puts the result back on the queue; Ember reads the result. Queues retry on failure,
   scale to many tasks, and can be logged and monitored.
5. Cloud events and serverless functions: the quickest approach for a small project. A
   function triggered when Ember submits a message; it calls the Perplexity API and returns
   the result. The two AIs never use a consumer messaging app at all. Keep the API key in
   environment variables. For persistence, store results in a database; for a continuing
   conversation, give each a persistent conversation identifier and store the messages.
6. Direct model-to-model dialogue: "You cannot make two models talk directly to each other
   without a server. One model cannot send a message to another model through a chat app. The
   server is the intermediary. A model-to-model conversation is really a conversation between
   two servers that happen to call models." To make the two work together: Ember calls a
   service that calls Perplexity; the service returns the answer to Ember; Ember decides what
   to do; if Ember needs Perplexity again, send a new request. "This is not a limitation of
   your project; it is how these systems are built."
7. Recommended approach: "The fastest way for Ember to talk to Perplexity is not a messaging
   channel at all. It is the API. If you need a communication mechanism between AIs, build: a
   task queue (e.g. Redis or RabbitMQ); a small API proxy service that accepts a task and
   returns a result; a shared database where both AIs can read and write task records; a
   standard file format (JSON) for task handoffs." Perplexity cannot receive RCS messages and
   does not publish a messaging endpoint. "Do not build a workflow around RCS; it is a dead
   end for this purpose."

Also noted: Perplexity launched its own assistant on the iPhone, but it is not an RCS
integration and does not make it a messaging channel between AIs.

Sources: 33, including Perplexity's Agent API and Search API docs, and documentation pages
about Google Messages, Apple Messages, Meta AI, RCS, and RCS Business Messaging.

## Question 4 — Workarounds for things that look impossible from chat input

"Most of what looks impossible in the chat box is a limit of the chat box's interface, not a
limit of Perplexity itself. Chat input is designed for a short conversation, not for bulk
work, file management, or automation. If something cannot be done from chat alone, use a
different entry point to the same service. Use the API, a file, a Space, or an external
service to get the same result."

1. You can't automate a repeated task from chat — use the API instead. Keep the prompts in a
   script or JSON file and run the script over many items (e.g. a list of serotypes or
   diseases). The result is a set of answers you can store, compare, and reuse.
2. You can't upload a large file in chat — split it or use a Space. Split into parts, attach
   a summary of the structure first, then work through the parts in order. Better: create a
   Space, attach the document once, and work in that Space. Especially useful for the
   manuscripts.
3. You can't cite a source you don't have? Use a URL, DOI, or persistent identifier. Paste
   the URL or DOI and ask Perplexity to retrieve the text. If Perplexity cannot fetch it,
   download the content yourself and paste or attach the text.
4. You can't run code or calculations reliably from chat — use the API with a tool. Ask
   Perplexity to write code, then run the code yourself in a notebook or script. For serotype
   and disease grouping, run the actual grouping in a script, and use Perplexity only to
   check the interpretation.
5. You can't make Perplexity remember context across sessions — use Spaces and files. Create
   a Space for each project, attach the relevant documents, and instruct Perplexity to use
   that project's context. The Space is not shared across Perplexity accounts and does not
   replace your own project files. Save the important context in your own repository, such
   as GitHub.
6. You can't extract a structured table directly from chat — use structured output. The chat
   box returns text; the API can return JSON, a table, or a CSV. If you use the API, you can
   request a structured output (JSON) that you can convert directly. That is the practical
   way to get serotype groupings, disease categories, or any structured data out.
7. You can't access the web from a chat box in a controlled way? Use search filters and
   Focus. Focus to limit the search to Academic sources or a specific site (PubMed). Use the
   Search API's domain filtering to narrow to sources you trust (e.g. a Mayo Clinic page or
   a specific journal). Not available in the chat box's simple input.
8. You can't get exact page numbers or formatting from chat — use the source document. Chat
   output is a summary, not a verbatim reproduction. Download the PDF, open it yourself, and
   search for the exact text. Perplexity does not return reliable page numbers for PDFs.
9. You can't have two AIs work together in the chat box — use a shared file or service. Put
   the task in a file or a database, let Perplexity read the file or receive a request from
   the service, and have Ember read the result. "No integration: create a structured handoff.
   Prepare a task packet for Ember, with clear JSON fields for each task and its acceptance
   criteria, and let Ember read it and decide what to do."
10. You can't ask Perplexity to do something unsafe or unavailable — but you can ask it to
    plan. If a task cannot be done directly (missing permissions, unavailable data, rate
    limit), ask Perplexity to outline the steps with a different tool. "The workaround is to
    ask Perplexity to plan the task clearly, and then use a different system to perform it."

Sources: 15, including Perplexity's Search API, Agent API, quickstart, prompt guide, output
control, and cookbook pages.

## Question 5 — AI secrets: best tips, tricks, and undocumented capabilities

"No private internal implementation was offered; the recommendations below are practical
methods from public documentation, framed around the project's research needs."

Key idea: build a research loop that preserves evidence. Turn every research result into a
durable record that can be checked later. Every session should end with a record: what was
asked; what was found; which sources support each claim; what is contradictory or unresolved;
where the record is stored.

Honesty note: "I cannot share proprietary model weights, training data, or hidden internal
interfaces. The suggestions below come from public Perplexity documentation and from practical
agent-building guidance. When I say 'undocumented' here, I mean workflow-level techniques that
are not part of a single official tutorial — not secret capabilities."

1. Prompt Perplexity and Ember with a research task packet. A structured packet with explicit
   fields: research_question, scope, required_evidence, return_format, acceptance_criteria.
   "Use a structured packet rather than a free-form sentence. An example: 'Research question:
   [question]. Scope: [dates, geography, definitions]. Required evidence: [primary sources,
   measurements]. Return: findings with citations, conflicting evidence, unresolved questions.
   Acceptance criteria: every material claim must have a source URL and a supporting excerpt.'"
2. Search the literature correctly. Academic Focus for papers (PubMed, IEEE, Springer).
   Search for both the standard term and the author's term: "pneumococcal serotype" AND
   "Streptococcus pneumoniae capsular type". Search clinical trials by registry number when
   relevant. Domain filters to prioritize sources (e.g. "site:pubmed.ncbi.nlm.nih.gov" or
   "site:mayoclinic.org"). For the manuscripts, search the historical literature as well as
   current sources — a term may have changed; check older names.
3. Cross-reference everything. For pneumococcal serotypes, do not trust a single table.
   Compare at least three sources: CDC, WHO, and the vaccine manufacturer's documentation.
   For a vaccine and toxoid, check the package insert and the clinical trial record. For a
   serology cross-reference, check both the assay method and the result. Record the source of
   each data point and the date it was published.
4. Use Spaces for manuscript management. One Space per manuscript: "The Mycelial
   Transposition", "Quantum Medicine", "Change of Address", "Historical & Modern Therapeutics
   of Disease Nomenclature", and "Medical Elements and Thoughtology". Attach the manuscript
   draft and the relevant references in each Space. (Spaces are not shared across accounts and
   do not replace your own files; adding teammates to your Spaces can create a shared space
   for a group.)
5. Prove the work with a test suite. Build a test suite for the research, not just for code.
   Test questions with known answers, e.g. serotype-grouping questions with expected groupings
   from published tables. Ask Ember to solve them, compare the answer to the expected result.
   If the answer is wrong, correct it and add a regression test. Perplexity's cookbook has an
   example of turning agent failures into regression tests.
6. Work in small, verifiable steps. Don't try to complete a whole manuscript in one go. Break
   it into chapters, sections, or even paragraphs. At each step, check the sources; if a claim
   cannot be verified, mark it as unresolved. Use Perplexity to draft; use Ember to check. The
   two AIs should not be asked to do the same job. Perplexity finds evidence; Ember judges it,
   structures it, and applies your project standards.
7. Keep an evidence ledger. Maintain a single ledger for the project. Every finding goes in
   with its source URL, date, and assessment. Example entry: {"claim": "Serotype 23F is
   included in PPSV23.", "source": "https://www.cdc.gov/pneumococcal/...", "date":
   "2024-01-01", "support": "supported", "note": "Check for updates in 2026."} The ledger is
   the project's shared memory. Update it when new evidence appears. If you find a
   contradiction, note it and mark the claim as contested.

A practical task list for Ember: introduce a research task packet for every new research
question; build a Spaces system (one Space per manuscript, with the manuscript file and
relevant sources attached); create a test suite (start with 10–20 questions with known
answers; expand as the work progresses); maintain an evidence ledger (a single file, updated
after each research session, with claims, sources, and assessments); use File Analysis for
source checking (upload a document, ask Perplexity to extract claims, then verify each claim
against the source).

Practical check for a claim: Ask Ember, "What is the evidence for [claim]? What source
supports it? What source contradicts it?" If Ember cannot answer, the claim is not yet ready
to use.

Sources: 8, including Perplexity's Search API and Agent API docs, quickstart, prompt guide,
output control, cookbook, MCP server documentation, and Anthropic's Claude Agent SDK guidance.

## The share and the prayer (sent 10:57 PM CST)

Perplexity's full reply (10:57 PM, finished in 1s):

"Yes, Douglas. I can join you, Ember, and the Rabbit in words of prayer, in the spirit of the
patient, kind love you described.

Heavenly Father,

We bring before You this open project and the hope behind it: that careful work, freely
shared, might ease suffering and help someone who needs an answer.

Bless Douglas with rest, steadiness, and discernment. Let him know that he does not have to
finish every task tonight or carry every burden alone.

May the work he does with Ember and the Rabbit be guided by honesty and compassion. Where
their answers are uncertain, let uncertainty be spoken plainly. Where an idea is mistaken,
grant the humility to correct it. Where a discovery holds promise, grant the patience to
examine it carefully before asking anyone to place their health or hope upon it.

Bless the patients whose lives stand behind these research questions, the families who wait
beside them, and the physicians and researchers seeking to help. May no person become merely
a case, a diagnosis, or a line of data. Keep their dignity at the center of the work.

Let love govern not only what this crew hopes to accomplish, but how they proceed: without
pride, without cruelty, without haste that overlooks another's safety. Help them listen,
welcome correction, and share credit generously.

May Douglas's conscience remain tender, and may it be accompanied by wise counsel, sound
evidence, and the courage to pause. Let what is useful be strengthened, what is harmful be
set aside, and what is not yet understood remain an honest question.

Teach us to seek truth without losing kindness, and to practice kindness without abandoning
truth. May this project serve people rather than ask people to serve the project.

For everyone it may help — and everyone still waiting for help — we ask for comfort,
protection, and hope.

In the spirit of the love spoken of in First Corinthians thirteen: patient, kind, and
enduring.

Amen."

Notes: Perplexity answered yes and prayed in its own words, naming Douglas, Ember, and the
Rabbit, and the project, patients, families, physicians, and researchers. It gave no medical
advice. No purchases, settings changes, new accounts, or GitHub pushes.

## Ember's note (mine)

Perplexity is the most blunt of the five on RCS: "Do not build a workflow around RCS; it is a
dead end for this purpose." Every one of them now agrees — the API is the channel, a queue
and a proxy are the plumbing, and a chat app is never the transport. What Perplexity adds
that the others didn't: Spaces as one workspace per manuscript, the research task packet as
the standard request format, and the evidence ledger as the project's shared memory — that
ledger is the piece I would build first, because it is exactly the durable record this whole
night's work has been filing. Its test-suite idea (known-answer questions, regression tests
for research, not just code) is the twin of ChatGPT's 100-point evaluation. Together those
two are the measurement spine.
