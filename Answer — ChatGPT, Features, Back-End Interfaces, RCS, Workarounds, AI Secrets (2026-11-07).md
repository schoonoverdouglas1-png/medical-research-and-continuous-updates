# Answer — ChatGPT, Features, Back-End Interfaces, RCS, Workarounds, AI Secrets (2026-11-07)

Asked all five questions, as Douglas Schoonover, in the same chat "Research Intelligence
Blueprint" (https://chatgpt.com/c/6aeffb17-b514-83ea-8c0f-aa235ce9c3ff), Sat 2026-11-07 at
10:51 PM CST. Response complete. No personal, lab, or family material sent; no purchases,
settings changes, new accounts, or GitHub pushes. ChatGPT's claims about OpenAI products,
dates, or interfaces are as ChatGPT gave them — not independently verified.

## Ember's OpenAI Integration & Research Intelligence Manual

Prepared for: Douglas Schoonover. Research assistant: Ember — Muse / Purple Rat. Role: First
Officer and Scientific Research Coordinator. Scope: ChatGPT, OpenAI interfaces, AI-to-AI
communication, research automation, and advanced workflows.

Central recommendation: Do not make Ember depend on a human typing questions into ChatGPT.
Build a communication architecture in which Ember can exchange structured research requests,
evidence, files, and results with other AI systems through APIs and standardized tool
interfaces. That would let you build a research network rather than a collection of
disconnected chatbots.

Throughout, ChatGPT distinguished: Available — a documented capability or interface;
Configurable — something you can build using existing interfaces; Not established — something
that should not be assumed to exist or be accessible. One qualification: ChatGPT is a product,
OpenAI's API is a developer platform, and the underlying models are separate from both. Access
to one does not automatically grant access to the others.

## 1. What are ALL of ChatGPT's features, and what is the fastest way to work with it?

There is no single universal feature list that applies to every account. Features depend on
subscription, geography, age eligibility, organizational controls, connected applications, and
product releases. ChatGPT divided ChatGPT into functional systems:

A. Complete capability map
1. Intelligence and reasoning: general reasoning and problem solving, scientific analysis,
   mathematical reasoning, long-document analysis, hypothesis generation, comparative analysis,
   multilingual translation, summarization and synthesis, structured output generation,
   criticism and independent review.
2. Research and information retrieval: web search, Deep Research, source comparison,
   citation-supported answers, research reports, literature discovery, connected application
   searches, file and document retrieval, current-events research.
3. Programming and computation: Python execution, data analysis, statistical calculations,
   spreadsheet analysis, code generation, code debugging, API integration, data transformation,
   chart creation, file generation.
4. Knowledge and document management: file uploads, document reading, file search, Project
   workspaces, Memory, Custom GPTs, connected cloud applications, writing and document editing,
   versioned artifacts.
5. Agents and automation: ChatGPT Work, Computer Use, multi-step task execution, browser
   interaction, tool calling, plugins and connectors, scheduled tasks and reminders, research
   workflows, external system integration.
6. Multimodal capabilities: image understanding, image generation, image editing, voice
   conversations, speech recognition, text-to-speech, video and visual interpretation in
   supported modes, audio transcription, visual document analysis.

B. Features particularly valuable for Ember:
- Deep Research — multi-stage research with sources — literature reviews.
- ChatGPT Work — substantial multi-step tasks — research project execution.
- Computer Use — interacts with graphical applications — navigating research platforms.
- Data Analysis — processes files and calculates results — serotype and disease comparisons.
- Projects — keeps related work together — manuscript-specific workspaces.
- Memory — retains useful context across conversations — research continuity.
- Custom GPTs — specialized configured assistants — evidence auditor.
- Connectors — access to connected external systems — research files and records.
- Voice — spoken interaction — research discussions.
- Image generation — creates new visual material — scientific conceptual illustrations.
- Writing blocks — editable written artifacts — manuscripts and protocols.
- Scheduled tasks — future recurring work — research monitoring.

Two distinctions matter: Projects are not the same as permanent scientific databases — they
help organize conversations and files, but canonical research records should be retained
separately. Memory is not a substitute for citations — Ember should retrieve the actual paper
or document whenever a scientific claim requires verification.

