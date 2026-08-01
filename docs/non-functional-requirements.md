# DayPilot AI V1 Non-Functional Requirements

## Status

Approved — Phase 0 Task #6 complete.

## Purpose and scope

Functional requirements define what DayPilot V1 must do. These non-functional requirements define the quality, safety, privacy, reliability, performance, accessibility, maintainability, and operational conditions under which those capabilities must work.

The requirements are calibrated for a private, owner-controlled, single-user V1. They do not introduce public SaaS, multi-tenant, enterprise-scale, or formal-certification expectations.

## Interpretation guidance

- **Must Have:** Required to operate V1 safely, protect owner data, or make an approved capability trustworthy.
- **Should Have:** Important quality improvement that may be deferred if it does not compromise core safety or data integrity.
- **Could Have:** Optional enhancement. None are proposed while the basic quality baseline is under review.
- A verification approach describes how a later phase can demonstrate conformance; it does not prescribe implementation.
- Performance targets cover behavior controlled by DayPilot. Latency introduced by Google Calendar or an AI provider is reported separately and is not represented as locally controllable.
- “Sensitive data” includes authentication credentials, calendar and task content, conversation content, explicit preferences, and diagnostic data that can reveal personal activity.

## Security

| Identifier | Title | Requirement | Rationale | Verification approach | Priority | Related capability or principle |
| --- | --- | --- | --- | --- | --- | --- |
| NFR-SEC-001 | Least-privilege external access | The system shall request only the external authorization scopes required by approved V1 capabilities and shall document the purpose of each requested scope. | Calendar and identity access expose sensitive owner data. | Scope inventory and security review | Must Have | FR-001–FR-008, FR-039, FR-050 |
| NFR-SEC-002 | Credential protection | The system shall protect authentication credentials and external-service tokens from unauthorized disclosure both while stored and while transmitted. | Compromised credentials could expose or modify the owner's calendar. | Security review and configuration inspection | Must Have | FR-001–FR-008, FR-042–FR-050 |
| NFR-SEC-003 | No committed secrets | Source control shall contain no live credentials, tokens, private keys, or environment-specific secrets, and documented secret-detection checks shall be run before releases. | Repository history is difficult to sanitize after disclosure. | Repository scan and release checklist review | Must Have | Owner-controlled operation |
| NFR-SEC-004 | Sensitive-value log exclusion | Logs shall not contain authentication tokens, credentials, session secrets, or complete authorization headers. | Diagnostic data must not become a credential leak. | Automated log-capture test and security review | Must Have | NFR-OBS-001 |
| NFR-SEC-005 | Owner authorization boundary | Every operation that reads or changes locally held personal data or invokes an owner-authorized external action shall be limited to the authenticated owner. | Single-user does not mean unauthenticated. | Authorization tests and security review | Must Have | FR-009–FR-017, FR-041–FR-050 |
| NFR-SEC-006 | Assistant cannot grant authority | Assistant-generated text, interpreted intent, or external content shall not bypass authorization checks or the explicit-confirmation rules for consequential actions. | Probabilistic output must not become an authority source. | Adversarial workflow tests and security review | Must Have | “DayPilot assists; the user decides,” FR-041–FR-046 |

## Privacy and data minimization

| Identifier | Title | Requirement | Rationale | Verification approach | Priority | Related capability or principle |
| --- | --- | --- | --- | --- | --- | --- |
| NFR-PRIV-001 | Purpose-limited local storage | The system shall retain only personal data needed for approved V1 capabilities, explicit preferences, recovery, or owner-requested history. | DayPilot handles detailed personal activity. | Data inventory and documentation review | Must Have | V1 scope boundaries, FR-009–FR-017, FR-036–FR-040 |
| NFR-PRIV-002 | Minimize AI-provider disclosure | For each AI-assisted operation, the system shall send only the calendar, task, preference, and conversation context needed for that operation. | Unnecessary transmission increases privacy exposure. | Data-flow review and integration tests with captured request metadata | Must Have | FR-029–FR-035 |
| NFR-PRIV-003 | Document external data flows | The project shall document what categories of owner data leave the owner-controlled system, why they are sent, and which external service receives them. | The owner must understand the privacy boundary. | Documentation and data-flow review | Must Have | Google Calendar and future AI integration boundaries |
| NFR-PRIV-004 | No hidden-reasoning retention | The system shall not request or retain hidden model reasoning or chain-of-thought. User-facing explanations shall contain concise known inputs, constraints, and rules only. | Hidden reasoning is unnecessary for useful explainability and creates retention risk. | Request/response review and tests of explanation output | Must Have | FR-032, NFR-PRIV-002 |
| NFR-PRIV-005 | Inspectable durable preferences | Every durable planning preference shall be visible to the owner and changeable or removable by the owner. | V1 rejects implicit long-term behavioral memory. | Acceptance tests and privacy review | Must Have | FR-036–FR-040 |
| NFR-PRIV-006 | Delete locally stored personal data | The system shall allow the owner to delete locally stored tasks, an individual retained conversation, or all retained conversation history without deleting Google Calendar commitments or required structured action records. | The owner needs control over locally retained personal information while safety records may have a separate lifecycle. | Acceptance and data-lifecycle tests | Must Have | FR-014, FR-040 |
| NFR-PRIV-007 | Limit conversation retention | The system shall retain permitted conversation history across sessions for 30 days by default and shall remove it after that period unless the owner deletes it sooner. Hidden model reasoning, chain-of-thought, and unnecessary internal model artifacts shall not be retained. | Conversation continuity must have a bounded and understandable privacy cost. | Retention-boundary tests and data-lifecycle review | Must Have | FR-029–FR-035, FR-040 |

