---
name: prototype
description: Build a throwaway artifact to answer a design or logic question. Use when something needs to be tried before it is committed to.
---

# prototype

A prototype is **throwaway work that answers a question**. The question decides the shape — code, a rough document, a sketch, a stubbed flow, whatever is cheapest to build and react to. If this is a task dispatched from `/pathfinder`, the question comes from the task's line in DESIGN-TREE.md; if it isn't obvious from there, ask.

## Rules
1. **Throwaway from day one, and clearly marked as such.** Put it where it's easy to find in context, but name it so it's obviously not production or final.
2. **One step to experience it.** Whatever "run it" means for this kind of artifact — a command, opening a file, reading a page — the user shouldn't have to think about how.
3. **No persistence or infrastructure by default.** State lives in memory or in the artifact itself. If the question explicitly involves persistence, use a clearly-marked scratch copy, never anything real.
4. **Skip the polish.** No tests, no error handling beyond what makes it runnable, no abstractions. The point is to learn something fast, then delete it.
5. **Surface the state.** After every action or variant, show the full relevant state so the reaction is to something concrete, not imagined.
6. **Delete or absorb when done.** Once it's answered its question, either delete it or fold the validated decision into the real thing — don't leave it rotting in the repo.

## When done
The **answer** is the only thing worth keeping. Capture it — in DESIGN-TREE.md if this was a pathfinder task, otherwise in a commit message, DECISIONS.md, or a note beside the prototype — along with the question it answered, before deleting the prototype.
