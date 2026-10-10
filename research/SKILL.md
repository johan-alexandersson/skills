---
name: research
description: Investigate a question against primary sources and save cited findings as Markdown. Use when facts, docs or API details need gathering.
---

# research

Spin up a **background agent** to do the research, so you keep working while it reads. Always use Opus 5.5 (Low effort) for sub-agents. If this is a task dispatched from `/pathfinder`, the question comes from the task's line in DESIGN-TREE.md.

Its job:

1. Investigate the question against **primary sources** — official docs, source code, specs, first-party APIs — not a secondary write-up of them. Follow every claim back to the source that owns it.
2. Write the findings to a single Markdown file, citing each claim's source.
3. Save it where the repo already keeps such notes; match the existing convention, and if there is none, put it somewhere sensible and say where.
4. If dispatched from a design tree, report the file path back so it can be linked from the task's line in DESIGN-TREE.md.