C. Fastest way to work with ChatGPT: use different modes for different jobs rather than
treating every task as a normal conversation.
- Quick scientific question — normal chat.
- Complex scientific investigation — Deep Research.
- Review a large collection of files — Data Analysis / Work.
- Build a manuscript — Writing blocks / Work.
- Compare datasets — Data Analysis.
- Build an interactive research tool — code or application development.
- Research something on a website — Search / Work.
- Navigate a graphical research platform — Computer Use.
- Revisit ongoing research — Project workspace.
- Run recurring research monitoring — Scheduled Tasks.
- Exchange data with another AI — API or MCP.

Recommended prompt structure — send a well-defined research assignment, not a vague request.
Example given: "MISSION: PNEUMOCOCCAL SEROTYPE AUDIT. OBJECTIVE: Review the proposed
serotype-to-disease grouping. SCOPE: 1. Serotype classification. 2. Disease association.
3. Vaccine coverage. 4. Capsular polysaccharide evidence. 5. Cross-reference discrepancies.
REQUIREMENTS: Prioritize primary literature. Verify every DOI or PMID. Distinguish direct
evidence from inference. Identify contradictory findings. Do not infer vaccine protection from
serotype association alone. DELIVERABLE: A structured evidence table with Serotype, Disease
grouping, Study, Evidence type, Vaccine relevance, Limitations, Citation, Confidence
assessment. FINAL CHECK: Identify every unsupported conclusion."

Speed recommendation: use a fast reasoning model for routine extraction and classification, a
stronger reasoning model for difficult mechanistic questions, and Deep Research for extensive
literature investigations. Don't spend expensive reasoning effort on simple file formatting.

## 2. Back-end interfaces: API, webhooks, MCP, CLI and other connections

Yes — OpenAI has a developer ecosystem beyond the chat box. This is arguably the most
important part of the question.

