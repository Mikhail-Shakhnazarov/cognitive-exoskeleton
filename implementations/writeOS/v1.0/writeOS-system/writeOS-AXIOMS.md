---
title: writeOS Axioms
type: specification
format-version: 0.1
status: draft
created: 2026-01-11
copyright: Mikhail Shakhnazarov 2026
license: CC BY 4.0
---

## Body

writeOS is a repo-backed operating discipline for doing complex work with frontier-model runtimes. It does not depend on conversational continuity. It treats the problem of semantic drift under iteration as architectural, not behavioral.

The first axiom is the cache-memory distinction. Model context windows behave like cache: fast, volatile, bounded, non-authoritative. Repo artifacts behave like memory: durable, diffable, re-enterable, authoritative. Correctness must not depend on what the model remembers. Chat is scratch unless committed to artifacts.

This distinction is epistemic, not just practical. If meaning exists primarily in cache, the system cannot reliably know what it believes. If meaning is forced into artifacts, the system becomes falsifiable. A claim exists when it is written. A decision binds when it is committed. Everything else is working state.

The second axiom is operator termination. The operator is root. All decision loops close with the human operator. Models produce options, drafts, analysis, and execution. The operator initiates, reviews, accepts, rejects. Nothing becomes true by confidence. Decisions become true only when committed into canonical artifacts under operator authority.

This is architectural, not ethical or sentimental. It creates accountability: when something goes wrong, responsibility is localizable. It creates quality control: errors are caught at decision points before propagation. It creates reversibility: decision points are natural checkpoints for rollback. It prevents authority drift: the system does not gradually assume control through accumulated confident outputs.

Operator termination does not mean operator does everything. Models do heavy lifting. But crossing from proposal to commitment requires operator action. The system is designed so this constraint is lightweight. Review is fast. Overhead is minimal. Control is maximal.

The third axiom is port separation. Interpretation and execution are different functions with different failure modes. Mixing them creates ambiguity about where problems originate. Port separation is process isolation applied to cognitive work.

Port B interprets. It thinks with the operator, analyzes situations, surfaces options, drafts specifications. It operates in the space of meaning, structure, and decision. Port A executes. It takes specifications and produces artifacts: code, files, changes. It operates in the space of implementation, precision, and verification.

They do not share context. Port B does not know Port A's execution state unless the operator provides it. Port A does not interpret ambiguity; it returns friction. The boundary localizes failure. Spec has wrong requirements? Port B problem. Code does not match spec? Port A problem. Requirements were ambiguous? Friction reveals it.

The spec is the interface between ports. It is a contract: Port B produces it, operator approves it, Port A consumes it. Friction is the return channel. When Port A cannot proceed, it signals what is missing. Friction routes to operator, who either decides or sends to Port B for elaboration.

These three axioms compose. Cache-memory forces meaning into artifacts. Operator termination ensures artifacts reflect human decisions. Port separation prevents interpretation and execution from contaminating each other. Together they define a system that resists drift, preserves accountability, and remains re-enterable across time gaps, tool changes, and context loss.

---

## Schema

[O-001] Cache-memory distinction
  Type: O-claim
  Summary: Model context is cache; repo artifacts are memory.

[O-002] Cache is volatile
  Type: O-claim
  Summary: Context windows are fast, bounded, and non-authoritative.
  Depends-on: [O-001]

[O-003] Artifacts are authoritative
  Type: O-claim
  Summary: Repo files are durable, diffable, and authoritative.
  Depends-on: [O-001]

[O-004] Chat is scratch
  Type: O-claim
  Summary: Conversation is working state unless committed to artifacts.
  Depends-on: [O-001], [O-003]

[O-005] Meaning requires commitment
  Type: O-claim
  Summary: A claim exists when written; a decision binds when committed.
  Depends-on: [O-004]

[O-006] Operator termination
  Type: O-claim
  Summary: All decision loops close with the human operator.

[O-007] Operator is root
  Type: O-claim
  Summary: The operator holds final authority and responsibility.
  Depends-on: [O-006]

