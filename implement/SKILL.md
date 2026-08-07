---
name: implement
description: Implement the tickets produced by /define — test-first at the seams the ticket already names, typechecked and tested as you go, reviewed along Standards and Spec axes, and committed per ticket on a branch. Last stage of the pathfinder → critique → define → implement chain. Use when tickets are ready to build.
disable-model-invocation: true
---

# implement

Build the work captured as **tickets** by `/define`. This is the last stage of the
`/pathfinder` → `/critique` → `/define` → `/implement` chain: pathfinder grew the idea tree,
critique crystallized the decisions, define turned them into tickets — implement lands them as
code. Consume that same context; don't re-derive it.

The work runs as one loop per ticket — build in test-first vertical slices, keep the checks
green — with each ticket committed on a shared branch and reviewed along two axes before its
final commit. At the end of the session, show the commits and ask whether to merge.

## Ground — before anything else

- Read the codebase first, then the **nearest `AGENTS.md`**, `ARCHITECTURE.md`, `DECISIONS.md`,
  `GLOSSARY.md`, and the module spec docs and tickets for the work you're implementing.
- Ground-truth priority: `codebase → ARCHITECTURE.md → DECISIONS.md → GLOSSARY.md → spec/tickets → stated goals`.
- Find the tickets in the **system of record** the way define did: from `AGENTS.md` if it names
  a tracker/location, else Markdown at `docs/<module>/<ticket>.md`.
- Use `GLOSSARY.md` canonical terms for test names and interface vocabulary, so what you build
  speaks the project's domain language.
- **Don't re-litigate a recorded DECISION.** If one genuinely needs revisiting, route it back
  through `/critique` — don't silently work around it in code.
- Work the tickets in **dependency order, blockers first**: a module's spec-update ticket lands
  before the implementation tickets it blocks (the spec doc is the contract; it lands first).

## Git — one branch per related set, commits per ticket

- **Branch once** for the set of related tickets (one define batch / one spec's tickets). Name
  it for the feature. Never commit the work to the main branch directly.
- Work every ticket on that one branch, in dependency order.
- **Each ticket gets one or several commits** — commit at green points within a ticket, and name
  the ticket (its id or title) in every message. Keep a commit to a single ticket; never blend
  two tickets into one commit.
- **At the end of the session**, show the user the commits grouped by ticket
  (`git log <branch-point>..HEAD --oneline`) and **ask whether to merge them to the main branch**.
  Do not merge without that confirmation.

## The loop — per ticket

TDD is the red → green loop, run in **vertical slices**: one test → one minimal implementation →
repeat. Each test is a tracer bullet that responds to what the last cycle taught you — never
write all the tests first, then all the implementation.

- **Use the seams the ticket already names.** define chose and confirmed the seams; test at those,
  don't re-invent them. Only if a ticket carries none (e.g. you're implementing outside a define
  pass) do you agree the seams with the user before writing any test.
- **Red before green.** Write the failing test first, then only enough code to pass it. Don't
  anticipate future tests or add speculative features.
- **One slice at a time.** One seam, one test, one minimal implementation per cycle.
- **Refactoring is not part of the loop.** It belongs to the review stage, not the red → green cycle.
- **Keep the checks green.** Typecheck regularly, run single test files as you touch them, and run
  the full test suite once before the ticket's final commit.

### What a good test is

Tests verify behavior through public interfaces, not implementation details. Code can change
entirely; tests shouldn't. A good test reads like a specification — "user can checkout with valid
cart" tells you exactly what capability exists — and survives refactors because it doesn't care
about internal structure.

### Anti-patterns

- **Implementation-coupled** — mocks internal collaborators, tests private methods, or verifies
  through a side channel (querying the database instead of using the interface). The tell: the
  test breaks when you refactor but behavior hasn't changed.
- **Tautological** — the assertion recomputes the expected value the way the code does
  (`expect(add(a, b)).toBe(a + b)`, a hand-derived snapshot, a constant asserted equal to itself),
  so it passes by construction. Expected values must come from an independent source of truth — a
  known-good literal, a worked example, the spec.
- **Horizontal slicing** — all tests first, then all implementation. Bulk tests verify _imagined_
  behavior and go insensitive to real changes. Work in vertical slices instead.