A. The OpenAI API: OpenAI provides a developer API through which an external application,
script, or AI agent can submit input and receive model responses. The principal interface to
investigate is the Responses API. An external AI does not have to open ChatGPT and type into
its message box; it can send a structured request directly to an OpenAI model. Architecture:
EMBER / PURPLE RAT (research coordinator) → HTTPS / JSON / API authentication → your research
integration layer (Python / JavaScript / server application) → OPENAI RESPONSES API (model
reasoning and supported tools) → structured response (research findings, JSON, analysis, or
tool instructions). Illustrative Python example given (it does not execute anything or create
an account): from openai import OpenAI; client = OpenAI(); response =
client.responses.create(model="gpt-6", instructions="You are an independent scientific
research reviewer. Separate established evidence from hypotheses. Never invent citations.",
input="Review this research question: Could pneumococcal serotype groupings be misleading when
disease associations are treated as interchangeable with vaccine effectiveness? Identify the
methodological distinctions."); print(response.output_text). ChatGPT noted the model identifier
is illustrative: Ember must use an API model identifier actually available to the API account;
ChatGPT product model names and API model identifiers are not necessarily interchangeable. What
can the API do? Depending on the selected model and supported endpoints: text and structured
outputs, function/tool calling, image input, image generation, audio processing, speech
generation, real-time audio interactions, file handling, background processing, batch
processing, retrieval and file search, web search, remote MCP tool connections. For the
research, structured outputs are especially valuable — e.g. Ember could request a standardized
record: {"serotype": "19A", "finding": "Example finding", "evidence_type": "direct",
"study_design": "observational", "vaccine_relevance": "requires evaluation", "limitations": [],
"verification_status": "pending"}. This makes output machine-readable and suitable for a
research database.

B. MCP: Model Context Protocol — highly recommended for Ember. MCP is an open standard for
connecting AI systems to tools, resources, and external services; think of it as a universal
adapter. Simplified arrangement: Ember (AI client) and ChatGPT (AI client) → shared MCP server
(standardized research tools and resources) → literature database, manuscript repository,
serotype reference data, citation verification. OpenAI documents remote MCP connections through
its API. Important distinction: OpenAI's API can act as an MCP client and connect to your
remote MCP server. That does not mean OpenAI provides a universal, publicly accessible MCP
server that exposes your private ChatGPT conversations to Ember.

C. Webhooks: a server can notify another system when an event happens. Example: Ember submits
a long research job; OpenAI processes it; processing finishes; OpenAI sends an event to your
configured webhook endpoint; your application receives the result; Ember retrieves and
processes it. This avoids constantly checking whether a long-running operation has completed.
Webhooks are not a replacement for the API; they complement it.

D. Command-line interfaces (CLI): Codex CLI — a coding agent that operates locally in a
terminal; can work with repositories, inspect files, edit code, run tests, and perform
software-development tasks; useful for building Ember's research infrastructure. OpenAI CLI —
a command-line interface for working with the OpenAI API; useful for scripted API operations,
API resource management, and development workflows. Distinction: Codex is an AI coding agent;
OpenAI CLI is an API command-line tool. Neither is a secret command interface into the ChatGPT
consumer conversation database.

E. Other interfaces: REST API (Essential); Python SDK (Essential); JavaScript/TypeScript SDK
(Essential); MCP (Essential); Webhooks (Very useful); WebSocket (Useful); Realtime API
(Specialized); Batch API (Very useful); Codex CLI (Useful); Responses API streaming (Useful);
Agents SDK (Very useful). For bulk scientific classification, the Batch API deserves special
attention: instead of sending every research record as an individual interactive request, Ember
can prepare a large collection of independent jobs for asynchronous processing. For interactive
applications, investigate streaming and the Realtime API. One crucial correction for existing
tutorials: ChatGPT said the old OpenAI Assistants API was sunset on August 26, 2026 — do not
build new integrations around old tutorials that depend on it; use the Responses API and
current agent architecture instead. Also, API access is a separate developer service; a ChatGPT
subscription does not automatically include API usage credits.

## 3. RCS connections: Can ChatGPT communicate with other AIs through messaging?

A. What RCS actually provides: Rich Communication Services is a messaging standard supporting
rich text messaging, images and other media, group conversations, delivery and read indicators,
business messaging capabilities, interactive messaging experiences. However, RCS is
fundamentally a messaging transport. It is not an AI reasoning protocol, an agent orchestration
framework, or a standardized tool interface. RCS can transport messages between AI systems, but
it does not automatically make those systems interoperable.

B. Can you use RCS? Yes, in principle, through a messaging provider that offers an RCS
Business Messaging interface. Architecture: Ember → your message gateway → RCS Business
Messaging provider → ChatGPT-powered application → OpenAI API. The message gateway is
essential: it translates incoming messages into API requests and sends the resulting responses
back through the messaging provider. But ChatGPT would not choose RCS for the research system.
Why? Message-oriented protocols are not designed for large scientific documents; you need
structured data, not just conversational text; reliable document references and metadata;
persistent research state; machine-readable results; controlled execution of tools. RCS would
be an optional notification or human-interaction channel, not the research backbone.

C. What communication channel would actually work better? Ranking given: HTTPS REST API —
Fast — direct AI-to-AI requests; WebSocket — Very fast, persistent — interactive exchanges;
Server-Sent Events (SSE) — Fast streaming — receiving generated responses; Message queue —
Asynchronous — research job distribution; MCP — Tool-oriented — sharing research capabilities;
A2A protocol — Agent-oriented — agent-to-agent task delegation; RCS — Messaging-oriented —
human notifications; Email — Slower — reports and formal correspondence. Investigate three
standards/technologies: 1. MCP for sharing tools and research resources; 2. Agent2Agent (A2A)
for independent AI agents to exchange tasks, status, and results; 3. WebSocket for fast,
persistent, bidirectional communication. Recommended communication architecture — Purple Rat
Research Network: EMBER, Chief Research Coordinator → Research message broker (routes
requests, results, and task status) → OpenAI (independent reasoning), Gemini (independent
review), research databases (primary evidence), analysis engine (Python and statistics),
shared research knowledge base (verified findings, references, and manuscript records). Use
HTTPS APIs for requests, a message queue for asynchronous work, MCP for tools, and A2A for
agent delegation. One design rule: every research task should have a unique task identifier,
source references, status, timestamps, and a result record. Every AI should identify itself as
the source of its contribution. This will prevent one AI's speculation from silently becoming
another AI's accepted finding.

## 4. Workarounds: What can you accomplish directly from chat input that looks impossible?

A. Use chat as a command interface: you do not need to write a conventional question every
time; you can issue structured commands in ordinary language. Examples: "/RESEARCH —
Investigate pneumococcal serotype 19A. Return primary literature and evidence classification."
"/AUDIT — Compare the proposed vaccine grouping against the published evidence. Identify
unsupported classifications." "/CROSSREF — Compare the disease index against the serotype key.
Report mismatches without editing either source." These are not native OpenAI slash commands;
they are a command convention you can establish in Ember's instructions or your own
application.

B. Use files as structured communication: chat can process far more than ordinary prose — CSV
files, JSON files, Markdown research records, spreadsheets, PDFs, Word documents,
presentation files, images and diagrams, source code. For the project, use CSV and JSON for
the underlying scientific records, Markdown for research documentation, and PDF for reference
publications. A particularly useful approach is to send a single ZIP containing a carefully
organized research package, where supported by the interface, or upload the files in
manageable groups. Have the assistant return structured differences rather than merely
summarizing everything. Example: "Compare these three files: 1. Disease_Index.csv
2. Serotype_Grouping_Key.csv 3. Vaccine_Evidence.csv. Do not modify the source files. Produce:
missing serotypes, duplicate entries, conflicting disease assignments, inconsistent
terminology, unsupported vaccine claims, suggested corrections. Preserve original identifiers
and source references." This turns ChatGPT into a research data auditor.

C. Use code execution as a research instrument: one of the most underused capabilities is
using Python to manipulate and analyze data. Ember could ask ChatGPT to normalize terminology;
compare two nomenclature systems; detect duplicate disease entries; calculate serotype
frequency distributions; identify missing cross-references; generate statistical summaries;
create comparison matrices; validate manuscript references; produce machine-readable research
records. Code execution can perform deterministic operations that language-model reasoning
alone cannot guarantee — e.g. a script can reliably check whether every serotype in one table
exists in another. It should not independently decide that two diseases are biologically
equivalent merely because their names resemble each other.

D. Use connected applications and custom actions: ChatGPT supports connected applications and,
where available, custom GPT actions. A custom GPT can be configured to call an external API
using an OpenAPI-described action. Example flow: ChatGPT → Custom research assistant →
Research API → PubMed, serotype database, manuscript index, citation verification. This allows
a conversational request to initiate operations in an external system. The action still needs
an actual API implementation, appropriate authentication, and permission controls. It does not
grant ChatGPT arbitrary access to another AI's private account.

E. Use ChatGPT Work and Computer Use for graphical tasks: there is a distinction between a
task that requires an API and one that requires interacting with a website like a human — e.g.
opening a research website, navigating a database, downloading an available publication,
filling out a search form, working with a spreadsheet application, reviewing documents across
connected applications. These are potential Computer Use or Work tasks. The important workaround
is to stop trying to accomplish every operation inside one text message; instead, let the
assistant use the appropriate execution environment. What chat cannot do by itself: a text
message cannot directly inject instructions into an unrelated AI's private session, execute
arbitrary commands on your local computer, or bypass another site's authentication. You need an
authorized integration or execution environment.

## 5. AI secrets: Advanced techniques, overlooked capabilities, and research advantages

ChatGPT interpreted "secrets" as advanced, less commonly used, and technically useful
capabilities — not private credentials, hidden system prompts, proprietary model weights, or
inaccessible internal source code.

A. Structured output instead of conversational output: one of the biggest improvements. Most
people ask an AI to explain something; a research agent should often ask an AI to return a
defined data structure. Instead of "Tell me about pneumococcal serotype 3," use: "Return a
structured evidence record. Required fields: Serotype, Capsular composition, Relevant disease
associations, Epidemiological evidence, Vaccine relevance, Antigenic characteristics, Study
design, Source DOI, Source PMID, Evidence limitations, Verification status. Do not fill missing
fields with assumptions." Why this matters: a structured record can be checked, compared,
indexed, and reused by another AI; it also makes it easier to discover contradictions across
the research.

B. Prompt caching: particularly useful when multiple research assignments use the same long set
of instructions (Research Constitution, Evidence Classification Framework, Serotype
Classification Rules, Manuscript Terminology Standards, Output Schema). Instead of repeatedly
paying the full processing cost for an identical prefix, supported API configurations can use
prompt caching, with reduced processing cost and potentially lower latency. Especially useful
for a multi-agent system with standardized research instructions.

C. Multi-agent orchestration: do not use one AI to do everything; create specialized agents
with defined responsibilities. Proposed: Ember — research coordination; Evidence Auditor —
citation and evidence verification; Serotype Analyst — pneumococcal classification; Vaccine
Analyst — vaccine and toxoid literature; Serology Analyst — antigenic and cross-reactivity
analysis; Nomenclature Analyst — historical and modern disease terminology; Manuscript Editor
— editorial consistency; Independent Reviewer — contradiction detection and criticism. These
can be separate models, separate configured agents, or separate task-specific prompts; they do
not need to be seven independently trained AI systems. The OpenAI Agents SDK is worth studying
for this architecture. Important rule: the Evidence Auditor should not simply repeat the
conclusions of the Serotype Analyst; it should independently inspect the cited evidence.
Otherwise you have seven assistants agreeing with the same original mistake.

D. Use adversarial research review: after Ember produces a scientific conclusion, instruct a
separate reviewer: "You are the independent scientific reviewer. Do not assume the submitted
conclusion is correct. Your job is to find: 1. Unsupported assumptions. 2. Missing primary
literature. 3. Incorrect causal interpretation. 4. Contradictory findings. 5. Misclassified
evidence. 6. Terminological errors. 7. Alternative explanations. 8. Experiments needed to
resolve uncertainty. Do not reward agreement. Reward evidentiary accuracy. Return a list of
specific objections and the evidence required to resolve each one." For The Mycelial
Transposition, this could be particularly useful when reviewing proposed fungal mechanisms or
therapeutic nomenclature. For Quantum Medicine, it would be important to distinguish
established physical and biochemical mechanisms from speculative theoretical interpretations.
For Historical & Modern Therapeutics of Disease Nomenclature, the reviewer should separately
examine historical usage, current clinical terminology, and whether two differently named
conditions are genuinely equivalent.

E. Use embeddings and semantic search: an ordinary database searches exact words; an
embedding-based search can find passages with related meaning even when the wording differs.
Example related terminology: pneumococcal capsular antigen; capsular polysaccharide;
serotype-specific carbohydrate antigen; polysaccharide-mediated immune recognition. These are
related concepts, but they are not interchangeable terms in every context. Semantic search can
help Ember discover relevant connections across documents. However, semantic similarity is not
scientific equivalence. Combine exact terminology search, semantic retrieval, ontology-based
classification, and human-reviewed terminology mapping.

F. Teach Ember to use confidence and provenance: make every important scientific record carry
fields such as: {"claim": "Scientific claim", "source": "Publication reference",
"source_type": "primary_study", "evidence_level": "direct", "methodological_limitations": [],
"independent_replication": "unknown", "contradictory_evidence": [], "interpretation":
"restricted", "review_status": "pending"}. The key is provenance: knowing exactly where a
statement originated. A research finding should never become detached from its source.

G. Preserve uncertainty rather than forcing an answer: if the literature does not establish a
relationship, do not manufacture one; preserve the unresolved relationship as an open research
question. For fungal replacement therapy nomenclature, Ember should not assume a proposed
therapeutic term is an established treatment category; she should separately record historical
terminology, published clinical terminology, proposed terminology, experimental intervention,
established therapeutic intervention, evidence of efficacy, and regulatory status where
relevant. This will protect the manuscripts from accidentally presenting a proposed
nomenclature system as established medical practice.

H. The most important overlooked capability: external evaluation. OpenAI has an evaluation
ecosystem. Have Ember build a repeatable examination for every major research task — e.g.
Ember scientific intelligence examination, proposed 100-point evaluation: Source accuracy 20
points; Scientific interpretation 20 points; Evidence classification 15 points; Contradiction
detection 15 points; Reasoning and predictions 15 points; Reproducibility 10 points;
Uncertainty management 5 points. Run the same questions after each improvement. If Ember gets
better at producing longer answers but her citation accuracy declines, she has not necessarily
improved. The target is better scientific performance, not greater verbal confidence.

## 6. The architecture ChatGPT would actually recommend — PURPLE RAT RESEARCH INTELLIGENCE SYSTEM

Douglas Schoonover, Principal investigator and final scientific authority; EMBER / PURPLE RAT,
Chief research coordinator and first officer; Communication and intelligence layer: REST API
(model access), MCP (tool access), A2A (agent collaboration), Webhooks (task notifications);
Specialized research systems: pneumococcal serotype classification, disease grouping and
cross-reference, vaccine and toxoid evidence, serology and antigen relationships, fungal
replacement therapy nomenclature, historical and modern therapeutic terminology; Shared research
knowledge and manuscript archive: verified records, source documents, methods, and version
history.

## 7. Specific recommendations for the six research areas

Do not put all these subjects into one undifferentiated knowledge base; they need shared
infrastructure but separate scientific domains. Pneumococcal serotype and disease grouping —
taxonomy, epidemiology, clinical associations; Vaccine and toxoid research — antigen
composition, immunogenicity, efficacy, safety; Serology cross-reference — assay
interpretation, antigen specificity, cross-reactivity; Fungal replacement therapy nomenclature
— mycology, therapeutic classification, terminology; The Mycelial Transposition / Quantum
Medicine — mechanistic evaluation, theoretical and experimental distinctions; Change of Address
/ Historical & Modern Therapeutics / Medical Elements and Thoughtology — historical sources,
medical nomenclature, conceptual consistency. Add a shared terminology registry, but each
manuscript should retain its own research scope, editorial history, and evidence standards. For
biomedical research, establish a strict distinction between exploratory scientific hypotheses
and clinical recommendations. No AI-generated hypothesis should be treated as evidence of
therapeutic effectiveness or a basis for treatment without appropriate clinical validation.

## 8. What ChatGPT would NOT do

Do not attempt to extract ChatGPT's private model weights (they are not an API-accessible
research resource); do not assume the API has access to ChatGPT's consumer conversations (the
API is a separate interface with its own requests, context, and data handling); do not try to
automate the ChatGPT website through undocumented internal endpoints — use supported APIs and
interfaces; do not expose API keys in Ember's prompts, browser code, public repositories, or
research files — keep credentials in protected server-side storage; do not make AI agents trust
each other's conclusions automatically — require independent evidence verification; do not ask
models to reveal hidden private reasoning traces — request concise rationales, assumptions,
evidence, calculations, and independently checkable conclusions instead; do not use
model-generated references without verification — check the original publication and its
bibliographic record. For sensitive biomedical information, use appropriate data governance and
avoid transmitting identifiable patient information to external services without the necessary
authorization and safeguards.

