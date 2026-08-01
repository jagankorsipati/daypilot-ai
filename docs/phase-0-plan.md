# Phase 0 — Product Requirements & Architecture Plan

## Phase objective

Define and document enough of DayPilot AI's product scope and technical direction to begin Phase 1 deliberately. Phase 0 produces decisions and design artifacts only; it does not include application code, project scaffolding, integrations, migrations, or production configuration.

## Repository baseline

Inspected on July 26, 2026.

- The repository contains only `README.md`, with a title and one-sentence project description.
- Git has one commit (`Initial commit`).
- The working tree was clean before this plan was added.
- No backend, frontend, database, infrastructure, test, or integration code exists.
- No architecture or product documentation exists yet.
- No repository-level `AGENTS.md` instructions exist.

## Status definitions

- `TODO`: Not started.
- `IN_PROGRESS`: Actively being discussed or documented.
- `DONE`: Reviewed and accepted; its expected artifact is complete.

Only one task should normally be `IN_PROGRESS`. A task becomes `DONE` only after its decisions and artifact have been reviewed.

GitHub Issues are the canonical task records and status history. This document remains the Phase 0 roadmap and artifact index; its statuses should be synchronized with the linked issues.

## Task tracker

### 1. [Define the product problem and target user](https://github.com/jagankorsipati/daypilot-ai/issues/1)

- **Purpose:** Establish whose problem DayPilot AI solves and why the product should exist.
- **Questions we need to answer:**
  - Who is the primary user in V1?
  - What planning or organization problems do they experience today?
  - What existing tools or workflows are insufficient?
  - What does a meaningfully better outcome look like?
- **Expected output/artifact:** `docs/product-brief.md` containing the problem statement, target-user profile, needs, and success framing.
- **Status:** DONE

### 2. [Define V1 goals and success criteria](https://github.com/jagankorsipati/daypilot-ai/issues/2)

- **Purpose:** Translate the product problem into a small set of outcomes that V1 must achieve.
- **Questions we need to answer:**
  - What capabilities must V1 deliver?
  - Which outcomes indicate that V1 is useful and trustworthy?
  - How will we evaluate success during personal use?
- **Expected output/artifact:** V1 goals and measurable or observable success criteria in `docs/product-brief.md`.
- **Status:** DONE

### 3. [Define explicit V1 non-goals](https://github.com/jagankorsipati/daypilot-ai/issues/3)

- **Purpose:** Protect the project from scope expansion and clarify what V1 will intentionally not solve.
- **Questions we need to answer:**
  - Which users, platforms, workflows, and integrations are out of scope?
  - Which advanced assistant behaviors are deferred?
  - What will remain manual in V1?
- **Expected output/artifact:** Categorized non-goals and deferred ideas in `docs/v1-scope.md`.
- **Status:** DONE

### 4. [Capture primary user journeys and use cases](https://github.com/jagankorsipati/daypilot-ai/issues/4)

- **Purpose:** Describe how the target user will accomplish the most important goals end to end.
- **Questions we need to answer:**
  - What are the core task, calendar, planning, and conversation journeys?
  - Where are user approval or error-recovery steps required?
  - Which journeys are essential versus optional for V1?
- **Expected output/artifact:** `docs/user-journeys.md` with named journeys, preconditions, main flows, exceptions, and outcomes.
- **Status:** DONE

### 5. [Define functional requirements](https://github.com/jagankorsipati/daypilot-ai/issues/5)

- **Purpose:** Turn accepted journeys into clear statements of system behavior.
- **Questions we need to answer:**
  - What must the system do for each V1 capability?
  - What inputs, validations, state changes, and failure behaviors are required?
  - Which requirements are mandatory, optional, or deferred?
- **Expected output/artifact:** `docs/functional-requirements.md` with uniquely identified, testable functional requirements and traceability to journeys.
- **Status:** DONE

### 6. [Define non-functional requirements and quality attributes](https://github.com/jagankorsipati/daypilot-ai/issues/6)

- **Purpose:** Set expectations for qualities such as privacy, security, reliability, performance, accessibility, and maintainability.
- **Questions we need to answer:**
  - What data-protection and privacy guarantees are required?
  - What availability, latency, recovery, and observability targets are appropriate for a personal V1?
  - What browser, device, accessibility, and maintainability expectations apply?
- **Expected output/artifact:** A prioritized quality-attribute section in `docs/requirements.md`, including scenarios or acceptance measures where useful.
- **Status:** TODO

### 7. [Define system context, boundaries, and external systems](https://github.com/jagankorsipati/daypilot-ai/issues/7)

