# Skills

Agent skills I use in my workflow. Most of them work together to take a large, vague problem through to built code. Each skill's folder holds its own `SKILL.md`. Any templates and references a skill needs live in the same folder.

## Install

Clone the repo and link the skills you want into `~/.claude/skills`:

## Working with pathfinder

`/pathfinder` is the way in when a problem is too big or too vague to start on. It doesn't solve the problem. Instead it grows a **design tree** of the smaller questions between you and a finished result, and you answer them one per session.

1. **Plant the tree.** Run `/pathfinder` with the problem as you'd describe it: "I want to build X." It asks what reaching the end looks like (a spec, a decision, a working prototype, a shipped change), then sketches branches of open questions. Questions that are already sharp become tasks, and fuzzy ones are kept as seeds. It writes `DESIGN-TREE.md` and `GLOSSARY.md`, then stops.
2. **Grow it, one task per session.** Run `/pathfinder` again. It picks the next open task (or the one you name) and hands it to the skill that fits:
   - `/research` for facts from docs, APIs or the codebase
   - `/ideation` for user-facing design questions where taste decides
   - `/prototype` for questions you answer by trying something cheap
   - `/critique` for decisions that need pressure-testing
   - Manual tasks get a checklist instead.

   Decisions go into `DECISIONS.md`, along with what each one rests on. Smaller answers stay as one line in the tree. When a later answer breaks something a decision rested on, pathfinder adds a task to revisit it rather than editing history.
3. **Prune when it gets heavy.** Every session loads the tree and decisions in full. Once they pass about 600 lines, run `/pruning`. It archives superseded decisions, cuts dead branches and merges duplicates, and asks before each cut that needs judgement.
4. **Build.** Once the tree reaches its destination, `/define` turns the settled design into a spec and tickets, and `/implement` builds them test-first, one commit per ticket.

## Skills

| Skill | What it's for | Source |
|---|---|---|
| [pathfinder](pathfinder/) | Grow a design tree of session-sized tasks for a large or vague problem | Original |
| [research](research/) | Investigate a question against primary sources and save cited notes | Original |
| [ideation](ideation/) | Diverge and converge on a user-facing design question | Original |
| [prototype](prototype/) | Build a throwaway artifact to answer a design or logic question | Original |
| [critique](critique/) | Pressure-test a design one hard question at a time and record the decisions | Adapted from Matt Pocock's [grill-me](https://github.com/mattpocock/skills) |
| [pruning](pruning/) | Keep a design tree and its decisions small enough to load in full | Original |
| [define](define/) | Turn a settled design into a spec and agent-ready tickets | Original |
| [implement](implement/) | Build tickets test-first, reviewed and committed one at a time | Original |
| [idea-to-design-tree](idea-to-design-tree/) | One-off migration from pathfinder's older `IDEA-TREE.md` format | Original |
| [improve-codebase-architecture](improve-codebase-architecture/) | Find opportunities to deepen a codebase's architecture and critique the one you pick | From [mattpocock/skills](https://github.com/mattpocock/skills) |
| [teach](teach/) | Teach a topic over several sessions as interactive HTML lessons | From [mattpocock/skills](https://github.com/mattpocock/skills) |
| [teach-md](teach-md/) | Teach a topic from a prewritten Markdown-only curriculum | Markdown variant of teach |
| [unslop](unslop/) | Cut AI tells from writing | Adapted from poteto's [pstack](https://github.com/cursor/plugins/tree/main/pstack) |
| [swiftui-expert-skill](swiftui-expert-skill/) | SwiftUI guidance on state, composition, performance and modern APIs | From [AvdLee/SwiftUI-Agent-Skill](https://github.com/AvdLee/SwiftUI-Agent-Skill) |

## Credits

- [Matt Pocock's skills](https://github.com/mattpocock/skills): `improve-codebase-architecture` and `teach` come from there. `critique` grew out of his `grill-me`, and its one-question-at-a-time interview with a recommended answer started as his.
- [Antoine van der Lee's SwiftUI Agent Skill](https://github.com/AvdLee/SwiftUI-Agent-Skill): `swiftui-expert-skill` is vendored from there.
- [Lauren Tan's (poteto) pstack](https://github.com/cursor/plugins/tree/main/pstack): `unslop` comes from there, with small modifications.
- Pathfinder's design tree takes its name and idea from Frederick P. Brooks's *The Design of Design*.

## License

MIT, see [LICENSE](LICENSE). The skills that come from other repos are also MIT and keep their original copyright notice in a `LICENSE` file inside their own folder.
