---
title: writeOS Protocols
type: specification
format-version: 0.1
status: draft
created: 2026-01-11
copyright: Mikhail Shakhnazarov 2026
license: CC BY 4.0
---

## Body

Protocols define how the system operates. They sequence actions, specify preconditions, and establish what counts as completion. Protocols convert architectural commitments into repeatable procedure.

The boot protocol establishes correct state on cold start. Load kernel first. The kernel defines what is invariant; loading it first prevents category errors. Load now.md second. now.md shows current state and next action. Load the relevant task pack third. The task pack brings in what is needed for the specific operation.

If anything required is missing during boot, emit friction. Do not improvise. Missing kernel is a system error. Missing now.md requires reconstruction. Missing pack components require either retrieval or explicit acknowledgment of reduced context. Boot must succeed cleanly or surface problems immediately.

The re-entry protocol handles time gaps. After any significant time away, re-entry follows boot protocol plus additional steps. Load the last session brief. The brief restores context: what happened, what was decided, what remains. Verify that now.md reflects the brief. If they diverge, reconcile before proceeding.

Re-entry friction is real. Cognitive state on return is not the same as state at session end. The system is designed to minimize re-entry cost by externalizing context into artifacts. But the operator must still perform the re-entry ritual: read, orient, then act.

The Port B workflow structures interpretation. Operator engages Port B with a situation, question, or goal. Port B clarifies: what is being asked, what constraints apply, what is already decided. Port B surfaces options, tradeoffs, failure modes. Port B and operator iterate until intent is stable.

When design stabilizes, Port B drafts a spec. The spec captures the stable intent in executable form. Operator reviews the spec. If the spec is incomplete or incorrect, iterate. If the spec is acceptable, operator approves. Approval transitions the spec from draft to active. Active specs are contracts.

Port B produces a session brief before ending. The brief captures what happened in the session: intent, analysis, decisions, outcomes, next steps. Without a brief, the session's value exists only in transcript, which is expensive to replay.

The Port A workflow structures execution. Port A loads the active spec. Port A loads the task pack: source files, recent changelog, relevant patterns. Port A executes according to the spec.

During execution, Port A produces diffs. Each change to a file is a diff. Diffs are concrete; they show exactly what changed. Port A runs verification as specified: tests, checks, manual review criteria. Results are recorded.

Port A appends a changelog entry. The entry records what changed, why, verification status, and any friction. If friction arose, the changelog notes it. The changelog is the primary record of what happened during execution.

If Port A encounters ambiguity, it emits friction. Friction items describe what is unclear and what would resolve it. Port A stops the blocked branch. If unblocked branches remain, Port A may continue those. At execution end, all friction routes to operator.

The handoff protocol coordinates transitions between ports. Port B completes work and produces a draft spec. Operator reviews draft. If acceptable, operator approves spec, transitioning it to active. Operator makes the approved spec available to Port A.

Port A loads the active spec and executes. Port A produces results: diffs, verification, changelog, and possibly friction. Operator reviews results. If friction exists, operator decides: resolve directly, return to Port B for elaboration, or defer.

The handoff is explicit at every transition. Port B to operator: draft spec ready for review. Operator to Port A: approved spec ready for execution. Port A to operator: results ready for review. No transition happens implicitly. The operator is always in the loop.

The definition of DONE is explicit and auditable. A task is DONE when: requirements are satisfied or explicitly deferred, verification has run and is recorded, diffs exist, a changelog entry is appended, a session brief exists, and now.md points to the next correct action.

DONE is not a feeling. It is a checklist of observable states. If any condition is missing, the task is not DONE regardless of how complete it seems. This prevents drift-by-declaration, where work is called complete without meeting criteria.

The commit cadence governs when work enters artifacts. When a requirement or decision appears, commit to the active spec immediately. Delaying commitment risks losing the decision to context churn. When ambiguity appears, create a friction item immediately. Delaying friction lets ambiguity propagate. When a session ends, write brief, append changelog, update now.md. These commits preserve what would otherwise exist only in volatile state.

Commit discipline converts cache to memory. Without it, meaning lives in conversation and dies with context. With it, meaning accumulates in artifacts that survive time, tool changes, and attention shifts.

---

## Schema

[O-001] Boot protocol sequence
  Type: O-claim
  Summary: Load kernel, then now.md, then task pack.

[O-002] Boot emits friction on missing components
  Type: O-claim
  Summary: Missing required artifacts surface immediately, not improvised.
  Depends-on: [O-001]

[O-003] Re-entry protocol extends boot
  Type: O-claim
  Summary: After time gaps, load session brief and verify now.md alignment.

[O-004] Re-entry ritual required
  Type: O-claim
  Summary: Operator must read, orient, then act after returning.
  Depends-on: [O-003]

[O-005] Port B workflow structures interpretation
  Type: O-claim
  Summary: Clarify, surface options, iterate until intent stable, draft spec.

[O-006] Design stabilization triggers spec drafting
  Type: O-claim
  Summary: Spec is drafted when intent is stable, not before.
  Depends-on: [O-005]

[O-007] Operator approval activates spec
  Type: O-claim
  Summary: Approval transitions spec from draft to active.
  Depends-on: [O-006]

[O-008] Port B produces session brief
  Type: O-claim
  Summary: Brief captures session value for future re-entry.
  Depends-on: [O-005]

[O-009] Port A workflow structures execution
  Type: O-claim
  Summary: Load spec, load pack, execute, produce diffs and verification.

