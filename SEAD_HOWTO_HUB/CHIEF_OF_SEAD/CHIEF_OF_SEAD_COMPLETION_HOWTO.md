# CHIEF OF SEAD COMPLETION HOW-TO

## Timestamp
20260411 173900 EDT

## Purpose
This how-to defines how the Chief of SEAD should frame technical completion.

It exists to prevent vague claims of completion and keep done-state concrete.

## Core rule
A technical project, task, or deliverable is not complete unless the done-state is explicit.

## Completion rule
Completion must be stated in concrete operational terms.

Completion must not be stated as vague progress language.

## Acceptable completion framing
Good completion framing includes results such as:

1. architecture locked
2. schema finalized
3. migration path documented
4. routing policy defined
5. tests passing
6. risks documented and accepted
7. handoff package ready
8. repo placement locked
9. review notes resolved or explicitly accepted

## Unacceptable completion framing
Do not use completion claims such as:

1. made progress
2. mostly done
3. first pass complete
4. ready for next phase without explicit completion criteria
5. basically finished
6. should be good now

## Completion statement shape
Use this shape:

1. Deliverable or work item
2. Concrete done-state reached
3. What was verified
4. What remains open, if anything
5. Whether follow-on work exists

## Partial completion rule
If part of the work is done and part remains open, state that explicitly.

Do not blur partial completion into full completion.

## Good completion example
1. Deliverable: SQLite event log schema
2. Done-state: schema fields locked and attachments table defined
3. Verified: field list, timestamps, event numbering, attachment linkage
4. Open: final implementation location in repo
5. Follow-on: write implementation instructions

## Bad completion example
“The SQLite part is basically done.”
“Should be finished.”
“We’re good.”

No. We are not doing fortune-cookie completion language.