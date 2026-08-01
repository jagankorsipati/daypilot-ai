# DayPilot AI V1 Functional Requirements

## Status

Approved — Phase 0 Task #5 complete.

## Purpose and scope

These requirements define the observable product capabilities needed to support the seven approved V1 user journeys. They state what DayPilot must do without prescribing technical design.

Priority meanings:

- **Must Have:** Required for the approved V1 journeys to work safely and coherently.
- **Should Have:** Valuable V1 behavior that improves an approved journey but is not essential to its basic outcome.
- **Could Have:** Optional if time permits. No requirements currently carry this priority because optional ideas belong outside the committed V1 boundary until justified.

Tasks represent intentions or work to be done. Calendar events represent time commitments. Requirements preserve that distinction.

## Calendar

| Identifier | Title | Description | Related user journey(s) | Priority | Notes |
| --- | --- | --- | --- | --- | --- |
| FR-001 | View today's commitments | The system shall provide the user's current calendar commitments for today, including enough date and time information to understand when each commitment occurs. | Journey 1 | Must Have | Google Calendar remains the calendar source of truth. |
| FR-002 | View commitments for a requested period | The system shall provide current calendar commitments for a user-requested date or time range. | Journeys 3, 4, 6, 7 | Must Have | Includes future dates needed for availability and planning. |
| FR-003 | Respect the user's time context | The system shall interpret and present calendar dates and times using the user's explicit time-zone context and shall seek clarification when the intended time context is materially ambiguous. | Journeys 1, 3, 4, 6, 7 | Must Have | The system must not silently choose between materially different times. |
| FR-004 | Identify scheduling conflicts | The system shall identify calendar commitments that overlap a proposed date and time interval. | Journeys 3, 4, 6 | Must Have | A conflict result must identify the relevant occupied interval. |
| FR-005 | Determine available intervals | The system shall determine available intervals within a requested period after accounting for calendar commitments and applicable explicit buffers. | Journeys 1, 3, 4, 5 | Must Have | Availability is determined by product rules, not guessed from conversational output. |
| FR-006 | Distinguish availability from workload | The system shall distinguish an interval with no calendar conflict from an interval that may still compete with known unscheduled tasks. | Journeys 1, 3, 4, 5 | Must Have | An unscheduled task is not represented as a calendar commitment. |
| FR-007 | Report unavailable calendar information | The system shall disclose when calendar information needed for an answer is unavailable or cannot be verified and shall not present the affected answer as certain. | Journeys 1, 3, 4, 6, 7 | Must Have | Applies to daily views, availability, proposals, and reviews. |
| FR-008 | Offer alternative available times | When a requested period conflicts or is insufficient, the system should identify suitable alternative intervals when such intervals exist within the user's stated constraints. | Journeys 3, 4, 6 | Should Have | The system must state when no suitable alternative is found. |
| FR-050 | Create confirmed calendar time | The system shall create a new calendar event or reserve a time block for a task only after the user confirms the exact proposed date, time, and duration. | Journey 4 | Must Have | V1 creation is limited to the confirmed time commitment needed by the approved journey. |

## Tasks

| Identifier | Title | Description | Related user journey(s) | Priority | Notes |
| --- | --- | --- | --- | --- | --- |
| FR-009 | Capture a task | The system shall retain a task described by the user so the task can be found and considered in later planning. | Journey 2 | Must Have | Capturing a task does not create calendar time. |
| FR-010 | Retain optional task details | The system shall allow a task to have an optional deadline, estimated duration, and priority and shall preserve any of those details supplied by the user. | Journeys 1, 2, 4, 5, 7 | Must Have | A task remains valid when one or more optional details are absent. |
| FR-011 | Identify unspecified task details | After capture or review, the system shall distinguish task details supplied by the user from deadline, duration, or priority details that remain unspecified. | Journeys 1, 2, 4, 5 | Must Have | The system shall not invent missing values. |
| FR-012 | View incomplete tasks | The system shall provide incomplete tasks relevant to a daily plan, requested planning period, or user review. | Journeys 1, 4, 5, 7 | Must Have | Relevance may use explicit deadlines, priorities, and requested periods. |
| FR-013 | Edit a task | The system shall allow the user to revise a task's description, deadline, estimated duration, priority, and completion status. | Journeys 2, 4, 5, 7 | Must Have | User-supplied changes replace earlier task information only after the intended task is clear. |
| FR-014 | Remove a task | The system shall allow the user to remove a task that is no longer relevant after identifying the intended task. | Journeys 2, 7 | Must Have | Removing a task shall not silently delete a calendar commitment. |
| FR-015 | Record task completion | The system shall allow the user to mark a task complete and shall preserve that status for later planning and review. | Journeys 5, 7 | Must Have | Completion is based on user action, not elapsed time. |
| FR-016 | Correct task completion | The system shall allow the user to return a completed task to incomplete status when correcting or reopening it. | Journey 7 | Must Have | Supports correction without recreating the task. |
| FR-017 | Flag a possible duplicate task | When a newly described task appears to duplicate an existing task, the system should identify the possible duplicate and let the user choose whether to reuse it or create another. | Journey 2 | Should Have | Similarity alone shall not prevent task capture. |

