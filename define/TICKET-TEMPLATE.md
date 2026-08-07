# [NN] — [ticket title]

> One file per ticket. When publishing to the default Markdown store, name it
> `docs/<module>/<NN>-<slug>.md` and number `NN` from `01` in dependency order (blockers
> first). When publishing to a tracker described in `AGENTS.md`, map these fields onto its
> native issue and use its native blocking / sub-issue relationship for **Blocked by**.

**Type:** spec-update | implementation

**Module:** [the module this ticket belongs to]

**What to build:**
The end-to-end behaviour this ticket makes work, from the user's perspective.

- *For `spec-update`:* describe the change to that module's spec doc — the module-relevant
  slice of the synthesized spec. Target: [path to the module's spec doc].
- *For `implementation`:* describe the vertical slice — a narrow but complete path through
  every layer (schema, API, UI, tests), demoable or verifiable on its own, sized to one
  fresh context window.

**Blocked by:**
The numbers/titles of the tickets that gate this one, or "None — can start immediately."
(An implementation ticket that changes a module is blocked by that module's spec-update ticket.)

**Status:** ready-for-agent

**Acceptance criteria:**
- [ ] [Specific, verifiable outcome]
- [ ] [Specific, verifiable outcome]
- [ ] [Specific, verifiable outcome]