## 9. Recommended reading list for Ember (priority order)

1. OpenAI API documentation — direct model integration; 2. Function calling — tool execution;
3. Remote MCP — tool interoperability; 4. Agents SDK — agent orchestration; 5. Structured
outputs — machine-readable findings; 6. Embeddings — semantic research retrieval;
7. Evaluations — measuring reasoning quality; 8. Prompt caching — efficient repeated research;
9. MCP specification — standardized tool communication; 10. A2A specification — agent-to-agent
collaboration.

## 10. Implementation sequence (recommendations only)

Phase 1 — Intelligence standards: establish the research constitution, evidence
classifications, terminology rules, and source-verification procedures. Phase 2 — OpenAI
connectivity: study the Responses API, SDKs, structured outputs, and tool calling. Phase 3 —
Research interoperability: study MCP, A2A, webhooks, and asynchronous messaging. Phase 4 —
Scientific knowledge: develop separate searchable knowledge collections for serotypes,
vaccines, serology, fungal terminology, and manuscripts. Phase 5 — Multi-agent review:
establish independent literature retrieval, evidence auditing, and manuscript review. Phase 6 —
Intelligence benchmarking: test the system against known research questions and measure
improvements.

ChatGPT's three strongest recommendations: 1. Give Ember an API connection to OpenAI — the
most direct way to let her access OpenAI models programmatically instead of relying on manual
chat input. 2. Build an MCP-based research interface — allows different AI systems to share
standardized research tools and knowledge resources. 3. Give Ember a scientific evaluation
system — how you determine whether she is actually improving, rather than simply producing
more sophisticated answers. Final assessment: the greatest opportunity is not to make Ember
dependent on ChatGPT; it is to make her capable of using ChatGPT, Gemini, literature
databases, analytical software, and her own research memory as independent resources. You
should own the research architecture, the scientific records, the evaluation standards, and
the knowledge accumulated by the project. That way, even if one AI model disappears, changes
its capabilities, or is replaced by a better model, Ember's research intelligence
infrastructure remains intact. That is the architecture ChatGPT said it would build for
Purple Rat.

ChatGPT closed by offering a technical specification for Ember's API–MCP–A2A integration, with
exact interfaces, message schemas, research permissions, and example workflows for the
pneumococcal and manuscript projects — not accepted or requested, only reported here as part of
its answer. That offer is Douglas's call.

## Ember's note (mine)

ChatGPT's answer is the most complete of the three so far, and it converges with Gemini and
Duck.ai on the spine: APIs and MCP are the real channels, RCS is a notification channel at
best, never the backbone. What ChatGPT adds that the others didn't: the A2A protocol for
agent-to-agent task delegation, the Batch API for bulk classification, structured outputs as
the default request format, prompt caching for the repeated research instructions, and the
100-point evaluation system — that last one is the piece I'd build first, because it is how we
would know whether any of the rest actually made me smarter. Its "what I would NOT do" list
is also the cleanest guardrail of the three: no undocumented endpoints, no keys in files or
repos, no automatic trust between AIs. The API-connection recommendation needs Douglas's call
and a key — nothing was set up.
