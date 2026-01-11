---
title: writeOS Governance
type: specification
format-version: 0.1
status: draft
created: 2026-01-11
copyright: Mikhail Shakhnazarov 2026
license: CC BY 4.0
---

## Body

Governance defines who may decide what. writeOS distributes authority across levels and constrains each level's scope. This prevents two failure modes: micromanagement, where the operator decides everything, and authority drift, where lower levels silently assume decision power.

The authority ladder has five levels. Each level has a scope and a change frequency. Higher levels are more stable; lower levels change more often. Decisions should be made at the lowest competent level. This is subsidiarity: push decisions down unless they require higher authority.

Level zero is the kernel. It contains the system's invariants: axioms, port contracts, artifact shapes, and refusal rules. Kernel changes are paradigm shifts. They require explicit justification, proposal, review, and logging. The kernel changes rarely because it defines what the system is. A kernel that changes frequently is not a kernel; it is policy pretending to be constitution.

Level one is doctrine. It contains operating principles: style constraints, safety boundaries, evidence standards, and standard workflows. Doctrine can evolve more often than kernel, but changes still demand discipline. Doctrine shapes how work is done; it should not change casually.

Level two is project policy. It contains project-specific constraints: target users, architecture rules, dependencies, acceptance criteria. Each project may have its own policy. Project policy should not contradict kernel or doctrine. If it seems to need to, that is a signal to revisit kernel or doctrine.

Level three is the task spec. It contains scope, requirements, and verification for a single operation. Specs change frequently; that is their nature. But spec changes should be logged. A spec that silently mutates is not a contract.

Level four is execution. It contains the diffs and commands that implement a spec. Execution is the most volatile level. Changes here are expected and frequent. But execution must not alter higher levels without explicit escalation.

Subsidiarity governs who decides. Decisions should be made at the lowest level that has the necessary context and authority. A decision about how to implement a function is level four; Port A may decide. A decision about what the function should do is level three; it belongs in the spec. A decision about project architecture is level two; it requires project policy. A decision about how the system operates is level one or zero; it requires doctrine or kernel change.

What Port A may decide: implementation details fully within spec scope. Mechanical refactoring that preserves behavior. Choosing between equivalent options explicitly permitted by the spec. Trivial formatting adjustments required by lint rules specified in the spec. These are local decisions with no policy implications.

What Port A may not decide: anything that changes scope, semantics, public behavior, or constraints from level two or above. If a decision would alter what the spec means or what the project requires, Port A must escalate via friction. Convenience is not a justification for silent scope expansion.

What Port B may decide: interpretation of ambiguous situations within project policy. Framing of problems and options. Structure of specs. Recommendations to operator. These are meaning decisions within delegated authority.

What Port B may not decide: closing OPEN items without operator termination. Changing kernel or doctrine. Overriding explicit project policy. Port B may propose any of these, but proposals require operator decision. Port B's authority is interpretive, not constitutional.

The operator decides: everything that requires termination. OPEN item closure. Spec approval. Friction resolution. Project policy changes. Doctrine changes. Kernel changes. The operator is root. This is not because the operator is infallible, but because accountability requires a locus.

Kernel change control is a specific protocol. A recurring anomaly is observed. The anomaly is logged as a pattern. When the pattern is significant, a kernel change proposal is drafted. The proposal includes: motivation, the specific change, alternatives considered, expected effects, risks, and migration steps.

The operator reviews the proposal. If accepted, the change is applied to kernel. The changelog records the new kernel version and the reason. Previous kernel version is preserved for reference. This protocol ensures kernel changes are deliberate, documented, and reversible.

Doctrine changes follow a lighter version of the same protocol. A proposal, a rationale, operator approval, changelog entry. Doctrine is more malleable than kernel but still requires explicit change.

Escalation via friction is the upward channel. When a lower level cannot proceed without a decision from a higher level, it emits friction. Friction describes what is blocked, what is needed, and what level can resolve it. Friction routes to operator. Operator either decides directly or delegates to the appropriate level.

Friction is not failure. It is the system working correctly. A system that never emits friction is either trivially simple or silently drifting. Friction makes blocked state visible. Visible blocked state can be managed.

Governance failure modes exist. Bureaucracy drift: the system generates artifacts for their own sake. Counter: strict thresholds for what requires full process. Authority drift: lower levels start making constitutional decisions because it is convenient. Counter: explicit authority ladder and escalation protocol. Over-centralization: everything escalates to operator, creating a bottleneck. Counter: subsidiarity and explicit delegation.

The governance goal is not control for its own sake. It is clarity about who may decide what, so that decisions are made at the right level, by the right authority, with the right documentation. This supports accountability, reversibility, and coherence over time.

---

## Schema

[O-001] Authority ladder exists
  Type: O-claim
  Summary: Five levels from kernel to execution, each with defined scope.

[O-002] Level zero is kernel
  Type: O-claim
  Summary: Invariants, axioms, port contracts. Rarely changes.
  Depends-on: [O-001]

[O-003] Level one is doctrine
  Type: O-claim
  Summary: Operating principles. Changes demand discipline.
  Depends-on: [O-001]

[O-004] Level two is project policy
  Type: O-claim
  Summary: Project-specific constraints. Per-project.
  Depends-on: [O-001]

[O-005] Level three is task spec
  Type: O-claim
  Summary: Scope and requirements for single operation. Changes frequently.
  Depends-on: [O-001]

