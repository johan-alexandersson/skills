---
name: define
description: Synthesize the current conversation into a spec, then capture it as tickets — one spec-update ticket per changing module plus vertical-slice implementation tickets — in the repo's system of record. No interview; deepens via /critique when context is thin. Use when a conversation has converged on a change and you're ready to turn it into tracked, agent-ready work.
disable-model-invocation: true
---

# define

## What to do

Invoke after a conversation has converged on a change — a new set of features, or edits to
what a module already does. `define` synthesizes that conversation into a spec, then
captures the spec as tickets in the repo's system of record. **Do NOT interview the user** —
synthesize what has already been discussed. If the conversation is too thin to write a
confident spec, that's what the gate is for: name the gaps and hand off to `/critique`.

The output is **two kinds of tickets**:

1. **Spec-update ticket(s)** — one per changing module, to update that module's spec doc.
2. **Implementation ticket(s)** — vertical slices that build the features the spec describes.

- Synthesize; don't interview. The design work is already in the conversation.
- Gate on sufficiency first — if the context is thin, flag it and go to `/critique` before
  capturing anything.
- Respect recorded DECISIONS and use GLOSSARY canonical terms throughout.
- Every ticket is a narrow-but-complete vertical slice, sized to one fresh context window.

## Workflows

### Ground — before anything else
- If a codebase exists: read it first. Understand the current state before synthesizing.
- Read the **nearest `AGENTS.md`**, then `ARCHITECTURE.md`, `DECISIONS.md`, `GLOSSARY.md`,
  and the existing spec docs of the modules you expect to touch.
- Ground-truth priority: `codebase → ARCHITECTURE.md → DECISIONS.md → GLOSSARY.md → stated goals`.
- Determine the **system of record** for tickets from `AGENTS.md`. If `AGENTS.md` describes
  a tracker (or an issue/ticket location), use it. If none is described, default to Markdown
  at `docs/<module>/<ticket>.md`.
- Do not re-litigate a recorded DECISION. If one genuinely needs revisiting, surface it via
  `/critique` — don't silently work around it.

### Gate — is the context enough?
- Before synthesizing, judge whether the conversation + codebase actually settle the change.
- If there are unresolved design questions, terminology conflicts against `GLOSSARY.md`, or
  load-bearing choices that were never decided: **name the specific gaps**, confirm with the
  user, then dispatch `/critique` to deepen. `/critique` settles the open questions and keeps
  `DECISIONS.md` / `ARCHITECTURE.md` / `GLOSSARY.md` current.
- **Resume** here once the gaps are closed. Only proceed to synthesis when you're confident
  you can write the spec without guessing.

### Synthesize the spec
- Write the spec using `SPEC-TEMPLATE.md`: Problem Statement, Solution, User Stories (a long,
  numbered list covering every aspect), Implementation Decisions, Testing Decisions, Out of
  Scope, Further Notes.
- In Implementation Decisions, name the modules/interfaces/contracts that change. Do NOT
  include file paths or code snippets — they go stale. (Exception: a precise decision-encoding
  snippet from a prototype — a schema, state machine, or type shape — trimmed to the
  decision-rich part.)
- Use `GLOSSARY.md` vocabulary throughout; respect the ADRs/DECISIONS in the area you touch.
- Identify the **set of changing modules** — this drives the spec-update tickets.
- This spec is internal. It is **not** published as a standalone doc; it is the source
  content for the tickets below.

### Choose seams
- Sketch the seams at which the feature will be tested. Prefer existing seams to new ones.
- Use the highest seam possible; the fewer seams across the codebase, the better — ideal is one.
- If a new seam is needed, propose it at the highest point you can. Check the seams with the
  user before drafting tickets.

### Draft tickets
Draft both kinds using `TICKET-TEMPLATE.md`:

- **Spec-update ticket — one per changing module.** Its job is to update that module's spec
  doc to describe the new behaviour. Carry the module-relevant slice of the synthesized spec
  as the ticket's target content and acceptance criteria. Co-locate it under that module.
- **Implementation tickets.** Each cuts a narrow but **complete** path through every layer
  (schema, API, UI, tests) — a tracer bullet that is demoable or verifiable on its own, sized
  to one fresh context window. Set `Blocked by` edges to only the tickets that genuinely gate it.
  - *Wide-refactor exception:* for a mechanical change with broad blast radius (renaming or
    retyping a shared symbol), use expand → contract: add the new form beside the old so
    nothing breaks, migrate call sites in batches (per package / per directory) keeping CI
    green, then delete the old form once no caller remains.
- **Blocking rule:** a module's spec-update ticket **blocks** the implementation tickets that
  change that module's behaviour. The spec doc is the contract; it lands first.

### Confirm granularity
Quiz the user before publishing:
- Does the granularity feel right — too coarse, too fine?
- Are the blocking edges correct — does each ticket depend only on tickets that genuinely gate it?
- Should any tickets be merged or split further?

### Publish
- Publish to the system of record determined in **Ground**, in dependency order (blockers first).
- Use the platform's native blocking / sub-issue relationship where it has one; otherwise set
  each ticket's `Blocked by`. Apply the tracker's `ready-for-agent` label where supported.
- **Default (no tracker in `AGENTS.md`):** one Markdown file per ticket at
  `docs/<module>/<ticket>.md`, numbered `01…NN` in dependency order. Never a single combined file.

## Rules
- No interview — synthesize what's already known. The gate, not questions, handles thin context.
- Read the code and `AGENTS.md` / `ARCHITECTURE.md` / `DECISIONS.md` / `GLOSSARY.md` before
  synthesizing — they are the first source of truth.
- Use `GLOSSARY.md` canonical terms; don't introduce competing names.
- Don't re-litigate a recorded DECISION — route any revisit through `/critique`.
- One spec-update ticket per changing module; spec-update blocks the matching implementation
  tickets.
- Every implementation ticket is a vertical slice sized to one fresh context window.
- Publish in dependency order, blockers first; one file per ticket.
- Use `SPEC-TEMPLATE.md` and `TICKET-TEMPLATE.md` for output structure.
