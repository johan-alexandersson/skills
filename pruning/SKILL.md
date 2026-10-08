---
name: pruning
description: Prune a design tree and its decisions so they stay small enough to load in full — archive superseded decisions, cut dead branches, merge duplicate tasks.
disable-model-invocation: true
---

# pruning

Every pathfinder session loads DESIGN-TREE.md and DECISIONS.md in full: the **standard context**. Pruning keeps it lean. What no longer bears on the design moves out of the standard context or is cut, and stays reachable through a pointer or git history. Pruning changes no decision and resolves no task; a change in a decision's footing is pathfinder's to route.

## Steps

1. **Load the standard context**: DESIGN-TREE.md, DECISIONS.md and GLOSSARY.md. Note the line count of DESIGN-TREE.md and DECISIONS.md together.
2. **Apply the mechanical cuts.** Done when no mechanical category's *Use when* still matches anywhere.
3. **Gather the judgement candidates.** Check every judgement category against every branch, task, seed, open thread, note and entry. Done when each category has been checked across the whole standard context, with "none" recorded for a category that found nothing.
4. **Present the candidates**, ordered by the lines each would remove, largest first. Quote each with its location and give the proposed cut. Ask which to apply.
5. **Apply the approved cuts.**
6. **Report**: the mechanical cuts made, the judgement cuts applied and declined, and the line count before and after.

## Mechanical cuts

Applied directly: each follows a fixed rule, and the full text stays one pointer away.

- **Superseded decisions** — *Use when* an entry carries **Superseded by**. Move it whole and unchanged to DECISIONS-ARCHIVE.md beside DECISIONS.md, keeping its number, and leave nothing in its place. The superseding entry's **Supersedes** line is the way back.
- **Restated decisions** — *Use when* a resolved task line repeats what its linked entry records. Cut the line to its question and the link.

## Judgement cuts

Presented as candidates: each can lose something a later session needed.

- **Unrecorded decisions** — *Use when* a resolved line carries a decision that passes critique's bar but has no entry. Write the entry from what the line records, using critique's DECISIONS-TEMPLATE.md, and cut the line to a link.
- **Dead branches** — *Use when* every task in a branch is resolved and nothing open depends on it, or a decision made the branch moot. Collapse it to the branch line and its decision links, or remove it.
- **Duplicates** — *Use when* two tasks, seeds or open threads ask the same question. Merge them into one.
- **Conflicts** — *Use when* an open task, seed or open thread contradicts a live decision or another task. Rewrite or remove it. Where the conflict suggests the decision is wrong rather than the task, keep both and name it in the report: that is a revisit for pathfinder to raise.
- **Sediment** — *Use when* Notes, Seeds, Out of scope or GLOSSARY.md repeat what another file holds, or describe what no longer holds. Cut it, or cut it to a pointer.

## Files

- **Standard context**, loaded every pathfinder session: DESIGN-TREE.md, DECISIONS.md, GLOSSARY.md.
- **Reached through pointers**: DECISIONS-ARCHIVE.md (through **Supersedes**), research notes, prototypes, specs.
- **Git history** holds whatever is cut outright.