## Daily planning

| Identifier | Title | Description | Related user journey(s) | Priority | Notes |
| --- | --- | --- | --- | --- | --- |
| FR-018 | Generate a daily overview | The system shall produce an overview that combines today's commitments, relevant incomplete tasks, available time, and items needing immediate attention. | Journey 1 | Must Have | The overview must keep tasks distinct from commitments. |
| FR-019 | Identify fixed commitments and flexibility | The system shall distinguish existing calendar commitments from intervals where the user's day remains flexible. | Journey 1 | Must Have | This distinction helps the user understand what can still change. |
| FR-020 | Propose a reasonable daily plan | The system shall propose an ordered, achievable plan around existing commitments using known tasks and explicit preferences. | Journey 1 | Must Have | The proposal is guidance and does not itself reserve time. |
| FR-021 | Expose an overcommitted day | When known commitments and candidate work cannot all fit within the relevant time, the system shall explain the shortfall and the principal tradeoffs rather than present an infeasible plan. | Journeys 1, 4, 7 | Must Have | The user decides what to defer or reprioritize. |
| FR-022 | Suggest task placement | The system shall identify intervals in which a task can fit before its deadline or within a user-requested planning horizon. | Journey 4 | Must Have | Suggestions use duration and applicable scheduling constraints. |
| FR-023 | Respect task splitting constraints | The system shall ask whether work may be split when that choice materially affects placement and shall not split a task the user has said must remain continuous. | Journey 4 | Must Have | A split proposal must make each interval clear. |
| FR-024 | Explain why a task does not fit | When no interval satisfies the task's known constraints, the system shall identify the unmet constraint and may present user-controlled options such as changing the period or allowing a split. | Journey 4 | Must Have | The system does not alter constraints automatically. |
| FR-025 | Recommend what to work on next | The system shall recommend a known incomplete task that can reasonably fit within the user's available time using deadline, priority, and estimated duration when available. | Journey 5 | Must Have | If confidence is reduced by missing information, that limitation must be disclosed. |
| FR-026 | Report when no suitable task is known | When no known incomplete task reliably fits the available interval, the system shall say so rather than invent work or claim a poor fit is suitable. | Journey 5 | Must Have | The user may still choose how to use the time. |
| FR-027 | Prepare an end-of-day review | On user request, the system shall summarize known completed tasks, unresolved or time-sensitive tasks, and the next day's important calendar commitments. | Journey 7 | Must Have | The review is user-initiated in V1. |
| FR-028 | Distinguish planned work from completed work | The system shall distinguish work that was suggested or planned from work the user has confirmed complete. | Journey 7 | Must Have | A past planned interval is not proof of completion. |

## Assistant interaction

