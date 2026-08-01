# DayPilot AI V1 User Journeys

## Status

Approved — Phase 0 Task #4 complete.

## Purpose

These journeys describe how the V1 user experiences DayPilot while pursuing everyday planning goals. They connect a real situation to an observable outcome and identify the points where DayPilot assists and the user decides.

User journeys are not functional requirements. A journey tells the end-to-end story of a user's goal, including alternatives and decisions; a functional requirement will later state precise, testable behavior derived from an approved journey. These journeys intentionally avoid prescribing interfaces or technical implementation.

Later Phase 0 tasks will use the approved journeys to define functional requirements, system boundaries, domain responsibilities, and representative architecture flows. Later implementation phases will use them to identify incremental product slices and acceptance scenarios.

## Shared journey principles

- **DayPilot assists; the user decides.** Recommendations and proposals do not replace user judgment.
- Google Calendar is the source of truth for calendar commitments.
- DayPilot tasks supplement calendar commitments; an unscheduled task is not automatically a calendar event.
- DayPilot explains the relevant constraints and reasoning behind a recommendation.
- The user may accept, reject, or revise a suggestion.
- Consequential actions require confirmation, especially actions that change calendar events, commit the user's time, communicate externally, or affect other people.
- When important information is ambiguous or missing, DayPilot asks rather than silently making a consequential assumption.

## Journey 1: Understand my day

### Goal

Start the day with a clear understanding of commitments, important tasks, available time, immediate concerns, and flexibility without mentally combining separate sources.

### Trigger

The user begins the day or asks DayPilot for today's plan.

### Preconditions

- The user has connected the Google account whose visible calendars should inform planning.
- DayPilot has access to the user's current tasks and explicit planning preferences.

### Information DayPilot considers

- today's calendar commitments and their times;
- incomplete tasks, deadlines, priorities, and estimated durations when known;
- available time between commitments;
- explicit working hours, buffers, and other planning preferences; and
- overdue or time-sensitive items that may need attention.

### Primary flow

1. The user asks to understand or plan the day.
2. DayPilot reviews today's commitments, relevant tasks, and available time.
3. DayPilot presents a concise view of fixed commitments, important work, open time, and anything requiring immediate attention.
4. DayPilot proposes a reasonable plan that fits around existing commitments and explains the most important choices or constraints.
5. The user reviews the plan and decides whether to follow it, adjust priorities, or request alternatives.

### Alternative flows

- **No commitments:** DayPilot makes clear that the day is calendar-free and uses tasks and preferences to suggest a flexible plan.
- **No tasks:** DayPilot presents commitments and free time without inventing work.
- **Overcommitted day:** DayPilot explains that everything may not fit and highlights tradeoffs rather than presenting an unrealistic plan.
- **Missing task details:** DayPilot distinguishes known facts from assumptions and may ask for a deadline, priority, or duration when the answer would materially improve the plan.
- **Calendar information unavailable:** DayPilot states that it cannot provide a trustworthy complete-day view and avoids presenting availability as certain.

### User control

The plan is guidance. The user chooses priorities and whether to follow or revise it. Merely presenting the plan does not create, move, or delete calendar events.

### Success outcome

The user can quickly explain what must happen today, where flexibility exists, and what deserves attention first.

## Journey 2: Capture a new task

### Goal

Move a task out of memory into a trusted place where it can be reviewed and considered during planning.

### Trigger

The user remembers something to do or receives a new responsibility, such as “Renew passport” or “Finish the presentation by Thursday.”

### Preconditions

The user can identify at least the task itself. A deadline, priority, and duration may be unknown.

### Information DayPilot considers

- the user's description of the task;
- an explicitly stated deadline, duration, or priority;
- ambiguities that would change what is captured; and
- existing tasks that appear to be the same responsibility.

### Primary flow

1. The user describes the task naturally.
2. DayPilot identifies the task and any details the user supplied.
3. DayPilot asks for clarification only when ambiguity would risk capturing the wrong responsibility; otherwise, it preserves the task with the information currently known.
4. DayPilot confirms what it retained and clearly identifies important details that remain unspecified.
5. The task becomes available for later review, scheduling suggestions, and daily planning.

### Alternative flows

- **No deadline:** DayPilot keeps the task without inventing one and may offer to add a deadline later.
- **No estimated duration:** DayPilot keeps the task but explains that scheduling recommendations may remain less precise until duration is known.
- **Ambiguous description:** DayPilot asks the user to clarify the intended outcome or scope.
- **Possible duplicate:** DayPilot points out the existing task and lets the user decide whether to reuse it or create another.
- **User wants immediate scheduling:** After capturing the task, the interaction may continue into Journey 4.

### User control

The user determines the task's meaning, deadline, priority, and duration. Capturing a task does not automatically reserve calendar time.

### Success outcome

The user trusts that the responsibility no longer depends on memory and can find it in future planning conversations.

