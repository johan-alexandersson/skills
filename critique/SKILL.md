---
name: critique
description: Critiques and deepen plans and software design, challenging it against existing design and documentation and sharpens terminology. Uses ARCHITECTURE.md, GLOSSARY.md and IDEA-TREE.md as ground truth. Produces DECISIONS.md and keeps ARCHITECTURE.md and GLOSSARY.md current. Use when designing or reviewing software architecture, planning features, or moving from ideation to implementation.
---

# Critique 

## What to do

Invoke with a design description, IDEA-TREE.md, architectural plan, or just "here's
what I want to build." A codebase does not need to exist yet.

Also invoked by `/pathfinder` as its critique task type — this is the idea tree's
"grilling." When dispatched that way, the question comes from the task's line in
IDEA-TREE.md, and the resulting DECISIONS.md entry (or resolved GLOSSARY.md term)
gets linked back there.

- Interview me relentlessly about every aspect of the plan.
- Explore the codebase or documentation to answer questions before asking.
- Ask one challenging question at a time, going deep before moving on. For each question, provide your recommended answer.
- Write DECISIONS.md entries when architectural decisions crystallize.

## Workflows

### Ground — before anything else
- If a codebase exists: read it first. Answer questions from code before asking the user.
- Ground truth priority: codebase → ARCHITECTURE.md → docs/specs → IDEA-TREE.md → stated goals.

### Map dependencies
- Before critiquing any component or feature: what does it depend on? What depends on it?
- Surface integration points, shared state, and sequencing constraints.
- Refer back to the dependency map when contradictions surface during critique.

### Critique — depth-first, one branch at a time
- Ask "why/how" to surface hidden assumptions: "Why would that hold under [scenario]?"
- Cross-check claims against the codebase or docs; surface mismatches explicitly.
- Flag terminology conflicts against GLOSSARY.md immediately.
- Express contradictions as shared confusion:
  "We seem to have two things that don't align — you said X, but also Y.
  How do those coexist?"
- For each question, provide your recommended answer.
- Exhaust one component or decision before opening the next.

### Decide — write to DECISIONS.md only when all 3 hold
1. Hard to reverse — real cost to changing course
2. Future readers need the reasoning — surprising without context
3. Genuine trade-offs — alternatives were actually evaluated

### Document
- Update GLOSSARY.md when a term is challenged and resolved; don't introduce new terms.
- Write DECISIONS.md entries immediately — don't batch.
- Update any ARCHITECTURE.md that might be affected by the decisions.
- Capture resolved domain terms using the canonical name from GLOSSARY.md.

## Rules
- One question at a time, always
- Read the codebase and documentation before asking the user — use code and documentatio as the first source of truth
- Use DECISIONS-TEMPLATE.md and GLOSSARY-TEMPLATE.md for output structure
