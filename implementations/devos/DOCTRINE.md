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
    â†“
Design stabilizes â†’ spec drafted
    â†“
Operator reviews spec â†’ approve or iterate
    â†“
Spec published to project
    â†“
Port A loads spec, executes
    â†“
Code + changelog (or friction)
    â†“
Operator reviews â†’ integrate or route friction
```

The spec is the interface. Port B produces it; operator approves it; Port A consumes it.

---

## Files

**Infrastructure (vault root):**
- `now.md` â€” global entry, project switcher
- `DOCTRINE.md` â€” this file
- `PORT_B_SYSTEM.md` â€” Port B context
- `PORT_A_PROTOCOL.md` â€” Port A rules
- `research/` â€” concept wiki
- `patterns/` â€” bugs, idioms, learnings
- `sessions/` â€” saved conversations
- `templates/` â€” artifact templates
- `assets/` â€” images, sketches, diagrams

**Per project (`projects/<n>/`):**
- `now.md` â€” project entry surface
- `specs/` â€” Port B â†’ Port A contracts
- `src/` â€” code (Port A writes)
- `logs/changelog.md` â€” execution history
- `assets/` â€” project-specific visual artifacts

---

## Entry

Operator sits down. Opens root `now.md` in Obsidian. Sees project landscape. Opens project's `now.md`. Reads state in 10 seconds. Opens terminal for Port B, or VS Code for Port A, or both in parallel.

Re-entry cost should be near-zero. If it's not, `now.md` needs updating.

---

## Unknowns

If something isn't decided, mark it:

```
[OPEN: description â€” what would close it]
```

Port A will friction on OPEN items, not guess. Closure is operator action.

---

## Friction

When Port A can't proceed:

```
[FRICTION] spec#clause â€” what's missing â€” proposed closure
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
