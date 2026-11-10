# Synaptech Solutions

**Practical software. Honest AI.**

🌐 [synaptech-solutions.com](https://synaptech-solutions.com/) ·
[Español](https://synaptech-solutions.com/es) ·
✉️ [g.martinez@synaptech-solutions.com](mailto:g.martinez@synaptech-solutions.com)

## Synaptech as a business

Synaptech Solutions is the independent software engineering practice of Germán
Martínez, based in Uruguay. It builds AI, LLM and backend systems that run in
production, for teams that need AI to work reliably: AI assistants, ERP and MCP
integrations, data pipelines and workflow automation. The work is remote, with
teams in Latin America, the United States and Europe.

Most of the experience is in three areas:

- **ERP software:** assistants that read and act on ERP records, and ERP
  reporting exposed to LLM clients through the Model Context Protocol (MCP),
  with OAuth and explicit report parameters.
- **Chatbots with RAG and GraphRAG:** conversational assistants grounded in
  product manuals, internal wikis and live business data, orchestrated with
  LangChain and LangGraph.
- **Knowledge bases on graph databases:** knowledge graphs built with Neo4j and
  Cognee, so an assistant can follow how entities relate to each other instead
  of pulling back loose text chunks.

How the work gets done:

- **Architecture before implementation.** Every project starts with a written
  spec, so scope and "done" are clear before any code is written.
- **AI as infrastructure, not magic.** LLM features ship with evals, guardrails
  and fallbacks, because models fail silently and drift over time.
- **Honest tradeoffs, documented decisions.** If AI isn't the right tool for a
  problem, you hear it before anything gets built.
- **Ownership by default.** Clients get the code, documentation and runbooks,
  so their systems don't depend on Synaptech to keep running.

**Products in development**

- **Hilo Nativo:** a multi-seller marketplace for handcrafted knitwear. It's a
  Python 3.12 modular monolith (FastAPI, with Jinja2 and HTMX for server-rendered
  pages, and SQLAlchemy 2 and Alembic on PostgreSQL) that runs as two process
  roles from one codebase: the web app, and an APScheduler worker for
  settlements, payouts, reconciliation and retries. Payment state comes only
  from verified, idempotent Mercado Pago webhooks. Money moves through an
  append-only ledger with compensating corrections, and stock is reserved under
  row locks, with a database constraint that blocks over-reservation.
  Buyer-seller messages and attachments are encrypted at rest. Attachments go to
  private object storage, and operator tools sit behind capability-based
  authorization. Tracing and metrics use OpenTelemetry.
- **Rentica:** property management for landlords: units, tenants, rent
  payments, guaranties, rent adjustments, maintenance and tax records. One Expo
  and React Native (TypeScript) codebase targets iOS, Android and web. It talks
  to an async FastAPI backend (SQLAlchemy 2 and Alembic, with SQLite for local
  development and PostgreSQL in production). Auth uses short-lived JWTs with
  single-use, rotating refresh sessions and per-IP and per-email rate limits.
  Uploads are served only through ownership-checked endpoints, and on the web,
  nginx serves the static export and proxies the API from the same origin.
- **Better Writing:** an AI-augmented creative writing platform built as 13
  Python microservices, each with its own PostgreSQL database (PostGIS, pgvector
  or Apache AGE where a service needs them). Services call each other over gRPC
  contracts managed with Buf, and publish domain events on NATS JetStream through
  FastStream. A FastAPI gateway combines them into one HTTP and WebSocket API. A
  plot graph, ordered with a NetworkX topological sort, is the clock that
  versions characters and locations. Sections are co-edited through
  Yjs-compatible CRDTs (pycrdt), and the AI layer combines LiteLLM, RAG over
  pgvector and structured output.

Services include new production systems, architecture audits and workflow
automation. The [website](https://synaptech-solutions.com/) has the details.

## Synaptech in open source

The projects below came out of the day-to-day work. Each one goes public when
it's solid enough for a first release.

**Available now**

### [Corrosion](https://github.com/Synaptech-Solutions-SAS/Corrosion-VST)

An industrial physical-modeling instrument for VST3 and CLAP, written in Rust
with NIH-plug and an egui editor. Instead of oscillators, every note runs an
exciter → object → damage → body/space signal path: 16 exciters (strikes, bows,
grinding, pneumatic jets…) drive 9 objects (pipe, plate, tank, chain, I-beam,
cable, spring, sheet metal, cog), each an algorithmic modal resonator.

It plays with 16-voice polyphony, full MIDI expression with per-note tuning and
choke in CLAP and VST3 hosts, four macros, a drum-kit mode and more than 130
automatable parameters, through a post chain of a ladder filter,
Lorenz-attractor drive, FEM body resonance, HRTF spread and an oversampled
diode clipper. The audio callback never allocates, locks or does I/O, which a
test enforces, and offline render tests hold aliasing to a set budget.

*v0.2.0, with 214 factory presets. Nightly builds for Windows, macOS and Linux
are validated with clap-validator and pluginval. MIT.*

**Coming soon**

### Omnisnap

Shows exactly which elements render differently in every browser engine your
users run, with one command and the browsers already installed. Instead of
pixel diffs, it compares element geometry (sizes, positions, line wraps,
overflow, truncation) and reports each difference at the element where it
starts, not at every element it pushes down the page.

It discovers Chrome, Edge, Brave, Opera, Vivaldi, Chromium, Firefox, Safari and
WebKitGTK and drives them over CDP, WebDriver BiDi or WebDriver Classic, running
branded browsers as shipped. Every finding comes with a cause: it neutralizes
the suspects and measures the page again, and a third engine settles which one
is wrong. Results go to a self-contained local report, or to one pull request
comment from a report-only GitHub Action on Ubuntu, Windows and macOS.

The prototype found 24/24 planted bugs at the right element, with no false
reports on bug-free pages across five engines. *Design and prototype: v1 is
specified in 17 module specs. Apache 2.0.*

### OpenCode HyperFlow

An [OpenCode](https://opencode.ai) plugin that runs the development lifecycle,
from product spec to release, as a state machine with quality gates. The LLM
orchestrates and deterministic TypeScript tools do the work: a PRD is atomized
into specs, questions and decisions with traceable IDs, planning waits until
every question is resolved, and a phase kernel refuses illegal transitions.

Implementation is test-first, repairs stop after three attempts, and shipping
requires lint, typecheck, tests, coverage, security scanning, fuzzing and
ablation checks that prove the tests catch regressions. *v0.1.0 MVP: 11 agents,
21 commands, 16 skills and 37 tools, all implemented, with 113 tests passing.
MIT.*

The full version (v1.0), already specified, adds regression-first bugfix and
behavior-preserving refactor workflows, versioned re-planning, test tool
selection across 14 language ecosystems, drift detection, and generated CI and
release checklists. Parallel tasks, browser automation and multi-repo support
are planned for v1.0. It won't install, delete, migrate, commit or deploy
anything without your approval.

**How the projects work**

- **Spec first.** Research and planning come before code. Projects plan their
  work with [OpenSpec](https://github.com/Fission-AI/OpenSpec) or
  [agent-skills](https://github.com/addyosmani/agent-skills), and the plans
  live in the repository, so you can see what's coming before you contribute.
- **Maintained alongside the business.** Replies and reviews can take a while,
  but every issue and pull request gets read.
- **Contributions.** Each project's README says what it accepts at its current
  stage. Read the
  [contributing guidelines](https://github.com/Synaptech-Solutions-SAS/.github/blob/main/CONTRIBUTING.md)
  before you start.
- **AI-assisted work is accepted**, as long as you understand it, verify it,
  and disclose it.
- **Found a vulnerability?** Don't open a public issue. Follow the
  [security policy](https://github.com/Synaptech-Solutions-SAS/.github/blob/main/SECURITY.md)
  to report it privately.