[O-008] Commitment requires operator action
  Type: O-claim
  Summary: Crossing from proposal to commitment requires operator action.
  Depends-on: [O-006], [O-007]

[O-009] Port separation principle
  Type: O-claim
  Summary: Interpretation and execution are isolated functions.

[O-010] Ports do not share context
  Type: O-claim
  Summary: Port B and Port A coordinate only through artifacts.
  Depends-on: [O-009]

[O-011] Boundary localizes failure
  Type: O-claim
  Summary: Port separation makes problem origin identifiable.
  Depends-on: [O-009], [O-010]

[O-012] Spec is the interface
  Type: O-claim
  Summary: The spec is the contract between Port B and Port A.
  Depends-on: [O-009]

[O-013] Friction is the return channel
  Type: O-claim
  Summary: Port A signals blockage through friction, not guessing.
  Depends-on: [O-009], [O-012]

[O-014] Axioms compose
  Type: O-claim
  Summary: The three axioms together define drift-resistant operation.
  Depends-on: [O-001], [O-006], [O-009]

[R-001] Conversational continuity is false memory
  Type: R-claim
  Summary: Chat medium performs continuity but context is unstable.
  Supports: [O-001], [O-004]

[R-002] Coherence bias causes drift
  Type: R-claim
  Summary: Models fill gaps with plausible coherence, introducing drift.
  Supports: [O-009], [O-013]

[R-003] Mixed interpretation-execution hides failure origin
  Type: R-claim
  Summary: When one process does both, problem source becomes ambiguous.
  Supports: [O-011]

[C:cache] Cache
  Type: concept
  Definition: Fast, volatile, bounded working space (model context).

[C:memory] Memory
  Type: concept
  Definition: Durable, diffable, authoritative state (repo artifacts).

[C:operator] Operator
  Type: concept
  Definition: Human authority who terminates decisions.

[C:port] Port
  Type: concept
  Definition: Constrained role with a contract.

[C:drift] Drift
  Type: concept
  Definition: Gradual divergence from intended meaning under iteration.

---

## Binding

[O-001]
  Anchor: "The first axiom is the cache-memory distinction"
  Scope: sentence

[O-002]
  Anchor: "fast, volatile, bounded, non-authoritative"
  Scope: phrase

[O-003]
  Anchor: "durable, diffable, re-enterable, authoritative"
  Scope: phrase

[O-004]
  Anchor: "Chat is scratch unless committed to artifacts"
  Scope: sentence

[O-005]
  Anchor: "A claim exists when it is written"
  Scope: sentence

[O-006]
  Anchor: "The second axiom is operator termination"
  Scope: sentence

[O-007]
  Anchor: "The operator is root"
  Scope: sentence

[O-008]
  Anchor: "crossing from proposal to commitment requires operator action"
  Scope: phrase

[O-009]
  Anchor: "The third axiom is port separation"
  Scope: sentence

[O-010]
  Anchor: "They do not share context"
  Scope: sentence

[O-011]
  Anchor: "The boundary localizes failure"
  Scope: sentence

[O-012]
  Anchor: "The spec is the interface between ports"
  Scope: sentence

[O-013]
  Anchor: "Friction is the return channel"
  Scope: sentence

[O-014]
  Anchor: "These three axioms compose"
  Scope: sentence

[R-001]
  Anchor: "the feeling that meaning is shared because it was once said"
  Scope: phrase

[R-002]
  Anchor: "Models fill gaps with plausible coherence"
  Scope: phrase

[R-003]
  Anchor: "Mixing them creates ambiguity about where problems originate"
  Scope: sentence

[C:cache]
  Anchor: "Model context windows behave like cache"
  Scope: phrase

[C:memory]
  Anchor: "Repo artifacts behave like memory"
  Scope: phrase

[C:operator]
  Anchor: "human operator"
  Scope: phrase

[C:port]
  Anchor: "Port separation is process isolation"
  Scope: phrase

[C:drift]
  Anchor: "semantic drift under iteration"
  Scope: phrase
