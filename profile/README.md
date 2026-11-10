# Synaptech Solutions

**Practical software. Honest AI.**

🌐 [synaptech-solutions.com](https://synaptech-solutions.com/) ·
[Español](https://synaptech-solutions.com/es)

## Synaptech as a business

Synaptech Solutions is the independent software engineering practice of Germán
Martínez, based in Uruguay. It builds AI, LLM and backend systems that run in
production, for teams that need AI to work reliably: AI assistants, ERP and MCP
integrations, data pipelines and workflow automation. The work is remote, with
teams in Latin America, the United States and Europe.

How the work gets done:

- **Architecture before implementation.** Every project starts with a written
  spec, so scope and "done" are clear before any code is written.
- **AI as infrastructure, not magic.** LLM features ship with evals, guardrails
  and fallbacks, because models fail silently and drift over time.
- **Honest tradeoffs, documented decisions.** No vague AI hype: if AI isn't the
  right tool for a problem, that gets said up front.
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

Services range from new production systems and architecture audits to workflow
automation. The [website](https://synaptech-solutions.com/) has the details.

## Synaptech in open source

Some of the tools built for this work are being prepared for release as open
source. They're private for now: each one goes public once it meets the quality
bar for a first release.

**Coming soon**

- **Omnisnap:** shows exactly which elements render differently in every
  browser engine your users run, with one command and the browsers already
  installed. It compares element geometry across engines, explains why each
  difference happens, and tells you whether anyone would see it.
  *Design and prototype.*
- **OpenCode HyperFlow:** an [OpenCode](https://opencode.ai) plugin for
  structured development workflows. It turns a product spec into atomic specs,
  a plan and a task graph, then guides implementation with TDD and quality
  gates. *v0.1.0 MVP.*
- **Corrosion:** an industrial physical-modeling instrument for VST3 and CLAP,
  written in Rust. MIDI notes excite modal resonators tuned for damaged metal,
  friction and mechanical tension instead of synth oscillators. *v0.1.0.*

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