## Journey 3: Check availability before accepting a commitment

### Goal

Determine confidently whether a proposed time is available before agreeing to a new commitment.

### Trigger

Someone proposes a time, or the user asks a question such as “Am I free Tuesday afternoon?”

### Preconditions

- The requested date or time range can be identified or clarified.
- Current Google Calendar information is available.

### Information DayPilot considers

- calendar commitments during the requested period;
- the user's time zone and meaning of broad expressions such as “afternoon”;
- relevant buffers or availability preferences; and
- the difference between calendar availability and unscheduled task workload.

### Primary flow

1. The user asks whether a proposed period is available.
2. DayPilot interprets the requested period and asks for clarification if it is materially ambiguous.
3. DayPilot checks existing commitments and applicable buffers.
4. DayPilot states whether the period is free, partially free, or conflicting and explains the relevant constraint.
5. When the requested period does not work, DayPilot may identify reasonable alternatives.
6. The user decides whether to accept, reject, or renegotiate the proposed commitment.

### Alternative flows

- **Partially available:** DayPilot identifies the actual free portion rather than describing the entire period as free.
- **Conflict exists:** DayPilot identifies the conflict without exposing irrelevant event details.
- **No suitable alternative:** DayPilot says so instead of forcing a recommendation.
- **Calendar information unavailable or stale:** DayPilot states that availability cannot be confirmed reliably.
- **Tasks compete for the time:** DayPilot distinguishes “no calendar conflict” from “no other planned work” so the user can make an informed decision.

### User control

DayPilot reports availability and alternatives; the user decides whether to make the commitment. Checking availability alone never creates a calendar event.

### Success outcome

The user can respond to the proposal without manually searching the calendar and with a lower risk of accidental double-booking.

## Journey 4: Fit a task into the schedule

### Goal

Find realistic opportunities to work on a task before its deadline without conflicting with existing commitments.

### Trigger

The user asks where a task can fit, for example, “Find two hours this week for FamilyPlate.”

### Preconditions

- The task is known or can be captured during the interaction.
- The necessary duration and scheduling horizon are known or can be clarified.
- Current calendar commitments are available.

### Information DayPilot considers

- task duration, deadline, priority, and whether work may be split;
- calendar commitments and available intervals;
- explicit working-time preferences and buffers; and
- other important tasks competing for the same time.

### Primary flow

1. The user identifies the task and asks for scheduling help.
2. DayPilot confirms the duration, deadline or search range, and any constraint that materially affects the result.
3. DayPilot identifies realistic openings using current commitments and explicit preferences.
4. DayPilot proposes one or more suitable options and explains relevant tradeoffs.
5. The user selects an option, requests alternatives, changes a constraint, or declines to schedule it.
6. If the user chooses to reserve calendar time, DayPilot presents the exact proposed calendar change for confirmation before carrying it out.

### Alternative flows

- **No suitable time before the deadline:** DayPilot explains the shortfall and presents user-controlled options such as splitting the work, changing the search period, or revisiting another constraint. It does not silently move commitments, extend the deadline, or alter assumptions.
- **Task cannot be split:** DayPilot limits suggestions to continuous openings of sufficient length.
- **Deadline or duration missing:** DayPilot asks for the information needed to make a realistic recommendation.
- **Several equally suitable openings:** DayPilot presents a small set of understandable options rather than choosing silently.
- **Calendar changes before confirmation:** DayPilot rechecks the proposal and reports the changed constraint instead of applying an outdated choice.

### User control

The user decides whether the task should be scheduled, whether it may be split, and which option to choose. Calendar time is reserved only after explicit confirmation of the proposed change.

### Success outcome

The user identifies a credible way to complete the task within the relevant period, or learns clearly why it does not currently fit.

## Journey 5: Decide what to work on next

### Goal

Use an available block of time effectively without repeatedly reviewing every task and commitment.

### Trigger

The user has time available and asks what would be reasonable to work on next.

### Preconditions

- DayPilot can identify the current time window before the next relevant commitment.
- The user has at least one incomplete task, or DayPilot can truthfully report that none is suitable.

### Information DayPilot considers

- the actual time available and relevant buffers;
- incomplete tasks, deadlines, priority, and estimated duration;
- existing calendar commitments; and
- explicit user preferences or constraints.

### Primary flow

1. The user asks what to do next or identifies an available period.
2. DayPilot determines the usable time and reviews relevant incomplete tasks.
3. DayPilot recommends a task that can reasonably fit and explains why it is a good option.
4. DayPilot may mention a small number of alternatives when meaningful tradeoffs exist.
5. The user chooses what to work on, asks for another suggestion, or decides to use the time differently.

### Alternative flows

