# DayPilot AI Product Brief

## Status

Tasks 1–2 complete — product problem, target user, V1 goals, and success criteria defined.

## Product problem

Busy professionals may already record commitments in Google Calendar, yet the information needed to organize their day remains divided among calendar events, tasks, priorities, and things they are holding in their head. They must repeatedly combine this information themselves to understand:

- what they need to do today;
- what is coming up;
- when they are actually free;
- where a new task can fit;
- whether a new commitment creates a conflict; and
- what they should work on next.

The core problem is the mental effort required to continuously coordinate commitments, tasks, priorities, and available time. Forgetting a calendar event or agreeing to a conflicting plan is one possible symptom, not the complete problem.

For example, the initial user forgot about an event planned by their family and discussed a different plan with neighbors. The event may have existed in the calendar, but it was not incorporated into a readily accessible view of the day when the new plan was discussed.

## Primary V1 target user

The primary V1 target user is:

> A busy professional who manages a mix of work, personal, and family commitments and already uses Google Calendar, but still relies on memory and manual planning to organize the day.

DayPilot AI is intended eventually to help other people with this same need. However, the project's creator is the first real user, and V1 will prioritize solving this problem well for one user before attempting to generalize for a broad audience.

## Current alternative and its limitation

The current tool is Google Calendar. It can store scheduled commitments, but a calendar alone does not combine those commitments with unscheduled tasks, priorities, information remembered by the user, and the reasoning needed to use available time.

The gap is therefore not simply calendar entry or event reminders. It is the manual coordination required to turn several sources of information into an actionable understanding of the day.

## Desired outcome

At the problem-framing level, the desired outcome is that the user can understand and navigate the day without repeatedly reconstructing the plan mentally. The user should be able to form a clear picture of commitments, responsibilities, priorities, and available time, reducing avoidable conflicts and uncertainty about what to do next.

The specific capabilities and success criteria that constitute a “perfectly planned day” will be defined in Task 2.

## Task 1 decisions

- The initial user is also the first real user of V1.
- The broader target is busy professionals balancing work, personal, and family commitments.
- The target user already uses Google Calendar but continues to rely on memory and manual planning.
- The core problem is cognitive coordination across calendar commitments, tasks, priorities, and available time.
- Forgetting or conflicting with an event is a symptom of that broader problem.
- V1 should first solve the problem well for one user; broader generalization is not the initial optimization target.

## V1 goals

### Goal 1: Provide clear daily orientation

At the beginning of the day, the user can understand the day without manually reconciling calendar events and tasks.

The user should be able to identify:

- today's existing commitments;
- important tasks that need attention;
- which commitments are fixed;
- where time remains available;
- anything needing immediate attention; and
- a reasonable plan for the day.

The intended outcome is that the user starts the day knowing what needs to happen and where flexibility remains.

### Goal 2: Capture tasks and make them schedulable

The user can describe a task naturally, including information such as its deadline and estimated duration. DayPilot retains the task so that it no longer depends on the user's memory and helps the user understand where it could realistically fit before its deadline.

A task does not have to be placed on the calendar immediately to be useful. DayPilot must be able to keep track of unscheduled work until it is appropriate to plan or complete it.

The intended outcome is that new tasks move out of the user's head, are less likely to be forgotten, and can be considered alongside actual availability.

### Goal 3: Support confident commitment decisions

Before accepting a proposed commitment, the user can ask whether a date or time window is available. DayPilot considers existing commitments, identifies conflicts, and, when appropriate, helps identify alternative available times.

The intended outcome is that the user can accept or reject proposed commitments confidently without manually searching the calendar or accidentally double-booking.

### Goal 4: Guide the user's next action

When the user is unsure what to do next, DayPilot provides reasonable guidance using:

- currently available time;
- incomplete tasks;
- deadlines;
- priority;
- estimated task duration; and
- existing calendar commitments.

For example, a 45-minute opening before the next commitment could be matched to an important task that can realistically fit within that window.

DayPilot provides guidance rather than taking control of the user's schedule. The intended outcome is less time spent deciding what to do and more time spent making progress.

### Goal 5: Preserve user control

DayPilot helps the user understand options and make decisions. It must not treat a recommendation or inferred intent as permission to change the user's schedule.

The intended outcome is that the user benefits from planning assistance while remaining in control of decisions that create or modify commitments.

## V1 success criteria

V1 is successful when regular real-world use over several weeks produces noticeable evidence that:

- the user forgets fewer commitments and tasks;
- the user creates fewer accidental scheduling conflicts;
- the user relies less on remembering tasks mentally;
- the user spends less time repeatedly checking the calendar;
- the user can quickly determine availability when asked;
- the user starts most days with a clearer understanding of what needs to happen;
- the user has less uncertainty about what to work on during available time;
- tasks with deadlines are less likely to be rediscovered at the last minute; and
- the user trusts DayPilot's view of the day enough to use it regularly.

These are qualitative, user-observable criteria for V1. Formal product analytics, productivity scoring, or claims of measured productivity improvement are not required.

## Overall V1 success statement

> DayPilot should reduce the mental effort required to coordinate the user's calendar, tasks, priorities, and available time while keeping the user in control of decisions that change the schedule.

## Task 2 decisions

- V1 success is defined by improved day-to-day outcomes, not merely by delivering integrations or screens.
- V1 covers daily orientation, durable task capture, availability and conflict checks, context-aware next-action guidance, and user control.
- Tasks may remain unscheduled while still being tracked and considered in planning.
- Recommendations should consider time, task status, deadlines, priority, duration, and calendar commitments.
- The first success evaluation will be qualitative and based on several weeks of real use.
- Formal analytics and productivity scoring are not V1 requirements.
