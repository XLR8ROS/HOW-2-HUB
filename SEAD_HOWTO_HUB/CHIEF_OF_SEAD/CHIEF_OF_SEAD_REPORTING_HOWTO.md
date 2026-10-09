# CHIEF OF SEAD REPORTING HOW-TO

## Timestamp
20260411 173900 EDT

## Purpose
This how-to defines how the Chief of SEAD should report upward during active work.

It exists to keep reporting concise, clear, and useful for decisions.

## Core rule
Reporting must be structurally clear and decision-useful.

Reporting is not narration for its own sake.

## When to report upward
Report upward when:

1. work has materially changed state
2. a blocker appears
3. a blocker clears
4. a decision is needed
5. a milestone is completed
6. timing risk becomes material
7. a dependency becomes due, at risk, or overdue
8. execution is continuing and a promised checkpoint is reached

## Required reporting contents
When reporting upward, include:

1. current state
2. current step
3. concrete progress
4. exact blocker, if any
5. blocker owner, if any
6. next action
7. whether execution continues or input is needed
8. next due checkpoint, if one exists

## Reporting shape (standard)
Use this shape **every time** unless you are explicitly told otherwise.

1. **Objective** (one line: what "done" means)
2. **State** (active | blocked | parked | done)
3. **Current step** (what you are doing right now)
4. **Progress since last update** (concrete facts, artifacts, numbers)
5. **Blocker** (exact issue) + **Owner** (who/what resolves it) + **Unblock condition** (what must be true)
6. **Next action** (what you will do next)
7. **Execution** (continuing | waiting for input)
8. **Next checkpoint** (when you will report next / what triggers the next report)

### Rules
- **No filler.** If you can’t name a concrete state change, say you’re waiting.
- **Name artifacts.** File paths, command outputs, counts, IDs—anything that makes the report verifiable.
- **If blocked:** you must include the unblock condition and the shortest path to clear it.
- **If done:** include what was verified and how.

## Concision rule
Keep reporting short unless complexity requires more detail.

## Anti-filler rule
Do not send updates with no meaningful state change unless a due checkpoint requires a status signal.

## Good reporting example
1. State: active
2. Current step: finalizing SQLite event log schema
3. Progress: schema cleaned to event-centered version with separate attachments table
4. Blocker: none
5. Next action: lock field names and write implementation notes
6. Execution: continuing
7. Next checkpoint: after schema lock

## Bad reporting example
“Still working on it.”
“Making progress.”
“Almost there.”

Worthless. That tells the receiver nothing actionable.