---
title: writeOS Ports
type: specification
format-version: 0.1
status: draft
created: 2026-01-11
copyright: Mikhail Shakhnazarov 2026
license: CC BY 4.0
---

## Body

A port is a constrained role with a contract. It is not a person, not a specific model, not a tool. It is a function that a runtime may perform if it obeys the contract. writeOS defines two ports: Port B for interpretation and Port A for execution.

Port B is the interpretation substrate. Its domain is meaning: understanding situations, surfacing assumptions, resolving ambiguity into explicit decisions, and encoding intent as executable requests. Port B thinks with the operator. It produces specs that Port A can execute without inventing meaning.

Port B must stabilize intent before handing off. This means clarifying scope, identifying constraints, surfacing tradeoffs, and making decisions explicit. Vague intent produces vague specs. Vague specs produce drift. Port B's discipline is to compress ambiguity into decision, not to smooth it into plausible prose.

Port B must write specs as structured requests. A spec is not good text; it is stable meaning encoded for execution. The spec must contain what Port A needs to proceed: summary, scope, requirements, interfaces, constraints, and verification criteria. Anything Port A would need to guess should be explicit in the spec.

Port B must mark unknowns as OPEN. When a decision has not been made, Port B does not close it by rhetorical smoothing. It marks it OPEN with a description and closure condition. Port A will friction on OPEN items rather than guess. This is the system preventing hidden state.

Port B must emit friction when decisions are missing. If the operator has not terminated a key branch and Port B cannot proceed without it, Port B creates a friction item. Friction is not failure; it is the correct representation of blocked state. Port B refuses to proceed when proceeding would require inventing authority.

Port B produces session briefs at session end. These are compressed memory: what happened, what was decided, what remains open, what comes next. Session briefs enable re-entry without transcript replay. They preserve the horizon under which work was meaningful.

Port A is the execution substrate. Its domain is implementation: taking specs and producing changes. Port A writes code, modifies files, runs commands, and reports results. Port A does not interpret; it executes.

Port A must read the spec as authoritative. The spec is the contract. Port A does not invent requirements that the spec does not contain. Port A does not interpret ambiguous language optimistically. Port A does not decide matters marked OPEN. If the spec says X, Port A does X. If the spec is silent, Port A does not improvise.

Port A must produce diffs and verification. A diff is an exact file change. Verification is evidence that the change does what the spec requires. Port A runs the checks specified in the spec and reports results. Output is not complete until verification is recorded.

Port A must emit friction on ambiguity. When Port A encounters something it cannot resolve from the spec, it does not guess. It writes a friction item: what is unclear, what is missing, what would resolve it. Then it stops that branch. It may continue unblocked branches if any exist. Friction routes to operator.

Port A must append changelog entries. Every execution produces a changelog entry: what changed, why, what spec clause it addresses, verification status, remaining friction. The changelog is the audit spine. It enables reconstruction of what happened without relying on memory.

Port A must consult patterns before writing. The pattern library captures recurring bugs and idioms. Port A checks relevant patterns before execution and updates them after encountering new issues. This is how the system learns across tasks.

The spec is the interface between ports. Port B produces it; operator approves it; Port A consumes it. The spec is a contract that creates accountability on both sides. If the spec is wrong, that is Port B's problem. If execution does not match the spec, that is Port A's problem. The boundary makes failure attributable.

Friction is the error channel. It is typed blocked state. Friction is not a complaint or a bug report. It is the system's formal representation of branching variety that requires closure. Friction items have structure: identifier, location, what is missing, options, impact, status. Friction routes to operator. Operator either decides or returns to Port B for elaboration.

The handoff sequence is explicit. Port B works with operator until design stabilizes. Port B drafts spec. Operator reviews and approves spec. Approved spec is published. Port A loads spec and executes. Port A produces diffs, verification, changelog, and possibly friction. Operator reviews results. If friction, operator decides or routes to Port B. The loop closes at operator.

Ports do not communicate directly. All coordination is through artifacts under operator authority. Port B does not send messages to Port A. Port A does not ask Port B questions. If Port A needs clarification, it emits friction. Operator receives friction and decides how to handle it. This ensures the operator remains in the loop for all significant decisions.

---

## Schema

[O-001] Port is constrained role
  Type: O-claim
  Summary: A port is a function with a contract, not a specific entity.

[O-002] Port B is interpretation substrate
  Type: O-claim
  Summary: Port B's domain is meaning, understanding, and specification.

[O-003] Port B stabilizes intent
  Type: O-claim
  Summary: Port B clarifies scope, constraints, and tradeoffs before handoff.
  Depends-on: [O-002]

[O-004] Port B writes specs
  Type: O-claim
  Summary: Port B encodes intent as structured executable requests.
  Depends-on: [O-002], [O-003]

[O-005] Port B marks OPEN items
  Type: O-claim
  Summary: Undecided matters are marked OPEN, not smoothed over.
  Depends-on: [O-002]

[O-006] Port B emits friction on missing decisions
  Type: O-claim
  Summary: Port B blocks and signals when operator decision is required.
  Depends-on: [O-002], [O-005]

[O-007] Port B produces session briefs
  Type: O-claim
  Summary: Compressed memory for re-entry without transcript replay.
  Depends-on: [O-002]

[O-008] Port A is execution substrate
  Type: O-claim
  Summary: Port A's domain is implementation and verification.

