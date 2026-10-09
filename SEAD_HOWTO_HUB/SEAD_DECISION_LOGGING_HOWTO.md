# SEAD DECISION LOGGING HOW-TO

## Timestamp
20260411 164903 EDT

## Purpose
This how-to defines how SEAD should log important engineering decisions.

It exists so important technical decisions do not get lost in conversation.

## What should be logged
Log a decision when it affects:

1. architecture
2. repo structure
3. implementation order
4. dependency structure
5. engineering procedure
6. future engineering work
7. routing or model use
8. tool adoption
9. memory structure
10. deployment shape

## What a decision log entry should answer
A decision log entry should answer:

1. what was decided
2. why it was decided
3. what authority or source supports it
4. what changes because of it
5. what happens next

## Good decision log shape
A decision log can be brief.

Use this shape:

1. Decision
2. Rationale
3. Authority or source
4. Impact
5. Next action

## Logging rule
Log the decision soon enough that later work does not depend on memory alone.

## Placement rule
Decision logs should go in the approved durable location for that repo or workstream.

Do not leave important engineering decisions only inside transient conversation.