## Reliability and data integrity

| Identifier | Title | Requirement | Rationale | Verification approach | Priority | Related capability or principle |
| --- | --- | --- | --- | --- | --- | --- |
| NFR-REL-001 | Calendar authority | The system shall treat current Google Calendar state, not a conversational summary or local proposal, as authoritative for calendar commitments. | Planning against a secondary copy can produce conflicts. | Integration tests and failure-injection tests | Must Have | FR-001–FR-008, FR-045 |
| NFR-REL-002 | Proposal revalidation | The system shall revalidate the relevant current calendar state immediately before a confirmed calendar write and require renewed review if the proposal is no longer current. | State can change between proposal and confirmation. | Concurrency and integration tests | Must Have | FR-042–FR-045, FR-050 |
| NFR-REL-003 | Duplicate-write prevention | A retry, repeated confirmation, or delayed response shall not create or apply the same consequential calendar change more than once. | External calls can time out after succeeding. | Retry and failure-injection tests | Must Have | FR-043–FR-045, FR-050 |
| NFR-REL-004 | Truthful operation result | The system shall report a calendar change as successful only after its success is verified and shall clearly report failure or an unknown result. | False success causes the owner to trust incorrect calendar state. | Integration and ambiguous-outcome tests | Must Have | FR-035, FR-049 |
| NFR-REL-005 | Task durability | Confirmed task creation, edits, completion changes, and removals shall survive normal application restart without silent loss or reversal. | Tasks must be a trusted replacement for memory. | Restart and persistence tests | Must Have | FR-009–FR-016 |
| NFR-REL-006 | Failure atomicity | A failed operation shall not leave local task state or a calendar-change record partially applied or internally contradictory. | Partial state undermines future planning. | Transactional and failure-injection tests | Must Have | FR-009–FR-016, FR-042–FR-050 |
| NFR-REL-007 | Deterministic availability results | Given the same calendar state, task constraints, preferences, time zone, and evaluation time, deterministic availability and placement rules shall produce the same result. | Core scheduling truth must be reproducible and testable. | Repeatability tests | Must Have | FR-004–FR-006, FR-022–FR-026 |

## Performance and responsiveness

| Identifier | Title | Requirement | Rationale | Verification approach | Priority | Related capability or principle |
| --- | --- | --- | --- | --- | --- | --- |
| NFR-PERF-001 | Local task responsiveness | With up to 5,000 locally stored tasks, at least 95% of locally processed task create, view, edit, completion, and removal operations shall complete within 1 second. | Task capture should not interrupt the user's thought. | Automated performance test using the representative V1 volume | Must Have | FR-009–FR-017 |
| NFR-PERF-002 | Availability calculation responsiveness | Once required calendar data is available locally, at least 95% of availability and task-placement calculations shall complete within 2 seconds for a query spanning no more than 90 days, containing up to 1,000 calendar events, and considering up to 100 candidate tasks. | Availability questions are interactive decisions. | Automated performance test using the representative V1 volume | Must Have | FR-004–FR-006, FR-022–FR-026 |
| NFR-PERF-003 | Daily-plan processing responsiveness | Once required calendar and task data is available, at least 95% of locally controlled daily-overview and planning processing shall complete within 2 seconds while considering up to 100 candidate tasks and the relevant portion of the representative event set. | Morning planning should provide timely orientation. | Automated performance test using the representative V1 volume | Should Have | FR-018–FR-021 |
| NFR-PERF-004 | Slow-operation feedback | When an external-service operation has not completed within 2 seconds, the system shall indicate that work is still in progress and shall ultimately report success, failure, timeout, or an unknown outcome. | Google and AI-provider latency cannot be guaranteed locally. | Simulated-latency usability and integration tests | Must Have | FR-007, FR-033, FR-049 |

