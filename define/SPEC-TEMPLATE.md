# Spec — [feature / change name]

> Internal working document. `define` does **not** publish this standalone — its content is
> embedded into the per-module spec-update tickets and drives the implementation tickets.
> Use `GLOSSARY.md` canonical terms throughout. No file paths or code snippets.

## Problem Statement

The problem the user is facing, from the user's perspective.

## Solution

The solution to the problem, from the user's perspective.

## User Stories

A long, numbered list. Each story:

1. As an [actor], I want [feature], so that [benefit].

Example:

1. As a mobile bank customer, I want to see the balance on my accounts, so that I can make
   better-informed decisions about my spending.

Cover every aspect of the change — be extensive.

## Implementation Decisions

The decisions this change locks in. May include:

- The modules that will be built or modified — this list drives the spec-update tickets.
- The interfaces of those modules that change.
- Technical clarifications from the developer.
- Architectural decisions, schema changes, API contracts, specific interactions.

Do NOT include file paths or code snippets — they go stale fast. *Exception:* a snippet from
a prototype that encodes a decision more precisely than prose can (state machine, reducer,
schema, type shape) — inline only the decision-rich part and note it came from a prototype.

## Testing Decisions

- What makes a good test here (test external behaviour, not implementation details).
- Which modules will be tested, and at which seams.
- Prior art — similar tests already in the codebase.

## Out of Scope

What this spec explicitly does not cover.

## Further Notes

Anything else worth recording about the change.
