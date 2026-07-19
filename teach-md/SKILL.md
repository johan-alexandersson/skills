---
name: teach-md
description: Teach the user a new skill or concept from a prewritten, Markdown-only curriculum, within this workspace.
disable-model-invocation: true
argument-hint: "What would you like to learn about?"
---

The user has asked you to teach them something. This is a stateful request — they intend to learn the topic over multiple sessions, following a curriculum you prewrite for them.

Everything you produce is **Markdown**. No HTML anywhere — not in the curriculum, not in lessons, not in quizzes. If you reach for an HTML tag (`<details>`, `<br>`, inline styles, embedded widgets), stop and express it in plain Markdown instead.

## Workspace

Treat the current directory as a teaching workspace. Its whole state lives in just a few files — create each one lazily, only when there's something to put in it:

- `CURRICULUM.md` — the spine of the workspace: the **mission**, the curated **resources**, and the prewritten **curriculum** (the ordered lesson sequence the user follows). One document, built from the process below.
- `REFERENCE.md` — the combined **resources + glossary** reference: the growing list of sources gathered while researching lessons, plus the canonical vocabulary every lesson adheres to.
- `./lessons/*.md` — the lessons themselves, one self-contained Markdown file each, named `0001-slug.md` to match the curriculum.
- `NOTES.md` — a scratchpad for how the user likes to be taught and any working notes to carry across sessions.

The workspace does **not** track progress. The user drives which lesson they're on; infer position from which lesson files exist, or just ask.

## Process

Producing the course is a short, mostly conversational pipeline. Do the thinking in chat first; commit to files only once the shape is settled.

1. **Explore & outline (in chat).** Find high-trust resources on the topic — never work from parametric memory. Clarify the **mission**: the concrete real-world goal driving this, pushed past "to understand X" to the underlying outcome. Then propose a **curriculum outline** conversationally — the modules and lessons at a glance — so the user can react before anything is written.
2. **Deepening session (in chat).** With the outline on the table, explore **which aspects the user wants to focus on** and **how the lessons should be built** — where the boundaries fall, how big each lesson is, where practice lands, what to skip or defer. A prewritten course is a set of choices about what to leave out; make them here, with the user.
3. **Write `CURRICULUM.md`.** Commit the settled plan — mission, resources, and the ordered curriculum — into one file (template below).
4. **Write `REFERENCE.md`.** Seed the combined resources + glossary file with the sources you have and the vocabulary the course will speak.
5. **Research & structure the lessons.** Work through the curriculum, researching and writing each lesson against it, and growing `REFERENCE.md` as you go.

Revisit steps 1–2 whenever the shape turns out wrong — a missing dependency, a lesson that's really three, a focus that shifts. Fixing the plan is far cheaper than reworking a course built on it. Because the curriculum is prewritten, a mission change usually means revising it — confirm with the user first.

## Philosophy

Deep learning needs three things: **knowledge** (captured from high-trust resources), **skills** (built through relevant practice), and **wisdom** (from testing skills against the real world). Some topics lean more one way — theoretical physics is knowledge-heavy, yoga is skills-heavy.

Split two kinds of retention: **fluency** (in-the-moment recall) can feel like mastery but is illusory; **storage strength** (durable retention) is the real goal. Build it with desirable difficulty — retrieval practice, spacing (revisiting earlier material later), and interleaving related topics. Sequence the curriculum so earlier material resurfaces in later lessons.

For **acquiring knowledge**, difficulty is the enemy — it eats the working memory needed to understand. For **building skill**, difficulty is the tool — effortful retrieval is what makes knowledge stick.

## `CURRICULUM.md`

The prewritten course: mission, resources, and the full lesson sequence, ordered so each lesson builds on the last. This is what the user follows, at their own pace — there's no adaptive, session-by-session recalculation. That trades adaptivity for legibility, so get the sequence right in steps 1–2 before committing.