## Availability and resilience

| Identifier | Title | Requirement | Rationale | Verification approach | Priority | Related capability or principle |
| --- | --- | --- | --- | --- | --- | --- |
| NFR-RES-001 | Calendar-outage degradation | When Google Calendar is unavailable, the system shall keep locally available task capabilities usable where safe and shall not claim current calendar availability. | A provider outage should not disable unrelated task work or produce unsafe advice. | Provider-outage test | Must Have | FR-007, FR-009–FR-017 |
| NFR-RES-002 | AI-outage degradation | When the AI provider is unavailable, the system shall preserve deterministic task and calendar capabilities that do not require language interpretation and shall identify the unavailable assistant capability. | Core records and rules should not depend entirely on AI availability. | Provider-outage test | Must Have | AI boundary principle, FR-033 |
| NFR-RES-003 | Staleness indication | If displayed or evaluated calendar information may be stale, the system shall identify that condition and shall not carry out a consequential calendar action until current state is revalidated. | Stale data can create conflicts. | Stale-data and integration tests | Must Have | FR-007, FR-030, FR-045 |
| NFR-RES-004 | Safe retry policy | The system shall retry failed external operations only when the retry cannot create an unconfirmed or duplicate consequential action. | Blind retries can double-book the owner. | Failure-injection and retry tests | Must Have | NFR-REL-003, FR-043–FR-045 |
| NFR-RES-005 | Recoverable owner data | Before V1 is ready for regular personal use, the system shall support backup creation for DayPilot-owned data, provide a documented restoration procedure, and periodically verify that restoration succeeds. Credentials and sensitive integration data shall be excluded from backups or protected appropriately, and backup or restore failure shall be reported truthfully. | Owner-controlled hosting still needs verified recovery from local loss without creating an unsafe credential copy. | Backup-and-restore exercise, documentation review, and backup-content security inspection | Must Have | FR-009–FR-017, FR-036–FR-040 |

No public uptime percentage or enterprise disaster-recovery target is proposed for V1.

## Usability and accessibility

| Identifier | Title | Requirement | Rationale | Verification approach | Priority | Related capability or principle |
| --- | --- | --- | --- | --- | --- | --- |
| NFR-UX-001 | Proposal/action distinction | The system shall make a pending proposal visually and textually distinguishable from an action that has been successfully executed. | Confusing a suggestion with a write undermines user control. | Usability review and acceptance tests | Must Have | FR-041–FR-045 |
| NFR-UX-002 | Explicit confirmation choices | Consequential proposals shall provide clearly labeled confirm and reject choices, and keyboard users shall be able to reach and activate both. | Approval must be deliberate and accessible. | Keyboard and usability tests | Must Have | FR-042–FR-046 |
| NFR-UX-003 | Actionable messages | Error and uncertainty messages shall state what could not be determined or completed, whether any change occurred, and what the user can do next. | The owner needs a safe recovery path. | Content review and failure-scenario tests | Must Have | FR-007, FR-030, FR-033, FR-049 |
| NFR-UX-004 | Keyboard operability | All V1 workflows shall be operable using a keyboard without requiring pointer input. | Keyboard access is a foundational accessibility expectation. | Keyboard-only usability test | Must Have | Journeys 1–7 |
| NFR-UX-005 | Perceivable status | Status, conflict, priority, success, and failure shall not be communicated by color alone and shall have readable text labels. | Meaning must remain available to users with color-vision differences or nonvisual access. | Accessibility review and automated checks | Must Have | Journeys 1–7 |
| NFR-UX-006 | Visible focus and programmatic labels | Interactive controls shall have a visible keyboard focus indicator and an accessible name that communicates their purpose. | Users must be able to locate and understand controls. | Automated accessibility scan and manual review | Must Have | Journeys 1–7 |

## Time and time-zone correctness

