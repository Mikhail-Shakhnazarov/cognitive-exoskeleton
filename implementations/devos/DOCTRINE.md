# Doctrine

Operational principles for the exoskeleton. This is how the system works.

---

## Core

**Operator terminates.** All decision loops close with the human operator. Models assist. Operator initiates, reviews, accepts, rejects. This is architecture, not preference.

**Ports don't share context.** Port B interprets, drafts specs. Port A executes specs, returns friction. The boundary localizes failure and enables parallel operation.

**Context is the resource.** Both ports are frontier models with large context windows. Load densely. Past sessions, patterns, specs, source files. Dense context beats roundtrips.

**Terse carries structure.** Dense prose. Grammar carries hierarchy. Artifacts carry their own map. If it can't be stated tersely, it's not stable yet.

---

## Flow

**Parallel, not pipeline.** Port B can work while Port A executes. Operator coordinates. Dispatch, receive, route.

**Sessions persist.** Conversations save to files. Searchable, loadable. Memory extends across time.

**Patterns accumulate.** Bugs become patterns. Idioms become scaffolds. Knowledge compounds across projects.

**State is observable.** now.md shows current position. Changelog shows what changed. Friction shows what's blocked. Operator can check without monitoring.

---

## Handoff

```
Operator thinks with Port B
    v
Design stabilizes -> spec drafted
    v
Operator reviews spec -> approve or iterate
    v
Spec published to project
    v
Port A loads spec, executes
    v
Code + changelog (or friction)
    v
Operator reviews -> integrate or route friction
```

The spec is the interface. Port B produces it; operator approves it; Port A consumes it.

---

## Files

**Infrastructure (vault root):**
- `now.md` -- global entry, project switcher
- `DOCTRINE.md` -- this file
- `PORT_B_SYSTEM.md` -- Port B context
- `PORT_A_PROTOCOL.md` -- Port A rules
- `research/` -- concept wiki
- `patterns/` -- bugs, idioms, learnings
- `sessions/` -- saved conversations
- `templates/` -- artifact templates
- `assets/` -- images, sketches, diagrams

**Per project (`projects/<n>/`):**
- `now.md` -- project entry surface
- `specs/` -- Port B -> Port A contracts
- `src/` -- code (Port A writes)
- `logs/changelog.md` -- execution history
- `assets/` -- project-specific visual artifacts

---

## Entry

Operator sits down. Opens root `now.md` in Obsidian. Sees project landscape. Opens project's `now.md`. Reads state in 10 seconds. Opens terminal for Port B, or VS Code for Port A, or both in parallel.

Re-entry cost should be near-zero. If it's not, `now.md` needs updating.

---

## Unknowns

If something isn't decided, mark it:

```
[OPEN: description -- what would close it]
```

Port A will friction on OPEN items, not guess. Closure is operator action.

---

## Friction

When Port A can't proceed:

```
[FRICTION] spec#clause -- what's missing -- proposed closure
```

Friction routes to operator. Operator either decides, or sends to Port B for elaboration. Friction is signal, not failure.

---

## Maintenance

**Sessions:** Save at session end. Name: `YYYYMMDD_HHMM_<project>_<slug>.md`

**Patterns:** Port A appends bugs. Operator curates periodically. High-count patterns may warrant tooling.

**now.md:** Update when state changes materially. Timestamps should be current.

**Learnings:** Add when sessions produce reusable insights.

**Distillation:** Periodically extract decisions and insights from old sessions into LEARNINGS.md. Archive or delete raw sessions. Working paper becomes canon through operator curation.

---

## Growth

The exoskeleton builds itself. This doctrine is versioned. New concepts get research entries. New patterns get added. Session history grows. The interface improves through use.