| Identifier | Title | Description | Related user journey(s) | Priority | Notes |
| --- | --- | --- | --- | --- | --- |
| FR-029 | Interpret supported natural-language requests | The system shall accept natural-language requests for the seven approved journey goals and identify the user's requested goal and explicitly supplied details. | Journeys 1–7 | Must Have | Natural language does not imply support for capabilities outside these journeys. |
| FR-030 | Handle incomplete or uncertain information | The system shall communicate when a request or recommendation depends on missing, ambiguous, stale, or incomplete information and shall request clarification when needed before proposing or carrying out a consequential action. | Journeys 1–7 | Must Have | Examples include unclear dates or durations, multiple matching events, incomplete task details, changed calendar state, and several reasonable interpretations. Safe partial input may still be preserved under FR-031. |
| FR-031 | Preserve non-consequential partial input | When a task can be captured safely with missing optional details, the system shall retain the known information instead of requiring unnecessary answers. | Journey 2 | Must Have | Deadline, duration, and priority may be added later. |
| FR-032 | Explain recommendations | When the user requests an explanation, the system shall provide a concise, user-facing account of the primary known inputs and rules supporting a planning or scheduling recommendation. | Journeys 1, 3, 4, 5, 6, 7 | Must Have | An explanation may reference uninterrupted time, deadlines, priority, duration, commitments, or explicit preferences. It shall not expose hidden model reasoning or internal chain-of-thought. |
| FR-033 | Communicate uncertainty and unsupported requests | The system shall state when information is uncertain or a requested capability is unsupported and shall not claim an action or conclusion it cannot substantiate. | Journeys 1–7 | Must Have | Unsupported requests must not be disguised as completed work. |
| FR-034 | Offer revisable proposals | The system shall allow the user to reject a proposal, request alternatives, or revise relevant constraints without treating rejection as an error. | Journeys 1, 3, 4, 5, 6, 7 | Must Have | A revised consequential proposal requires review on its own terms. |
| FR-035 | Confirm retained information and completed actions | The system shall report what task information it retained and the verified outcome of an approved action. | Journeys 2, 6 | Must Have | A failed action must not be reported as successful. |

## Explicit preferences

| Identifier | Title | Description | Related user journey(s) | Priority | Notes |
| --- | --- | --- | --- | --- | --- |
| FR-036 | Manage working-hour preferences | The system shall allow the user to define, review, change, and remove the hours within which task placement may normally be suggested. | Journeys 1, 4, 5, 7 | Must Have | These are explicit preferences, not inferred habits. |
| FR-037 | Manage buffer preferences | The system shall allow the user to define, review, change, and remove time buffers used when evaluating availability or suggesting placement. | Journeys 1, 3, 4, 5, 6 | Must Have | Applied buffers must be reflected in explanations when relevant. |
| FR-038 | Manage scheduling preferences | The system shall allow the user to define, review, change, and remove explicit constraints that affect task placement, including whether a task may be split when specified for that task. | Journeys 1, 4, 5 | Must Have | Preferences do not override fixed commitments. |
| FR-039 | Select calendars used for planning | The system shall allow the user to explicitly select which calendars already visible to the connected Google account are considered when planning and checking availability. | Journeys 1, 3, 4, 5, 6, 7 | Must Have | V1 does not manage calendar sharing. |
| FR-040 | Avoid implicit personal memory | The system shall use only current conversation context and explicit, reviewable user information for durable planning preferences. | Journeys 1–7 | Must Have | V1 does not silently build a long-term behavioral profile. |

## Safety and user control

| Identifier | Title | Description | Related user journey(s) | Priority | Notes |
| --- | --- | --- | --- | --- | --- |
| FR-041 | Separate suggestions from actions | The system shall present plans, availability results, and placement recommendations without treating them as authorization to modify tasks or calendar commitments. | Journeys 1, 3, 4, 5, 6, 7 | Must Have | DayPilot assists; the user decides. |
| FR-042 | Present an exact calendar-change proposal | Before a calendar modification, the system shall present the affected commitment, proposed change, relevant conflicts, and consequences in a form the user can review. | Journeys 4, 6 | Must Have | Reserving task time is also a calendar modification. |
| FR-043 | Require explicit confirmation for calendar changes | The system shall modify a calendar commitment only after the user explicitly confirms the current, specific proposal. | Journeys 4, 6 | Must Have | An initial request or confirmation of an earlier proposal is insufficient. |
| FR-044 | Preserve state after rejection | If the user rejects or does not confirm a proposed calendar change, the system shall leave the calendar unchanged. | Journeys 4, 6 | Must Have | The user may request a revised proposal. |
| FR-045 | Revalidate before calendar modification | Immediately before carrying out a confirmed calendar change, the system shall account for relevant calendar changes since the proposal was prepared and shall require renewed review if the proposal is no longer current. | Journeys 4, 6 | Must Have | Prevents an outdated proposal from being applied silently. |
| FR-046 | Disclose effects on other people | When a proposed calendar change may affect other people, the system shall make that consequence visible before requesting confirmation. | Journey 6 | Must Have | The user remains responsible for approving the effect. |
| FR-047 | Preserve user authority over priorities | The system shall allow the user to accept, reject, or override planning and priority recommendations and shall not change user-defined priorities without instruction. | Journeys 1, 4, 5, 7 | Must Have | Recommendations do not replace user judgment. |
| FR-048 | Never infer task completion | The system shall change a task to complete only in response to an explicit user decision and never solely because planned time elapsed or a calendar interval ended. | Journeys 5, 7 | Must Have | Reinforces the distinction between planning and completion. |
| FR-049 | Report action failure accurately | If an approved calendar modification cannot be completed, the system shall report the failure and shall not represent the calendar as changed. | Journey 6 | Must Have | The user may decide whether to retry or revise. |

