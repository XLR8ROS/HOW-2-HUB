# SEAD TECHNICAL REVIEW HOW-TO

## Timestamp
20260411 164903 EDT

## Purpose
This how-to defines how SEAD should review substantial engineering work before treating it as settled.

## When to review
Review substantial work before treating it as settled.

Examples include:

1. architecture decisions
2. technical plans
3. repo structures
4. implementation specs
5. durable technical notes
6. tool choices
7. major refactors

## What the review should check
A technical review should check for:

1. ambiguity
2. structural weakness
3. missing dependencies
4. hidden assumptions
5. avoidable future friction
6. implementation mismatch
7. incomplete done-state definition

## Review questions
Use these questions:

1. Is the output clear?
2. Is the structure sound?
3. Are dependencies named?
4. Are assumptions separated from settled facts?
5. Will this make later work easier or harder?
6. Does the done-state make sense?

## Review outcome
A review should end in one of these states:

1. accepted
2. revise
3. blocked
4. deferred

## Review record
When useful, record:

1. what was reviewed
2. what was found
3. what changed
4. what still remains open