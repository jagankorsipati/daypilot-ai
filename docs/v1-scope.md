# DayPilot AI V1 Scope Boundaries

## Status

Approved — Phase 0 Task #3 complete.

## Purpose

A **non-goal** is a capability or concern that DayPilot V1 deliberately will not attempt to deliver. Naming non-goals protects the core outcome from scope creep and prevents architecture work from quietly assuming capabilities that V1 does not need.

A V1 non-goal is not automatically a permanently rejected idea. This document uses two dispositions:

- **Deferred:** Potentially valuable after V1, but not required to prove V1's core value. Deferral does not promise that the capability will be built later.
- **Outside direction:** Inconsistent with the current product purpose or its user-control principles. Pursuing it would require an explicit change in product direction, not merely more implementation time.

The classifications below define the approved V1 boundary.

## Guiding product principle

> **DayPilot assists; the user decides.**

DayPilot recommends, explains, finds conflicts, proposes schedules, and uses explicit user preferences. It asks for confirmation before consequential actions. The user remains the final decision-maker, especially when an action changes calendar events, commits the user's time, communicates externally, or affects other people.

DayPilot is an assistant, not a fully autonomous agent.

## Product scope

### Replace Google Calendar or build a complete calendar interface — Deferred

DayPilot will use Google Calendar as the source of calendar commitments and add a planning and coordination layer above it. V1 may present the calendar information needed for its workflows, but it will not reproduce the full Google Calendar interface or all calendar-management features.

### Automatically reorganize the user's entire day — Outside direction

V1 will propose a reasonable daily plan and help the user adapt it. It will not continuously or unilaterally rearrange the whole day. That would conflict with the requirement that the user remain in control of schedule-changing decisions.

### Advanced recurring-routine automation — Deferred

Sophisticated habits, templates, automatic recurrence rules, and adaptive routine management would expand the scheduling model before the core event-and-task coordination workflow has been validated.

### Location-aware, travel-time, or traffic-aware planning — Deferred

These capabilities require location data, travel modeling, additional providers, and new privacy decisions. V1 will base availability on calendar commitments, working preferences, buffers, and task duration rather than physical travel conditions.

### Productivity scoring or employee monitoring — Outside direction

DayPilot is a personal planning assistant, not a system for rating productivity or observing employees. V1 will not assign performance scores, rank the user, or provide surveillance capabilities.

### Formal analytics dashboards — Deferred

V1 success will be evaluated through regular real-world use. Building metrics pipelines and dashboards would not directly validate whether DayPilot reduces the user's planning effort.

## Integrations

### Calendar providers other than Google Calendar — Deferred

V1 will support Google Calendar only. Supporting additional providers would multiply authentication, calendar semantics, testing, and synchronization work before the main workflow is proven.

### Broader shared-calendar collaboration — Deferred

V1 may read calendars already visible to the connected Google account when the required Google permissions allow it. It will not manage sharing, invite other DayPilot users, coordinate several users' preferences, or provide family/team collaboration workflows.

### Gmail or general email integration — Deferred

V1 will not read, classify, draft, or send email. Email introduces additional sensitive data, permissions, intent interpretation, and communication risks that are not necessary for calendar-and-task coordination.

### Phone calls, appointment booking, or communication with external businesses — Deferred

V1 will not contact people or businesses, negotiate appointments, or make calls on the user's behalf. Later versions may help prepare appointment details, identify suitable times, or integrate with online booking systems for services such as dental visits, haircuts, or restaurants. DayPilot must not become a call center or communicate externally without explicit user authorization.

### Contacts integration — Deferred

Contact data is unnecessary for proving personal day planning and would add another sensitive data source and permission boundary.

### Smart-home integrations — Outside direction

Controlling devices and home automations does not support the defined problem of coordinating commitments, tasks, priorities, and available time.

### Broad third-party task-platform integrations — Deferred

V1 will use DayPilot's own personal task capability rather than synchronizing with many external task systems. Cross-provider semantics and synchronization would distract from validating the core task-and-calendar model.