| Identifier | Title | Requirement | Rationale | Verification approach | Priority | Related capability or principle |
| --- | --- | --- | --- | --- | --- | --- |
| NFR-TIME-001 | Explicit owner time zone | The system shall maintain an explicit, inspectable owner time zone used for planning, deadlines, and display unless the user specifies another zone for a request. | Silent machine-zone assumptions can schedule the wrong time. | Configuration and acceptance tests | Must Have | FR-003, FR-036–FR-039 |
| NFR-TIME-002 | Time-zone display context | Dates and times shall display their relevant date and time-zone context whenever omission could make a commitment or proposal ambiguous. | Users must know which local time they are approving. | Content and acceptance tests | Must Have | FR-003, FR-042–FR-046, FR-050 |
| NFR-TIME-003 | Daylight-saving correctness | Availability, duration, deadlines, and calendar proposals spanning a daylight-saving transition shall reflect the actual elapsed time and the applicable local offset. | Clock changes create non-obvious gaps and overlaps. | Boundary-date automated tests | Must Have | FR-003–FR-006, FR-022, FR-042–FR-050 |
| NFR-TIME-004 | Relative-date clarification | When a relative date or time phrase has more than one reasonable interpretation, the system shall present or request an explicit date and time before a consequential proposal. | “Tomorrow” or “afternoon” can be unsafe near boundaries or without a defined preference. | Ambiguity scenario tests | Must Have | FR-003, FR-030, FR-042–FR-045 |
| NFR-TIME-005 | Consistent temporal comparison | The system shall compare deadlines, commitments, buffers, and available intervals using a consistent instant and time-zone interpretation. | Inconsistent comparison produces missed deadlines or false availability. | Automated boundary and property-based tests | Must Have | FR-004–FR-006, FR-021–FR-026 |

## Maintainability and testability

| Identifier | Title | Requirement | Rationale | Verification approach | Priority | Related capability or principle |
| --- | --- | --- | --- | --- | --- | --- |
| NFR-MAINT-001 | Independently testable scheduling rules | Availability, conflict, buffer, and task-placement rules shall be verifiable independently of conversational interpretation and live external services. | Deterministic scheduling is a source-of-truth responsibility. | Test-suite and design review | Must Have | FR-004–FR-006, FR-022–FR-026 |
| NFR-MAINT-002 | Controllable integration tests | Tests shall be able to exercise Google Calendar and AI-dependent behavior using controlled responses, including errors, delays, stale data, and ambiguous outcomes. | Safe failure behavior cannot depend on provoking live providers. | Test-harness review and automated tests | Must Have | NFR-REL-001–NFR-REL-004, NFR-RES-001–NFR-RES-004 |
| NFR-MAINT-003 | Consequential-workflow coverage | Automated tests shall cover proposal creation, confirmation, rejection, revalidation, duplicate prevention, provider failure, and truthful outcome reporting for each supported calendar-write operation. | Calendar writes carry the highest V1 consequence. | Coverage review and automated workflow tests | Must Have | FR-042–FR-050 |
| NFR-MAINT-004 | Requirements traceability | Approved user journeys, functional requirements, non-functional requirements, and acceptance scenarios shall retain identifiable links where they materially depend on one another. | Traceability prevents safety behavior from disappearing during implementation. | Documentation review | Must Have | Phase 0 working agreement |
| NFR-MAINT-005 | Externalized environment configuration | Environment-specific configuration and secrets shall be supplied outside committed application source and documented for local and deployed operation. | Owner-controlled environments differ and secrets must remain protected. | Configuration inspection and setup review | Must Have | NFR-SEC-003 |
| NFR-MAINT-006 | Clear responsibility boundaries | Product rules, external-service interaction, personal-data handling, and user-facing orchestration shall have documented responsibilities that can be reviewed and tested separately. | Clear boundaries reduce accidental coupling without fixing an implementation architecture prematurely. | Architecture and testability review | Should Have | Tasks #7–#9, AI/deterministic boundary |

## Observability and supportability

| Identifier | Title | Requirement | Rationale | Verification approach | Priority | Related capability or principle |
| --- | --- | --- | --- | --- | --- | --- |
| NFR-OBS-001 | Privacy-conscious diagnostics | Diagnostic records shall contain enough event type, outcome, timing, and error context to investigate failures while excluding credentials and personal calendar, task, and conversation content by default. | Supportability must not create a second store of sensitive content. | Log review and failure-scenario tests | Must Have | NFR-SEC-004, NFR-PRIV-001 |
| NFR-OBS-002 | Proposal/action correlation | The system shall assign a non-sensitive correlation identifier that allows a calendar proposal, confirmation decision, execution attempt, and verified outcome to be associated during diagnosis. | Consequential actions need an auditable operational trail without logging full content. | Workflow and log-capture tests | Must Have | FR-042–FR-050 |
| NFR-OBS-003 | Dependency health visibility | The system shall provide the owner a current, understandable indication of whether required calendar and AI integrations are available, degraded, or unavailable. | The owner should know when answers may be incomplete. | Provider-state and usability tests | Should Have | FR-007, FR-033, NFR-RES-001–NFR-RES-003 |
| NFR-OBS-004 | Actionable internal errors | Diagnosable failures shall record an error category and correlation identifier without exposing sensitive values to the user or diagnostic output. | Failures need supportable context without leaking data. | Failure-injection and log review | Must Have | FR-049, NFR-OBS-001 |