## Review — before each ticket's final commit

Review the ticket's diff along two axes. Run each axis as a **parallel sub-agent** so they don't
pollute each other's context, then aggregate side by side — do not merge or rerank across axes. A
change can pass one axis and fail the other; keeping them separate stops one from masking the other.

Capture the diff once: `git diff <ticket-start>...HEAD` (three-dot, against the merge-base), plus
`git log <ticket-start>..HEAD --oneline`. Confirm the ref resolves and the diff is non-empty first.

### Standards axis

Does the code conform to the repo's documented standards — `ARCHITECTURE.md`, `DECISIONS.md`,
`CODING_STANDARDS.md`/`CONTRIBUTING.md`, and `GLOSSARY.md` terms? On top of whatever the repo
documents, always carry the **smell baseline** below. Two rules bind it: **the repo overrides** (a
documented standard always wins), and **it's always a judgement call** (each smell is a labelled
heuristic, never a hard violation). Skip anything tooling already enforces.

- **Mysterious Name** — a name that doesn't reveal what it does or holds. → rename it; if no honest name comes, the design's murky.
- **Duplicated Code** — the same logic shape in more than one hunk or file. → extract it, call it from both.
- **Feature Envy** — a method that reaches into another object's data more than its own. → move it onto the data it envies.
- **Data Clumps** — the same few fields or params keep travelling together. → bundle them into one type.
- **Primitive Obsession** — a primitive standing in for a domain concept that deserves its own type. → give the concept its own small type.
- **Repeated Switches** — the same `switch`/`if`-cascade on the same type recurs. → replace with polymorphism, or one shared map.
- **Shotgun Surgery** — one logical change forces scattered edits across many files. → gather what changes together into one module.
- **Divergent Change** — one module edited for several unrelated reasons. → split so each changes for one reason.
- **Speculative Generality** — abstraction or hooks added for needs the spec doesn't have. → delete it; inline back until a real need shows.
- **Message Chains** — long `a.b().c().d()` navigation the caller shouldn't depend on. → hide the walk behind one method.
- **Middle Man** — a class or function that mostly just delegates. → cut it, call the real target direct.
- **Refused Bequest** — a subclass that ignores or overrides most of what it inherits. → drop the inheritance, use composition.

Sub-agent brief: "Report, per file/hunk where relevant, (a) every place the diff violates a
documented standard: cite the standard (file + rule); and (b) any baseline smell: name it and quote
the hunk. Distinguish hard violations from judgement calls — documented breaches can be hard,
baseline smells are always judgement calls, and a documented standard overrides the baseline. Skip
anything tooling enforces. Under 400 words."

### Spec axis

Does the code faithfully implement the ticket? The spec source is **the ticket itself plus its
module spec doc** — the artifacts define produced, found via the system of record from **Ground**.

Sub-agent brief: "Report (a) requirements the ticket/spec asked for that are missing or partial; (b)
behaviour in the diff that wasn't asked for (scope creep); (c) requirements that look implemented but
wrong. Quote the ticket/spec line for each finding. Under 400 words."

### Aggregate

Present the two reports under `## Standards` and `## Spec` headings, lightly cleaned. End with a
one-line summary: total findings per axis and the worst issue _within each axis_. Don't pick a single
winner across axes — that's the reranking the separation exists to prevent. Address the findings, then
make the ticket's final commit.

## Rules

- Consume the chain's context — read the code, `AGENTS.md`, `ARCHITECTURE.md`, `DECISIONS.md`,
  `GLOSSARY.md`, and the tickets before building; they are the first source of truth.
- Use `GLOSSARY.md` canonical terms; don't introduce competing names.
- Don't re-litigate a recorded DECISION — route any revisit through `/critique`.
- Test at the seams the ticket names; only agree new seams if the ticket carries none.
- Red before green; one vertical slice at a time; refactoring belongs to review, not the loop.
- One branch per related set of tickets; one or several commits per ticket, never blended; never on
  the main branch directly.
- Review each ticket along both axes before its final commit; report the axes separately.
- End the session by showing the commits and asking whether to merge to the main branch — never merge
  unprompted.