- **Nothing fits:** DayPilot says that no known task fits reliably and may suggest using a shorter action only when one is already known.
- **Task durations are unknown:** DayPilot communicates lower confidence or asks the user to estimate duration.
- **Several urgent tasks compete:** DayPilot explains the deadline or priority tradeoff and leaves the choice to the user.
- **User rejects the recommendation:** DayPilot offers another suitable option without treating the rejection as an error.
- **Available time changes:** DayPilot updates its guidance using the new constraint.

### User control

The recommendation is optional. DayPilot does not change task priority or reserve time merely because it recommended something.

### Success outcome

The user spends less time deciding and can begin a suitable task with confidence that it fits the available window.

## Journey 6: Propose and confirm a calendar change

### Goal

Safely change an existing calendar commitment while understanding the exact effect and any conflicts before approval.

### Trigger

The user requests a change such as “Move my meeting to tomorrow.”

### Preconditions

- The intended calendar event can be identified or clarified.
- DayPilot can access current calendar information.
- The requested change can be made specific enough for the user to review.

### Information DayPilot considers

- the event the user intends to change;
- the proposed date, time, duration, and time zone;
- conflicts and relevant buffers;
- whether the event affects or involves other people; and
- any calendar change since the request began.

### Primary flow

1. The user asks DayPilot to change an event.
2. DayPilot clarifies which event and what new date or time the user means when necessary.
3. DayPilot checks the proposed change against current calendar commitments.
4. DayPilot presents the existing event, exact proposed change, conflicts or consequences, and any relevant alternatives.
5. DayPilot asks the user to confirm the specific proposal.
6. The user confirms, rejects, or revises it.
7. Only after confirmation, DayPilot carries out the approved change and reports the result.

### Alternative flows

- **Ambiguous event or time:** DayPilot asks a focused question and makes no change.
- **Conflict at the requested time:** DayPilot explains the conflict and may propose alternatives; it does not override the conflict silently.
- **Event affects other people:** DayPilot makes that consequence visible before confirmation.
- **Calendar changed before approval:** DayPilot invalidates or refreshes the proposal and asks the user to review the current version.
- **User rejects or revises:** No change occurs; DayPilot may prepare a new proposal if requested.
- **Approved change cannot be completed:** DayPilot reports the failure clearly and does not claim the calendar was updated.

### User control

The user explicitly approves the exact calendar change. An initial request, interpreted intent, or approval of a different proposal is not sufficient authorization.

### Success outcome

The calendar reflects only the change the user reviewed and approved, or remains unchanged with a clear explanation when the proposal was rejected or could not be completed.

## Journey 7: Review the day and prepare for tomorrow

### Goal

End the day with a clear understanding of what was completed, what remains unresolved, and what needs attention tomorrow.

### Trigger

The user asks for an end-of-day review or begins planning the following day.

### Preconditions

DayPilot has the current state of the user's tasks and calendar commitments.

### Information DayPilot considers

- tasks the user has marked complete;
- incomplete, overdue, or approaching-deadline tasks;
- today's past commitments and tomorrow's upcoming commitments;
- previously proposed plans as context, without assuming that a suggestion proves work was completed; and
- known available time and explicit preferences for tomorrow.

### Primary flow

1. The user asks to review the day.
2. DayPilot summarizes known completed work and distinguishes it from work whose status is unknown.
3. DayPilot identifies unfinished or time-sensitive tasks that may need attention.
4. DayPilot previews tomorrow's important commitments and likely constraints.
5. DayPilot suggests what the user may want to carry forward or consider tomorrow.
6. The user confirms task status, adjusts priorities, or asks to plan a specific item.

### Alternative flows

- **Completion status unknown:** DayPilot asks rather than assuming that planned work was completed.
- **Unfinished work no longer matters:** The user may complete, revise, or remove the task instead of carrying it forward.
- **Tomorrow is overcommitted:** DayPilot highlights the constraint and tradeoffs without automatically reorganizing the schedule.
- **No unfinished tasks:** DayPilot provides a concise review and tomorrow preview without inventing concerns.
- **Calendar information unavailable:** DayPilot limits the review to known task information and states what it could not verify.

### User control

The user confirms what was completed, what remains important, and what should carry forward. DayPilot does not infer completion from elapsed time or automatically reschedule unfinished work.

### Success outcome

The user ends the day knowing what remains open and begins the next day with fewer surprises and less mental carryover.

## Approved journey assumptions

1. V1 includes an explicit end-of-day review as a user-initiated journey, not an automatically triggered workflow.
2. A minimally described task may be retained without a deadline, duration, or priority; DayPilot asks for those details when they materially affect later guidance.
3. “Free” primarily means no calendar conflict after applicable buffers. DayPilot should separately disclose known task workload rather than representing unscheduled tasks as calendar conflicts.
4. A calendar-change proposal is refreshed when relevant calendar state changes before confirmation.
5. DayPilot does not infer task completion merely because time was planned or elapsed; the user remains the authority on completion.

These assumptions were approved with the seven journeys as part of Task #4.