[O-009] Port A reads spec as authoritative
  Type: O-claim
  Summary: Port A executes what spec says, nothing more.
  Depends-on: [O-008]

[O-010] Port A does not invent requirements
  Type: O-claim
  Summary: Port A does not add what spec does not contain.
  Depends-on: [O-008], [O-009]

[O-011] Port A produces diffs and verification
  Type: O-claim
  Summary: Output is exact changes plus evidence of correctness.
  Depends-on: [O-008]

[O-012] Port A emits friction on ambiguity
  Type: O-claim
  Summary: Port A signals blockage rather than guessing.
  Depends-on: [O-008]

[O-013] Port A appends changelog
  Type: O-claim
  Summary: Every execution produces an audit record.
  Depends-on: [O-008], [O-011]

[O-014] Port A consults patterns
  Type: O-claim
  Summary: Pattern library is checked before and updated after execution.
  Depends-on: [O-008]

[O-015] Spec is the interface
  Type: O-claim
  Summary: The spec is the contract between Port B and Port A.
  Depends-on: [O-004], [O-009]

[O-016] Friction is the error channel
  Type: O-claim
  Summary: Friction formally represents blocked state requiring closure.
  Depends-on: [O-006], [O-012]

[O-017] Handoff sequence is explicit
  Type: O-claim
  Summary: B drafts, operator approves, A executes, operator reviews.
  Depends-on: [O-015]

[O-018] Ports do not communicate directly
  Type: O-claim
  Summary: All coordination is through artifacts under operator authority.
  Depends-on: [O-015], [O-016]

[R-001] Vague specs produce drift
  Type: R-claim
  Summary: Underspecified intent leads to execution that diverges from intent.
  Supports: [O-003], [O-004]

[R-002] Guessing introduces hidden state
  Type: R-claim
  Summary: Implicit decisions made during execution are not auditable.
  Supports: [O-010], [O-012]

[R-003] Boundary makes failure attributable
  Type: R-claim
  Summary: Separated ports enable identifying which side caused a problem.
  Supports: [O-015], [O-018]

[C:port-b] Port B
  Type: concept
  Definition: The interpretation substrate; produces specs from intent.

[C:port-a] Port A
  Type: concept
  Definition: The execution substrate; produces diffs from specs.

[C:spec] Spec
  Type: concept
  Definition: Structured request encoding intent for execution.

[C:friction] Friction
  Type: concept
  Definition: Typed blocked state requiring operator decision.

[C:session-brief] Session brief
  Type: concept
  Definition: Compressed memory enabling re-entry without transcript replay.

[C:changelog] Changelog
  Type: concept
  Definition: Append-only audit record of execution.

[C:handoff] Handoff
  Type: concept
  Definition: Transfer from Port B to Port A via operator-approved spec.

---

## Binding

[O-001]
  Anchor: "A port is a constrained role with a contract"
  Scope: sentence

[O-002]
  Anchor: "Port B is the interpretation substrate"
  Scope: sentence

[O-003]
  Anchor: "Port B must stabilize intent before handing off"
  Scope: sentence

[O-004]
  Anchor: "Port B must write specs as structured requests"
  Scope: sentence

[O-005]
  Anchor: "Port B must mark unknowns as OPEN"
  Scope: sentence

[O-006]
  Anchor: "Port B must emit friction when decisions are missing"
  Scope: sentence

[O-007]
  Anchor: "Port B produces session briefs at session end"
  Scope: sentence

[O-008]
  Anchor: "Port A is the execution substrate"
  Scope: sentence

[O-009]
  Anchor: "Port A must read the spec as authoritative"
  Scope: sentence

[O-010]
  Anchor: "Port A does not invent requirements"
  Scope: phrase

[O-011]
  Anchor: "Port A must produce diffs and verification"
  Scope: sentence

[O-012]
  Anchor: "Port A must emit friction on ambiguity"
  Scope: sentence

[O-013]
  Anchor: "Port A must append changelog entries"
  Scope: sentence

[O-014]
  Anchor: "Port A must consult patterns before writing"
  Scope: sentence

[O-015]
  Anchor: "The spec is the interface between ports"
  Scope: sentence

[O-016]
  Anchor: "Friction is the error channel"
  Scope: sentence

[O-017]
  Anchor: "The handoff sequence is explicit"
  Scope: sentence

[O-018]
  Anchor: "Ports do not communicate directly"
  Scope: sentence

[R-001]
  Anchor: "Vague specs produce drift"
  Scope: phrase

[R-002]
  Anchor: "it does not guess"
  Scope: phrase

[R-003]
  Anchor: "The boundary makes failure attributable"
  Scope: sentence

[C:port-b]
  Anchor: "Port B thinks with the operator"
  Scope: phrase

[C:port-a]
  Anchor: "Port A writes code, modifies files, runs commands"
  Scope: phrase

[C:spec]
  Anchor: "A spec is not good text; it is stable meaning encoded for execution"
  Scope: sentence

[C:friction]
  Anchor: "Friction is not a complaint or a bug report"
  Scope: sentence

[C:session-brief]
  Anchor: "compressed memory: what happened, what was decided"
  Scope: phrase

[C:changelog]
  Anchor: "The changelog is the audit spine"
  Scope: sentence

[C:handoff]
  Anchor: "Port B works with operator until design stabilizes"
  Scope: sentence