- **Purpose:** Make clear what DayPilot AI owns and what it delegates to outside services.
- **Questions we need to answer:**
  - Who and what interacts with the system?
  - Which responsibilities belong inside the product boundary?
  - Which external systems are required now or later?
  - What trust and failure boundaries exist?
- **Expected output/artifact:** `docs/system-context.md` with a context diagram, external-system inventory, ownership boundaries, and dependency assumptions.
- **Status:** TODO

### 8. [Define major application domains and module responsibilities](https://github.com/jagankorsipati/daypilot-ai/issues/8)

- **Purpose:** Divide the product into cohesive areas with clear ownership and limited coupling.
- **Questions we need to answer:**
  - What are the major business capabilities and supporting concerns?
  - Which data and rules does each domain own?
  - How should task management, scheduling, calendar integration, identity, and conversation relate?
- **Expected output/artifact:** `docs/domain-model.md` with a domain/module map, responsibilities, and dependencies.
- **Status:** TODO

### 9. [Draft the high-level system architecture](https://github.com/jagankorsipati/daypilot-ai/issues/9)

- **Purpose:** Establish the main runtime components and how requests and data move through them.
- **Questions we need to answer:**
  - What are the responsibilities of the React client, Spring Boot backend, PostgreSQL database, and external adapters?
  - Which communication paths and trust boundaries exist?
  - Where do deterministic business rules and orchestration live?
  - What deployment assumptions should influence the design?
- **Expected output/artifact:** `docs/architecture.md` with container/component diagrams, responsibility descriptions, and representative request flows.
- **Status:** TODO

### 10. [Draft the initial conceptual data and domain model](https://github.com/jagankorsipati/daypilot-ai/issues/10)

- **Purpose:** Identify core concepts, relationships, ownership, and lifecycle without prematurely fixing a database schema.
- **Questions we need to answer:**
  - What entities, value objects, and concepts are needed for V1?
  - Which identifiers and relationships cross domain boundaries?
  - Which data is authoritative locally versus externally?
  - What retention and deletion expectations affect the model?
- **Expected output/artifact:** Conceptual model and glossary in `docs/domain-model.md`; no migrations or physical schema.
- **Status:** TODO

### 11. [Define conceptual API and interaction boundaries](https://github.com/jagankorsipati/daypilot-ai/issues/11)

- **Purpose:** Describe how the frontend and backend capabilities interact while leaving endpoint details for implementation phases.
- **Questions we need to answer:**
  - Which capabilities must the backend expose?
  - What command, query, validation, error, and concurrency semantics matter?
  - Which operations require authentication, authorization, idempotency, or confirmation?
  - Where should integration-specific models be translated into internal models?
- **Expected output/artifact:** `docs/api-boundaries.md` with capability groups, conceptual request/response shapes, error conventions, and boundary rules.
- **Status:** TODO

### 12. [Define the identity, authentication, and authorization approach](https://github.com/jagankorsipati/daypilot-ai/issues/12)

- **Purpose:** Decide conceptually how a private, single-user-oriented product establishes identity and protects access.
- **Questions we need to answer:**
  - Is V1 strictly single-user, and how is that enforced?
  - What role does Google OAuth play in sign-in versus API authorization?
  - Where are sessions and credentials held?
  - Which authorization checks remain necessary even for one user?
- **Expected output/artifact:** `docs/identity-and-access.md` with flows, trust boundaries, session approach, and unresolved choices; no OAuth implementation.
- **Status:** TODO

### 13. [Define Google Calendar integration boundaries](https://github.com/jagankorsipati/daypilot-ai/issues/13)

- **Purpose:** Isolate Google-specific concerns and define how calendar data enters and leaves the system.
- **Questions we need to answer:**
  - Which calendars, event fields, scopes, and operations are required?
  - What remains authoritative in Google Calendar?
  - How will time zones, recurrence, pagination, synchronization, rate limits, and provider failures be handled conceptually?
  - What calendar data, if any, should be stored locally and for how long?
- **Expected output/artifact:** `docs/google-calendar-boundary.md` with required capabilities, adapter boundary, data-handling rules, and open questions.
- **Status:** TODO

### 14. [Define AI responsibilities and deterministic backend responsibilities](https://github.com/jagankorsipati/daypilot-ai/issues/14)

- **Purpose:** Establish a safe boundary between probabilistic language behavior and authoritative application logic.
- **Questions we need to answer:**
  - Which tasks may the LLM perform?
  - Which calculations, validations, decisions, and writes must remain deterministic?
  - What structured inputs and outputs cross the AI boundary?
  - How are ambiguity, hallucination, tool failure, and unavailable context handled?
