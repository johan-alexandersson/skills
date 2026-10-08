---
name: critique
description: Challenge a plan or design one hard question at a time until the decisions crystallize into DECISIONS.md and ARCHITECTURE.md. Use when a design needs pressure-testing before it is built.
---

# Critique 

## What to do

Invoke with a design description, DESIGN-TREE.md, architectural plan, or just "here's what I want to build." A codebase does not need to exist yet.

Also invoked by `/pathfinder` as its critique task type — this is the design tree's
pressure test. When dispatched that way, the question comes from the task in the DESIGN-TREE.md, and the resulting DECISIONS.md entry (or resolved GLOSSARY.md term) gets linked back there.

- Interview me relentlessly about every aspect of the plan.
- Explore the codebase or documentation to answer questions before asking.
- Ask one challenging question at a time, going deep before moving on. For each question, provide your recommended answer.
- Write DECISIONS.md entries when architectural decisions crystallize.

## Workflows

### Ground — before anything else
- If a codebase exists: read it first. Answer questions from code before asking the user.
- Ground truth priority: codebase → ARCHITECTURE.md → docs/specs → DESIGN-TREE.md → stated goals.

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

Anything short of the bar is an answer, not a decision: it goes on the task's line in
DESIGN-TREE.md.

A decision is provisional — it holds while what it rests on holds. Record that footing in
**Rests on**: the specific requirements, constraints and goals it assumes.

### Revisit — when a recorded decision's footing has moved
- Name the change and which **Rests on** items it breaks. An entry without **Rests on** stands on
  its Context and Why; the new entry always carries **Rests on**.
- Earlier superseded versions sit in DECISIONS-ARCHIVE.md, reached through **Supersedes**; follow
  that link when the decision's history bears on the revisit.
- Critique the decision again from that new footing, as for a fresh one.
- If it changes, write a new entry with **Supersedes**, and add **Superseded by** to the old
  one. The old entry's reasoning stays as written — it is the history of how the design moved;
  `/pruning` later moves it to DECISIONS-ARCHIVE.md.

### Document
- Update GLOSSARY.md when a term is challenged and resolved; don't introduce new terms.
- Write DECISIONS.md entries immediately — don't batch.
- Update any ARCHITECTURE.md that might be affected by the decisions.
- Capture resolved domain terms using the canonical name from GLOSSARY.md.

## Rules
- One question at a time, always
- Read the codebase and documentation before asking the user — use code and documentation as the first source of truth
- Use DECISIONS-TEMPLATE.md and GLOSSARY-TEMPLATE.md for output structure