## Compatibility and portability

| Identifier | Title | Requirement | Rationale | Verification approach | Priority | Related capability or principle |
| --- | --- | --- | --- | --- | --- | --- |
| NFR-PORT-001 | Required desktop browsers | All primary V1 journeys shall work correctly on the latest stable Google Chrome and latest stable Microsoft Edge. Pixel-identical rendering is not required. | These are the owner's required desktop browser baseline. | Cross-browser journey tests and compatibility review | Must Have | Journeys 1–7 |
| NFR-PORT-002 | Responsive browser access | Core V1 journeys should remain usable in a mobile browser viewport without requiring a native mobile application. | Mobile access may be useful while native apps remain deferred. | Responsive usability review | Should Have | V1 scope boundaries, Journeys 1–7 |
| NFR-PORT-003 | Reproducible Windows development | The project shall document a reproducible local development and verification workflow for the owner's Windows environment. | The initial owner must be able to understand and operate the project. | Clean-environment setup exercise | Must Have | Phase 1 handoff |
| NFR-PORT-004 | Hosting-provider independence | Core application behavior and owner data shall not require a single proprietary hosting vendor, and deployment prerequisites shall be documented. | Future owner-controlled deployment should not be blocked by avoidable vendor lock-in. | Deployment-documentation and portability review | Should Have | Private owner-controlled product direction |
| NFR-PORT-005 | Secondary desktop browsers | Primary V1 journeys should work correctly on the latest stable Firefox and latest stable Safari without requiring pixel-identical rendering. | Broader browser compatibility is valuable but not required for initial owner use. | Cross-browser journey tests and compatibility review | Should Have | Journeys 1–7 |

## Assumptions and constraints

- V1 serves one authenticated owner and does not define public signup, tenant isolation, organization roles, or large-scale concurrency targets.
- Google Calendar is authoritative for calendar commitments; locally stored tasks and explicit preferences remain owner-controlled application data.
- The AI provider may assist with language interpretation and explanations but is not authoritative for availability, validation, or calendar writes.
- External-provider latency and uptime cannot be guaranteed by DayPilot. V1 must communicate dependency status and fail safely.
- Formal compliance certification, multi-region operation, enterprise disaster recovery, and native mobile certification are outside V1.
- Performance verification uses up to 5,000 stored tasks, up to 1,000 events in the queried window, a maximum 90-day availability range, and up to 100 candidate tasks per planning operation. These are private V1 verification assumptions, not public-service capacity promises.

## Traceability summary

| Product concern | Primary NFR categories | Related functional areas or principles |
| --- | --- | --- |
| Protect personal data and credentials | Security, Privacy, Observability | FR-001–FR-017, FR-029–FR-040 |
| Preserve calendar and task truth | Reliability, Resilience, Time correctness | FR-001–FR-017, FR-042–FR-050 |
| Keep the user in control | Security, Usability, Reliability | “DayPilot assists; the user decides,” FR-041–FR-050 |
| Produce trustworthy planning results | Reliability, Performance, Time correctness, Maintainability | FR-004–FR-006, FR-018–FR-028 |
| Explain limits and recover from dependencies | Resilience, Usability, Observability | FR-007, FR-030–FR-035, FR-049 |
| Keep V1 understandable and operable by its owner | Maintainability, Compatibility, Observability | Phase 0 working agreement and private owner-controlled direction |

## Intentionally excluded requirements

- Public SaaS uptime, tenant isolation, organization administration, subscription billing, and large-scale concurrency
- Multi-region deployment and enterprise disaster-recovery objectives
- Formal legal or industry compliance certification
- Native mobile application certification
- Email, voice, smart-home, or broad third-party integration quality requirements
- Complex AI-memory or multi-agent infrastructure
- Productivity scoring or employee-monitoring controls
- A large monitoring or analytics platform

## Approved V1 calibration decisions

- Conversation history may persist across sessions for 30 days by default and remains individually and collectively deletable. It is contextual, not authoritative state.
- Local task operations target 1 second at the 95th percentile. Local availability and planning calculations target 2 seconds at the 95th percentile under the documented representative V1 volumes. External-provider latency is excluded, with visible waiting feedback required.
- Latest stable Chrome and Edge are required. Latest stable Firefox, Safari, and responsive mobile-browser access are `Should Have`.
- Verified backup and restore is required before V1 is ready for regular personal use, though it need not be delivered in the earliest foundation milestone.
