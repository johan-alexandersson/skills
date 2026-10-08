---
name: idea-to-design-tree
description: Convert a project's IDEA-TREE.md into a DESIGN-TREE.md and repoint everything that references it.
disable-model-invocation: true
---

# idea-to-design-tree

Converts one project from pathfinder's old idea tree to its design tree. The conversion is a **rename and a relink**: the file and every pointer to it change name, and decision nodes are checked against DECISIONS.md. It rewrites pointers only. Every decision, answer and line of reasoning stays as written. Old entries gain **Rests on** when a revisit touches them; recording decisions that live only on the tree is work for `/pruning`.

The target shape is pathfinder's `DESIGN-TREE-TEMPLATE.md` and critique's `DECISIONS-TEMPLATE.md`. Read both first.

## Steps

1. **Find the tree.** Locate `IDEA-TREE.md` in the project. Done when you hold exactly one path. Several trees, or a `DESIGN-TREE.md` already present: stop and ask the user.
2. **Rename it.** `git mv` when the project is a git repository, a plain move otherwise. Change the heading `# Idea Tree:` to `# Design Tree:`. Done when `IDEA-TREE.md` is gone and the new file opens with the new heading.
3. **Repoint every reference.** Search the whole project, case-insensitive, for `idea.tree` — AGENTS.md / CLAUDE.md, conventions docs, READMEs, research notes, specs, tickets, GLOSSARY.md and DECISIONS.md included. Change each to `DESIGN-TREE.md` / design tree, matching the original's form. A mention inside a DECISIONS.md entry is a pointer and gets repointed; the entry's words around it stay. Done when the search returns nothing outside vendored or generated files.
4. **Audit the decision nodes.** Walk every checked task line in the tree and sort it into one of three:
   - **Linked** — points to a DECISIONS.md entry that exists. Conforms.
   - **Answer** — a one-line resolution short of critique's decision bar, with or without an asset link. Conforms.
   - **Unrecorded decision** — reads as a decision that passes the bar, but has no entry, or carries the alternatives set aside on the tree instead of in the entry.

   Done when every checked line has a sort.
5. **Report.** Give the user the renamed path, each file repointed with its count, and the list of **unrecorded decisions**, each quoted with its line number. That list is the hand-off to `/pruning`; leave the lines themselves as they are.
