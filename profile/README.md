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

Areas of deep experience:

- **ERP software:** assistants that read and act on ERP records, and ERP
  reporting exposed to LLM clients through the Model Context Protocol (MCP),
  with OAuth and explicit report parameters.
- **Chatbots with RAG and GraphRAG:** conversational assistants grounded in
  product manuals, internal wikis and live business data, orchestrated with
  LangChain and LangGraph.
- **Knowledge bases on graph databases:** knowledge graphs built with Neo4j and
  Cognee that give assistants connected context, not isolated text chunks.

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

### Omnisnap

Shows exactly which elements render differently in every browser engine your
users run, with one command and the browsers already installed. Instead of
pixel diffs, it compares **element geometry** (sizes, positions, line wraps,
overflow, truncation) and reports each difference at the element where it
starts, not at every element it pushes down the page.

- **Your browsers, as installed:** it discovers Chrome, Edge, Brave, Opera,
  Vivaldi, Chromium, Firefox, Safari and WebKitGTK, and drives them over CDP,
  WebDriver BiDi or WebDriver Classic. Nothing is downloaded unless you ask, and
  branded browsers run as shipped, so Brave Shields and Edge tracking
  prevention behave as they do for your users.
- **Stable captures:** each engine is captured after fonts, lazy content and
  animations settle, and twice, so dynamic content is recognized and ignored.
- **Explained findings:** suspected causes (fractional line-heights, fonts,
  form-control defaults) are neutralized and the page re-measured to confirm the
  cause and the fix. A third engine family decides which engine is the odd one
  out, and broken design intent (alignments, equal heights, even spacing) is
  flagged.
- **Local and CI:** a self-contained local report with synced side-by-side
  screenshots, and a report-only GitHub Action on Ubuntu, Windows and macOS that
  posts one pull request comment. npm and PyPI packages will wrap the same Go
  binary.
- **Prototype results:** 24/24 planted bugs found at the right element, zero
  report-level causes on bug-free control pages across five engines, and at
  least 99.9% of elements matched between engines on real sites.

*Design and prototype: v1 is specified in 17 module specs. Apache 2.0.*

### OpenCode HyperFlow

An [OpenCode](https://opencode.ai) plugin that runs the whole development
lifecycle, from product spec to release, as a state machine with quality gates.
The LLM orchestrates; deterministic TypeScript tools do the work.

- **What it installs:** 11 specialized agents, 21 `/hf-*` commands, 16 skills,
  37 deterministic tools and 7 plugin modules, with one
  `npx opencode-hyperflow install`.
- **Spec to tasks:** a PRD is atomized into specs, open questions and decisions
  with traceable IDs (`SPEC-0001`, `TASK-0001`). Planning is blocked until every
  question is resolved. Plans are immutable and versioned, and tasks form a
  dependency graph with parallelization hints.
- **Enforced workflow:** a phase kernel (`INITIALIZED` → `PRD_ATOMIZED` →
  `PLAN_CONFIRMED` → `TASKS_READY` → … → `HANDOFF_READY`) refuses illegal
  transitions.
- **TDD and gates:** implementation requires a failing test first, repairs stop
  after three attempts, and shipping needs lint, typecheck, unit tests,
  coverage, BDD, security scanning, fuzzing and ablation checks that confirm the
  tests catch regressions.
- **Safety first:** no silent overwrites, backups before every write, and
  approval gates for destructive actions.

*v0.1.0 MVP: every agent, command, skill and tool is implemented, and 113 tests
pass. MIT.*

**The full version (v1.0)** is specified in a PRD and grows the system to 16
agents, 34 skills and 36 tools, behind the same small set of commands:

- **Separate workflows by kind of work:** `/hf-bugfix` writes a failing
  regression test before any patch, and ablation then confirms the test catches
  the bug. `/hf-refactor` writes characterization tests first and requires
  zero behavior drift unless you approve it. `/hf-replan` regenerates the plan
  from your feedback, keeps every earlier version, and records the feedback as
  a decision.
- **Language-aware testing across 14 ecosystems:** existing project tooling
  wins, then native tools. For example, Vitest and fast-check for TypeScript,
  pytest and Hypothesis for Python, `go test` with native fuzzing, proptest and
  cargo-fuzz for Rust, JUnit 5 and jqwik for Java, and libFuzzer or AFL++ for
  C and C++. Nothing is installed without approval.
- **Deeper verification:** fuzz and property testing in smoke, targeted and
  deep modes, spec drift detection, behavior drift detection, and quality
  scoring. New subagents write BDD scenarios, attack input surfaces, and
  prepare releases.
- **Shipping:** generated CI for GitHub Actions and GitLab, plus release notes
  and rollback, migration and observability checklists. Production deployment
  never runs automatically.
- **Planned for v1.0:** parallel task execution, browser automation, multi-repo
  support, release automation, a telemetry dashboard, side-by-side comparison
  of plan versions, and AST-aware ablation.
- **Approval by default:** it never installs dependencies, deletes files, runs
  migrations, commits or deploys without your approval.

### Corrosion

An industrial physical-modeling instrument for VST3 and CLAP, written in Rust
with NIH-plug and an egui editor. Instead of oscillators, every note runs an
**exciter → object → damage → body/space** signal path, tuned for damaged
metal, friction, weight and mechanical tension.

- **Sound sources:** 16 exciters (strikes, bows, grinding, pneumatic jets,
  electromagnetic hum, particle rain…) in three envelope families, driving 9
  objects (pipe, plate, tank, chain, I-beam, taut cable, coil spring, sheet
  metal, industrial cog). Each object is an algorithmic modal resonator with
  its own character parameters.
- **Playing:** 16-voice polyphony with tiered voice stealing, full MIDI
  expression (pitch bend, channel and polyphonic pressure, mod wheel, sustain),
  four macros (Mass, Corrosion, Violence, Brightness), tonal, kit and drone
  modes, and more than 130 automatable parameters.
- **Post chain:** a WDF-style ladder filter, Lorenz-attractor drive, FEM body
  resonance, HRTF stereo spread, factory, spring and tempo-synced echo spaces,
  and an oversampled clipper. Quality modes scale oversampling (1× to 16×)
  and modal density together.
- **Real-time safe:** no heap allocation, locks or I/O in the audio callback
  (enforced by a test), NaN and denormal guards at every voice, and aliasing
  held to an asserted budget by offline render tests.

*v0.1.0, with 50 factory presets.*

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
