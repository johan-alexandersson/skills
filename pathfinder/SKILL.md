---
name: pathfinder
description: Break a large, undefined problem into a design tree of session-sized tasks, maintained in DESIGN-TREE.md and GLOSSARY.md. Use when a problem is too big or too vague to tackle directly.
---

# pathfinder

## What to do

Invoke with any large or half-formed problem: "I want to build X" or "I'm thinking about Y" or "we need to figure out Z."

A big problem arrives wrapped in the unknown: the way from here to done isn't visible yet. Pathfinder isn't about solving the problem — it's about growing a **design tree**, in Brooks's sense, of the smaller questions that stand between here and there, so each can be resolved in its own session.

The tree and DECISIONS.md split the record:
- **The tree records the path.** Each node is a question and the task that answers it.
- **DECISIONS.md records the decision** — what was chosen, the alternatives set aside, and what it rests on. A node that produced a decision links to its entry rather than restating it.
- **Answers** are resolutions short of critique's decision bar: a fact found, a prototype's verdict, a manual step done. They stay as one line on the node.

Decisions are provisional. Each rests on the requirements, constraints and goals as they were understood when it was made, and those keep moving outside the tree — problem and solution co-evolve. Revisiting a decision as that footing moves is part of designing: a later entry supersedes the earlier one, and the tree keeps both on the same node, so the history of how the design changed stays readable.

- Use divergent thinking to fan the problem out breadth-first into branches and tasks, no evaluation yet.
- Use convergent thinking to name the destination and pick which task to work next.
- Every task gets a name, a type, and the question or exploration it's meant to resolve.
- Build and maintain DESIGN-TREE.md and GLOSSARY.md using the templates in this skill folder.

## Task Types

Each task is one of five types, dispatched to its own skill (or handled directly for manual work):

- **Research** — reading docs, APIs, or the codebase for facts that inform a decision. Dispatch to `/research`. AFK: can run as a background pass; produces a linked markdown note.
- **Ideation** — a user-facing design question with many directions worth generating, settled by taste. Dispatch to `/ideation`. HITL: a live conversation; updates the task's branch and GLOSSARY.md. Technical questions are Critique tasks.
- **Prototyping** — "does this feel right" questions answered with a cheap, throwaway artifact. Dispatch to `/prototype`. HITL: built and reacted to together.
- **Critique** — pressure-testing a decision or design until it crystallizes, or revisiting one whose footing has moved. Dispatch to `/critique`: one challenging question at a time. HITL. Produces DECISIONS.md entries, keeps ARCHITECTURE.md/GLOSSARY.md current.
- **Task** — manual work that has to happen before a decision can be made, but isn't itself a decision (signing up for a service, provisioning access, moving data so its shape can be seen). No specifying skill: pathfinder hands over a precise checklist and records what was done.

## Workflows

### Plant the tree — first invocation
1. **Name the destination.** One question at a time: what does reaching the end of this tree look like — a spec, a decision, a working prototype, a shipped change? This fixes scope before anything else.
2. **Sketch the branches, breadth-first.** Diverge across the whole space rather than deep on one thread: accept every direction, no evaluation, surface the open questions. Turn what's already sharp into a task (name + type + question); leave anything too vague to phrase precisely yet as a seed.
3. **Write DESIGN-TREE.md** using DESIGN-TREE-TEMPLATE.md: Destination, Notes, Branches with their first tasks, Seeds, Out of scope left empty.
4. **Seed GLOSSARY.md** for any terms that already stabilized during sketching.
5. Stop. Planting the tree is its own session — don't resolve tasks yet.

### Grow the tree — later invocations
1. Load DESIGN-TREE.md and DECISIONS.md.
2. Pick the next task: the one the user names, or the first open task in Branches order. Note it as in progress so it's obvious what's being worked.
3. Dispatch to the task's skill (or, for a manual task, hand the user a precise checklist). Let that skill's own rules govern the session.
4. **Record the resolution** on DESIGN-TREE.md: check the task off, then link its DECISIONS.md entry if it produced a decision, or add a one-line answer and link any asset it produced (research note, prototype) if it didn't.
5. **Route any change.** Does this answer, or anything the user said this session, break a **Rests on** item of a live decision, or move the Destination? An entry without **Rests on** stands on its Context and Why.
   - **Major** — it breaks a **Rests on** or moves the Destination. A broken **Rests on** becomes a **revisit**: a critique task on that decision's node, naming the entry and what changed; it resolves into a new entry that supersedes the old one, and the original task line stays as it is. A moved Destination is settled with the user one question at a time, before any other task.
   - **Minor** — it bears only on open tasks. Rewrite, merge or add those tasks in place; resolved tasks stay as they are.
6. **Sprout the seeds.** If the answer makes a seed specifiable, turn it into a new task under the right branch and remove it from Seeds. If it reveals work beyond the destination, move it to Out of scope instead of resolving it.
7. Resolve one task per session — the pull to keep going past it is usually the signal to stop and let the tree absorb what was just learned.
8. If DESIGN-TREE.md and DECISIONS.md together run past 600 lines, end the session by suggesting `/pruning`.

## Rules
- One question at a time when naming the destination or sketching branches.
- Diverge before converge — no evaluating a direction while still fanning it out.
- Don't invent a task for a question you can't yet phrase precisely — leave it as a seed.
- Every task names the skill (or manual checklist) that will resolve it.
- Use DESIGN-TREE-TEMPLATE.md and GLOSSARY-TEMPLATE.md for output structure.