[O-010] Port A produces diffs
  Type: O-claim
  Summary: Each file change is a concrete diff showing what changed.
  Depends-on: [O-009]

[O-011] Port A runs verification
  Type: O-claim
  Summary: Tests and checks run as specified; results recorded.
  Depends-on: [O-009]

[O-012] Port A appends changelog
  Type: O-claim
  Summary: Execution produces audit record.
  Depends-on: [O-009]

[O-013] Port A emits friction on ambiguity
  Type: O-claim
  Summary: Unclear situations produce friction, not guesses.
  Depends-on: [O-009]

[O-014] Handoff protocol coordinates transitions
  Type: O-claim
  Summary: Explicit handoffs at each port-operator boundary.

[O-015] No implicit transitions
  Type: O-claim
  Summary: Every transition requires explicit operator action.
  Depends-on: [O-014]

[O-016] DONE definition is explicit
  Type: O-claim
  Summary: Requirements met, verification recorded, diffs exist, changelog appended, brief exists, now.md updated.

[O-017] DONE is observable checklist
  Type: O-claim
  Summary: DONE is states, not feeling.
  Depends-on: [O-016]

[O-018] Commit cadence specified
  Type: O-claim
  Summary: Decisions commit immediately; friction commits immediately; session end commits brief, changelog, now.md.

[O-019] Commit converts cache to memory
  Type: O-claim
  Summary: Without commit, meaning dies with context.
  Depends-on: [O-018]

[R-001] Re-entry cost is real
  Type: R-claim
  Summary: Cognitive state on return differs from state at session end.
  Supports: [O-003], [O-004]

[R-002] Drift-by-declaration
  Type: R-claim
  Summary: Work called complete without meeting criteria causes drift.
  Supports: [O-016], [O-017]

[R-003] Delayed commitment loses decisions
  Type: R-claim
  Summary: Context churn erases uncommitted decisions.
  Supports: [O-018]

[C:boot] Boot protocol
  Type: concept
  Definition: Sequence establishing correct state on cold start.

[C:re-entry] Re-entry protocol
  Type: concept
  Definition: Boot plus session brief loading after time gaps.

[C:port-b-workflow] Port B workflow
  Type: concept
  Definition: Interpretation sequence ending in spec draft.

[C:port-a-workflow] Port A workflow
  Type: concept
  Definition: Execution sequence ending in diffs, verification, changelog.

[C:handoff] Handoff protocol
  Type: concept
  Definition: Explicit transitions between ports via operator.

[C:done] Definition of DONE
  Type: concept
  Definition: Auditable checklist of completion conditions.

[C:commit-cadence] Commit cadence
  Type: concept
  Definition: When work enters artifacts.

---

## Binding

[O-001]
  Anchor: "Load kernel first"
  Scope: sentence

[O-002]
  Anchor: "If anything required is missing during boot, emit friction"
  Scope: sentence

[O-003]
  Anchor: "The re-entry protocol handles time gaps"
  Scope: sentence

[O-004]
  Anchor: "the operator must still perform the re-entry ritual"
  Scope: phrase

[O-005]
  Anchor: "The Port B workflow structures interpretation"
  Scope: sentence

[O-006]
  Anchor: "When design stabilizes, Port B drafts a spec"
  Scope: sentence

[O-007]
  Anchor: "Approval transitions the spec from draft to active"
  Scope: sentence

[O-008]
  Anchor: "Port B produces a session brief before ending"
  Scope: sentence

[O-009]
  Anchor: "The Port A workflow structures execution"
  Scope: sentence

[O-010]
  Anchor: "Port A produces diffs"
  Scope: sentence

[O-011]
  Anchor: "Port A runs verification as specified"
  Scope: sentence

[O-012]
  Anchor: "Port A appends a changelog entry"
  Scope: sentence

[O-013]
  Anchor: "If Port A encounters ambiguity, it emits friction"
  Scope: sentence

[O-014]
  Anchor: "The handoff protocol coordinates transitions"
  Scope: sentence

[O-015]
  Anchor: "No transition happens implicitly"
  Scope: sentence

[O-016]
  Anchor: "The definition of DONE is explicit and auditable"
  Scope: sentence

[O-017]
  Anchor: "DONE is not a feeling"
  Scope: sentence

[O-018]
  Anchor: "The commit cadence governs when work enters artifacts"
  Scope: sentence

[O-019]
  Anchor: "Commit discipline converts cache to memory"
  Scope: sentence

[R-001]
  Anchor: "Re-entry friction is real"
  Scope: sentence

[R-002]
  Anchor: "drift-by-declaration"
  Scope: phrase

[R-003]
  Anchor: "Delaying commitment risks losing the decision"
  Scope: phrase

[C:boot]
  Anchor: "The boot protocol establishes correct state on cold start"
  Scope: sentence

[C:re-entry]
  Anchor: "After any significant time away"
  Scope: phrase

[C:port-b-workflow]
  Anchor: "Operator engages Port B with a situation"
  Scope: phrase

[C:port-a-workflow]
  Anchor: "Port A loads the active spec"
  Scope: sentence

[C:handoff]
  Anchor: "The handoff is explicit at every transition"
  Scope: sentence

[C:done]
  Anchor: "checklist of observable states"
  Scope: phrase

[C:commit-cadence]
  Anchor: "When a requirement or decision appears, commit"
  Scope: phrase