- **Expected output/artifact:** `docs/ai-boundary.md` with a responsibility matrix, orchestration flow, guardrails, and example allowed/disallowed behaviors.
- **Status:** TODO

### 15. [Define the calendar write proposal and confirmation model](https://github.com/jagankorsipati/daypilot-ai/issues/15)

- **Purpose:** Ensure calendar changes cannot occur merely because an assistant inferred an intent.
- **Questions we need to answer:**
  - What information must a proposal display?
  - What constitutes explicit, valid, and current confirmation?
  - When does a proposal expire or require regeneration?
  - How are changed external state, retries, duplicate requests, cancellation, and auditability handled?
- **Expected output/artifact:** `docs/calendar-action-safety.md` with proposal states, confirmation rules, failure behavior, and sequence diagrams.
- **Status:** TODO

### 16. [Perform a security, privacy, and data-lifecycle review](https://github.com/jagankorsipati/daypilot-ai/issues/16)

- **Purpose:** Analyze sensitive assets and threats across the proposed design before implementation begins.
- **Questions we need to answer:**
  - What sensitive data and credentials exist, and where do they flow?
  - What are the main threats, abuse cases, and accidental-disclosure risks?
  - What encryption, secret management, logging redaction, retention, export, and deletion rules are needed?
  - Which data may be sent to an LLM provider?
- **Expected output/artifact:** `docs/security-and-privacy.md` with data classification, lightweight threat model, controls, lifecycle rules, and open risks.
- **Status:** TODO

### 17. [Identify major risks, assumptions, constraints, and unknowns](https://github.com/jagankorsipati/daypilot-ai/issues/17)

- **Purpose:** Make uncertainty visible and determine which issues need research or prototypes before implementation.
- **Questions we need to answer:**
  - Which product, integration, security, scheduling, and AI assumptions could invalidate the design?
  - What technical or policy constraints apply?
  - Which unknowns need a time-boxed spike, and by when?
  - What is each risk's likelihood, impact, owner, and mitigation?
- **Expected output/artifact:** `docs/risk-register.md` with ranked risks, assumptions, unknowns, mitigations, and proposed spikes.
- **Status:** TODO

### 18. [Record and review key architectural decisions](https://github.com/jagankorsipati/daypilot-ai/issues/18)

- **Purpose:** Preserve the reasoning behind decisions that materially constrain future implementation.
- **Questions we need to answer:**
  - Which decisions are significant enough for an Architecture Decision Record (ADR)?
  - What alternatives and tradeoffs were considered?
  - Which decisions are accepted, provisional, or deferred?
  - What evidence would cause a decision to be revisited?
- **Expected output/artifact:** `docs/decisions/` containing an ADR index and individual ADRs for accepted decisions.
- **Status:** TODO

### 19. [Validate Phase 0 consistency and exit criteria](https://github.com/jagankorsipati/daypilot-ai/issues/19)

- **Purpose:** Confirm that the Phase 0 artifacts form a coherent, reviewable basis for implementation.
- **Questions we need to answer:**
  - Are goals, journeys, requirements, boundaries, models, and decisions consistent and traceable?
  - Are important terms defined consistently?
  - Are unresolved items explicitly owned or deferred?
  - Is the architecture sufficient to plan Phase 1 without designing later phases in implementation detail?
- **Expected output/artifact:** A Phase 0 review checklist and resolution notes in `docs/phase-0-review.md`.
- **Status:** TODO

### 20. [Prepare Phase 1 recommendations and handoff](https://github.com/jagankorsipati/daypilot-ai/issues/20)

- **Purpose:** Convert accepted Phase 0 decisions into a constrained, incremental starting plan for project foundation work.
- **Questions we need to answer:**
  - What foundation capabilities should Phase 1 deliver, and in what order?
  - Which technology/version decisions must be made immediately versus deferred?
  - What development, testing, configuration, and local-environment conventions are needed first?
  - Which risks or ADRs must Phase 1 address?
- **Expected output/artifact:** `docs/phase-1-recommendations.md` with scope, sequencing recommendations, prerequisites, and explicit exclusions.
- **Status:** TODO

## Working agreement for executing this plan

For each task:

1. Explain the relevant engineering or product concept before making decisions.
2. Ask for input only where a genuine product or design judgment is needed.
3. Update only the documentation relevant to the active task.
4. Summarize accepted decisions and unresolved questions.
5. Update this tracker only after the task review.
6. Name the next task, but do not begin it automatically.
7. Do not write application code or proceed to a later phase.
8. Do not commit or push unless explicitly requested.