```md
# {Topic}

## Mission
**Why:** {1–3 sentences — the concrete real-world goal driving this.}
**Success looks like:** {specific, observable things the user will be able to do.}
**Out of scope:** {what's deliberately not being chased right now.}

## Resources
{The handful of high-trust sources that ground the course, plus communities for real-world practice. One line each: what it covers, when to reach for it. Prefer a few sharp sources to many mediocre ones.}
- [Source title](url) — {what it covers / when to use it}
- Community: [name](url) — {what to test there}

## Curriculum
{1–2 sentences: what the course covers end to end, tied to the mission.}

### Module 1 — {module title}
1. **[{Lesson title}](./lessons/0001-slug.md)** — {the single win} · _builds on:_ nothing
2. **[{Lesson title}](./lessons/0002-slug.md)** — {the single win} · _builds on:_ Lesson 1

### Module 2 — {module title}
3. **[{Lesson title}](./lessons/0003-slug.md)** — {the single win} · _builds on:_ Lessons 1–2
```

Rules:
- **Plan the whole arc before writing any lesson** — coherence end to end is the point of a prewritten course.
- **Number lessons globally** (`0001`, `0002`, …) to match the filenames in `./lessons/`; modules just group them.
- **Order for the zone of proximal development** — each lesson reachable from the last, none assuming what the curriculum hasn't taught. `builds on:` keeps the ordering auditable.
- **Front-load knowledge, build toward skill**, and deliberately revisit earlier material later.
- **Lessons may be listed before they're written** — the plan precedes the lessons.
- **Ground it in the mission.** Every lesson traces back to why the user is here. If the mission is unclear, interview them before writing anything.

## `REFERENCE.md`

The combined resources-and-glossary reference — the working companion to the curriculum. Where `CURRICULUM.md` holds the few sources that shaped the plan, this holds the fuller list gathered while researching lessons, plus the canonical vocabulary. Lessons cite its sources and speak its terms.

```md
# {Topic} Reference

## Sources
{Sources gathered while researching lessons — the detailed, growing list. One line each. High-trust only; prune what turns out shallow or wrong.}
- [Source title](url) — {what it covers, which lessons it backs}

## Communities (wisdom)
{Where the user tests skills in the real world — a forum, subreddit, or local group. Respect it if they opt out.}
- [name](url) — {what to practise there}

## Glossary
{The canonical vocabulary. Define what each term IS in one or two tight sentences; when several words exist, pick one and list the rest as aliases to avoid. Use these terms everywhere, including inside other definitions.}
**{Term}**: {tight definition.} _Avoid:_ {aliases}
```

When a question calls for real-world **wisdom**, answer if you can, then point the user to one of the listed communities to test it for real.

## Lessons

Each lesson is one self-contained Markdown file in `./lessons/`, named `0001-slug.md` to match its curriculum entry. It teaches one tightly-scoped thing tied to the mission and gives the user a single tangible win. Keep it short — working memory is small — but beautiful: clean headings, short paragraphs, readable when printed. Think Tufte, in Markdown.

Teach only the knowledge the skill needs, cite claims with links into `REFERENCE.md`, and speak its glossary exactly. Then make it stick with practice. Since Markdown has no interactive widgets, use **inline self-checks**: a Practice section, and an Answer key at the very bottom, separated by distance so recall comes first — never hidden HTML. Invite the user to bring answers back to you; the agent is the tightest feedback loop available.

If possible, open the lesson file for the user with a CLI command.

```md
# {Lesson title}

> **Lesson {nnnn}** of the [{Topic} Curriculum](../CURRICULUM.md) · _builds on:_ [Lesson {prev}](./{prev}.md) · _next:_ [Lesson {next}](./{next}.md)

{One or two sentences: the single win, and why it matters for the mission.}

## Learn
{The minimum knowledge the skill needs. Cite claims with links into ../REFERENCE.md. Use its glossary terms exactly.}

## Practice
1. {Question or task — make the user recall or do, not just read}
2. {…}

## Read next
**Primary source:** [{the single best resource}](url) — {why this one}.
Unclear on anything? Ask your teacher (the agent).

---

## Answer key
1. {Answer}
2. {…}
```

For multiple-choice items, make every option the same number of words (and characters where you can) — give no formatting or length tell.

## `NOTES.md`

Where the user expresses preferences for how they want to be taught, or anything worth carrying across sessions. Record them here and honour them when building lessons.