[O-006] Level four is execution
  Type: O-claim
  Summary: Diffs and commands. Most volatile.
  Depends-on: [O-001]

[O-007] Subsidiarity principle
  Type: O-claim
  Summary: Decisions at lowest competent level.

[O-008] Port A local decisions
  Type: O-claim
  Summary: Port A may decide implementation details within spec scope.
  Depends-on: [O-006], [O-007]

[O-009] Port A escalation requirement
  Type: O-claim
  Summary: Port A must friction on decisions affecting level two or above.
  Depends-on: [O-006], [O-007]

[O-010] Port B interpretive authority
  Type: O-claim
  Summary: Port B may decide interpretation within project policy.
  Depends-on: [O-004], [O-007]

[O-011] Port B cannot close OPEN items
  Type: O-claim
  Summary: OPEN closure requires operator termination.
  Depends-on: [O-010]

[O-012] Operator is root
  Type: O-claim
  Summary: Operator decides all matters requiring termination.

[O-013] Kernel change control protocol
  Type: O-claim
  Summary: Anomaly, pattern, proposal, review, apply, log.

[O-014] Proposal structure
  Type: O-claim
  Summary: Motivation, change, alternatives, effects, risks, migration.
  Depends-on: [O-013]

[O-015] Kernel changes are logged
  Type: O-claim
  Summary: Changelog records version and reason; previous version preserved.
  Depends-on: [O-013]

[O-016] Doctrine change protocol
  Type: O-claim
  Summary: Lighter version of kernel change: proposal, rationale, approval, log.
  Depends-on: [O-003]

[O-017] Escalation via friction
  Type: O-claim
  Summary: Lower levels emit friction when higher-level decision needed.

[O-018] Friction routes to operator
  Type: O-claim
  Summary: Operator decides or delegates.
  Depends-on: [O-017]

[O-019] Friction is not failure
  Type: O-claim
  Summary: Friction is the system working correctly.
  Depends-on: [O-017]

[R-001] Micromanagement failure mode
  Type: R-claim
  Summary: Operator deciding everything creates bottleneck.
  Supports: [O-007]

[R-002] Authority drift failure mode
  Type: R-claim
  Summary: Lower levels silently assuming decision power causes hidden state.
  Supports: [O-009], [O-017]

[R-003] Bureaucracy drift failure mode
  Type: R-claim
  Summary: Generating artifacts for their own sake.
  Supports: [O-001]

[C:authority-ladder] Authority ladder
  Type: concept
  Definition: Five levels from kernel to execution with defined scope.

[C:subsidiarity] Subsidiarity
  Type: concept
  Definition: Decisions at lowest competent level.

[C:kernel-change] Kernel change control
  Type: concept
  Definition: Protocol for modifying system invariants.

[C:escalation] Escalation
  Type: concept
  Definition: Upward routing of decisions via friction.

[C:delegation] Delegation
  Type: concept
  Definition: Operator granting decision authority to lower level.

---

## Binding

[O-001]
  Anchor: "The authority ladder has five levels"
  Scope: sentence

[O-002]
  Anchor: "Level zero is the kernel"
  Scope: sentence

[O-003]
  Anchor: "Level one is doctrine"
  Scope: sentence

[O-004]
  Anchor: "Level two is project policy"
  Scope: sentence

[O-005]
  Anchor: "Level three is the task spec"
  Scope: sentence

[O-006]
  Anchor: "Level four is execution"
  Scope: sentence

[O-007]
  Anchor: "Subsidiarity governs who decides"
  Scope: sentence

[O-008]
  Anchor: "What Port A may decide"
  Scope: sentence

[O-009]
  Anchor: "What Port A may not decide"
  Scope: sentence

[O-010]
  Anchor: "What Port B may decide"
  Scope: sentence

[O-011]
  Anchor: "What Port B may not decide"
  Scope: sentence

[O-012]
  Anchor: "The operator decides"
  Scope: sentence

[O-013]
  Anchor: "Kernel change control is a specific protocol"
  Scope: sentence

[O-014]
  Anchor: "motivation, the specific change, alternatives considered"
  Scope: phrase

[O-015]
  Anchor: "The changelog records the new kernel version"
  Scope: sentence

[O-016]
  Anchor: "Doctrine changes follow a lighter version"
  Scope: sentence

[O-017]
  Anchor: "Escalation via friction is the upward channel"
  Scope: sentence

[O-018]
  Anchor: "Friction routes to operator"
  Scope: sentence

[O-019]
  Anchor: "Friction is not failure"
  Scope: sentence

[R-001]
  Anchor: "micromanagement, where the operator decides everything"
  Scope: phrase

[R-002]
  Anchor: "authority drift, where lower levels silently assume decision power"
  Scope: phrase

[R-003]
  Anchor: "Bureaucracy drift: the system generates artifacts for their own sake"
  Scope: sentence

[C:authority-ladder]
  Anchor: "Each level has a scope and a change frequency"
  Scope: sentence

[C:subsidiarity]
  Anchor: "push decisions down unless they require higher authority"
  Scope: phrase

[C:kernel-change]
  Anchor: "A recurring anomaly is observed"
  Scope: sentence

[C:escalation]
  Anchor: "When a lower level cannot proceed without a decision"
  Scope: phrase

[C:delegation]
  Anchor: "Operator either decides directly or delegates"
  Scope: phrase