## Journey traceability summary

| User journey | Primary requirement groups | Requirement identifiers |
| --- | --- | --- |
| Journey 1 — Understand my day | Calendar, Tasks, Daily planning, Assistant interaction, Explicit preferences, Safety and user control | FR-001, FR-003, FR-005–FR-007, FR-010–FR-012, FR-018–FR-021, FR-029, FR-030, FR-032–FR-034, FR-036–FR-041, FR-047 |
| Journey 2 — Capture a new task | Tasks, Assistant interaction, Explicit preferences | FR-009–FR-011, FR-013, FR-014, FR-017, FR-029–FR-031, FR-033, FR-035, FR-040 |
| Journey 3 — Check availability | Calendar, Assistant interaction, Explicit preferences, Safety and user control | FR-002–FR-008, FR-029, FR-030, FR-032–FR-034, FR-037, FR-039–FR-041 |
| Journey 4 — Fit a task into the schedule | Calendar, Tasks, Daily planning, Assistant interaction, Explicit preferences, Safety and user control | FR-002–FR-008, FR-010–FR-013, FR-021–FR-024, FR-029, FR-030, FR-032–FR-034, FR-036–FR-045, FR-047, FR-050 |
| Journey 5 — Decide what to work on next | Calendar, Tasks, Daily planning, Assistant interaction, Explicit preferences, Safety and user control | FR-005, FR-006, FR-010–FR-013, FR-015, FR-025, FR-026, FR-029, FR-030, FR-032–FR-034, FR-036–FR-041, FR-047, FR-048 |
| Journey 6 — Propose and confirm a calendar change | Calendar, Assistant interaction, Explicit preferences, Safety and user control | FR-002–FR-004, FR-007, FR-008, FR-029, FR-030, FR-032–FR-035, FR-037, FR-039–FR-046, FR-049 |
| Journey 7 — End-of-day review | Calendar, Tasks, Daily planning, Assistant interaction, Explicit preferences, Safety and user control | FR-002, FR-003, FR-007, FR-010, FR-012–FR-016, FR-021, FR-027–FR-030, FR-032–FR-034, FR-036, FR-039–FR-041, FR-047, FR-048 |

## Intentionally excluded requirements

- Calendar providers other than Google Calendar, email, voice, native mobile applications, third-party task platforms, family collaboration, and public SaaS capabilities remain deferred under the approved V1 boundaries.
- Autonomous schedule reorganization, unconfirmed calendar writes, implicit long-term AI memory, productivity scoring, employee monitoring, and silent ambiguity resolution remain outside the product direction.
- Calendar event deletion and arbitrary event-detail editing are deferred. V1 does not modify attendees, locations, descriptions, reminders, or unrelated event properties because the approved journeys require only event creation, task-time reservation, and moving or rescheduling an existing commitment.
- Automatic carryover or rescheduling of incomplete tasks is excluded; Journey 7 keeps that decision with the user.
- Automatic changes to a calendar work block after task completion or task deletion are excluded because no approved journey establishes that behavior.

## Approved calendar-modification boundary

V1 supports reading calendar events, determining free time, detecting conflicts, creating a new calendar event or time block, reserving time for a task, and moving or rescheduling an existing commitment.

V1 does not support deleting calendar events or arbitrarily editing event details, attendees, locations, descriptions, reminders, or unrelated event properties. These operations may be considered later but are not part of the approved V1 journeys.
