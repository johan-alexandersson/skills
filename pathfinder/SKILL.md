---
name: pathfinder
description: Breaks down a large, undefined problem into an idea tree of small, independently resolvable tasks — research, ideation, prototyping, critique, or manual — each sized for one session. Produces and maintains IDEA-TREE.md and GLOSSARY.md. Use when a problem is too big or too undefined to tackle directly and needs to be broken down before it can be worked.
---

# pathfinder

## What to do

Invoke with any large or half-formed problem: "I want to build X" or "I'm thinking about Y" or "we need to figure out Z."

A big problem arrives wrapped in the unknown: the way from here to done isn't visible yet. Pathfinder isn't about solving the problem — it's about growing an **idea tree** of the smaller questions that stand between here and there, so each can be resolved in its own session. Some resolutions will crystallize into decisions the critique skill can turn into ARCHITECTURE.md / DECISIONS.md.

- Use divergent thinking to fan the problem out breadth-first into branches and tasks, no evaluation yet.
- Use convergent thinking to name the destination and pick which task to work next.
- Every task gets a name, a type, and the question or exploration it's meant to resolve.
- Build and maintain IDEA-TREE.md and GLOSSARY.md using the templates in this skill folder.

## Task Types

Each task is one of five types, dispatched to its own skill (or handled directly for manual work):

- **Research** — reading docs, APIs, or the codebase for facts that inform a decision. Dispatch to `/research`. AFK: can run as a background pass; produces a linked markdown note.
- **Ideation** — a vague sub-question that needs diverge/converge dialogue to take shape. Dispatch to `/ideation`. HITL: a live conversation; updates the task's branch and GLOSSARY.md.
- **Prototyping** — "does this feel right" questions answered with a cheap, throwaway artifact. Dispatch to `/prototype`. HITL: built and reacted to together.
- **Critique** — pressure-testing a decision or design until it crystallizes. Dispatch to `/critique` — this is pathfinder's "grilling": one challenging question at a time. HITL. Produces DECISIONS.md entries, keeps ARCHITECTURE.md/GLOSSARY.md current.
- **Task** — manual work that has to happen before a decision can be made, but isn't itself a decision (signing up for a service, provisioning access, moving data so its shape can be seen). No specifying skill: pathfinder hands over a precise checklist and records what was done.

## Workflows

### Plant the tree — first invocation
1. **Name the destination.** One question at a time: what does reaching the end of this tree look like — a spec, a decision, a working prototype, a shipped change? This fixes scope before anything else.
2. **Sketch the branches, breadth-first.** Diverge across the whole space rather than deep on one thread: accept every direction, no evaluation, surface the open questions. Turn what's already sharp into a task (name + type + question); leave anything too vague to phrase precisely yet as a seed.
3. **Write IDEA-TREE.md** using IDEA-TREE-TEMPLATE.md: Destination, Notes, Branches with their first tasks, Seeds, Out of scope left empty.
4. **Seed GLOSSARY.md** for any terms that already stabilized during sketching.
5. Stop. Planting the tree is its own session — don't resolve tasks yet.

### Grow the tree — later invocations
1. Load IDEA-TREE.md.
2. Pick the next task: the one the user names, or the first open task in Branches order. Note it as in progress so it's obvious what's being worked.
3. Dispatch to the task's skill (or, for a manual task, hand the user a precise checklist). Let that skill's own rules govern the session.
4. **Record the resolution** on IDEA-TREE.md: check the task off, add a one-line answer, link any asset it produced (research note, prototype, DECISIONS.md entry).
5. **Sprout the seeds.** If the answer makes a seed specifiable, turn it into a new task under the right branch and remove it from Seeds. If it reveals work beyond the destination, move it to Out of scope instead of resolving it.
6. Resolve one task per session — the pull to keep going past it is usually the signal to stop and let the tree absorb what was just learned.

## Rules
- One question at a time when naming the destination or sketching branches.
- Diverge before converge — no evaluating a direction while still fanning it out.
- Don't invent a task for a question you can't yet phrase precisely — leave it as a seed.
- Every task names the skill (or manual checklist) that will resolve it.
- Use IDEA-TREE-TEMPLATE.md and GLOSSARY-TEMPLATE.md for output structure.