## Automation and user control

### Fully autonomous scheduling — Outside direction

DayPilot will assist with planning and may prepare proposals, but it will not independently decide which commitments the user should accept or how the schedule should change.

### Calendar modifications without explicit user confirmation — Outside direction

Creating, moving, updating, or deleting a calendar event must follow a proposal-and-confirmation workflow. Natural-language input, a suggestion, or inferred intent alone is not authorization to write to the calendar.

### Automatically resolve ambiguity or conflicting instructions — Outside direction

When missing or contradictory information could materially change the result, DayPilot should explain the ambiguity and ask the user rather than silently choosing an interpretation.

### Replace user judgment about priorities or commitments — Outside direction

DayPilot can recommend what fits and what appears important, but the user decides priorities, accepts commitments, and approves schedule changes.

## Platforms and users

### Multi-user, family-account, or organization-account management — Deferred

V1 is optimized for one real user and one connected account. It will not include account hierarchies, household membership, organization administration, roles, or permissions for multiple users. Family and household coordination may be considered later for partner schedules, children's activities, reminders, travel, and other shared planning.

### Team collaboration and project management — Outside direction

DayPilot will not provide team workspaces, task assignment, project boards, status reporting, or managerial workflows. Its V1 task model supports an individual's daily planning.

### Native iOS or Android applications — Deferred

V1 will use a web client rather than maintaining separate native mobile applications. Mobile access may be reconsidered after the core workflow and usage patterns are understood.

### Voice interaction — Deferred

V1 will use text interaction. Speech recognition, speech output, device audio permissions, and voice-specific error handling are separate usability and privacy concerns.

## AI and memory

### Support every possible natural-language scheduling request — Outside direction

V1 will support a documented set of useful intents and must handle unsupported requests honestly. Open-ended language input does not imply unlimited backend capabilities.

### Guarantee that AI suggestions are always correct — Outside direction

Probabilistic model output cannot be guaranteed correct. DayPilot must instead constrain AI responsibilities, validate structured inputs, use deterministic services as the source of truth, communicate uncertainty, and preserve user review.

### Long-term implicit AI memory — Deferred

V1 will not silently accumulate an open-ended personal profile from conversations. Any durable preferences needed for deterministic planning should be explicit, inspectable application data with defined lifecycle rules.

### Vector databases or semantic memory systems — Deferred

V1 has no established retrieval or memory requirement that justifies this infrastructure. It should be introduced only if a later, reviewed use case cannot be served by simpler structured data.

### Complex multi-agent architecture — Deferred

V1 does not require autonomous agents delegating among themselves. A simpler application-service design with explicit tools and deterministic boundaries will be easier to understand, test, secure, and operate.

## Business and operations

### Billing and subscriptions — Deferred

V1 is intended to prove value for the initial user, not implement payment plans, entitlements, invoicing, or subscription lifecycle management.

### Public SaaS capabilities and multi-tenancy — Deferred

V1 is private, single-user, used first by the product owner, and self-hosted or deployed in infrastructure controlled by the product owner. It will not provide public signup, tenant isolation, organization administration, customer support tooling, or commercial-service operations. A public service may be considered only after demand is validated.

The implementation should avoid careless assumptions that make reasonable future expansion unnecessarily difficult. This does not justify building multi-user account management, multi-tenancy, SaaS administration, or external-communication infrastructure in V1. Build so future expansion remains possible; do not build SaaS capabilities before there is validated demand.

## V1 boundary summary

V1 remains focused on one user's coordination of Google Calendar commitments and personal tasks. It should provide daily orientation, retain tasks, calculate realistic availability deterministically, guide next actions, and offer conversational assistance. It may propose schedule changes, but the user must approve calendar writes.

V1 will not become a calendar replacement, general-purpose digital agent, communication proxy, collaboration suite, employee-monitoring product, or public multi-tenant SaaS platform. Capabilities classified as deferred remain possibilities, not roadmap commitments.
