---
title: writeOS Artifacts
type: specification
format-version: 0.1
status: draft
created: 2026-01-11
copyright: Mikhail Shakhnazarov 2026
license: CC BY 4.0
---

## Body

The artifact ABI defines the shapes that system components must respect so that work composes across tools, sessions, and time. writeOS runs on artifacts, not on transcript replay. The ABI is the interface layer that makes this possible.

The kernel is the minimal invariant set. It contains what must remain true for the system to function: axioms, port contracts, artifact shapes, and refusal rules. The kernel must stay short. If it grows too large, it becomes unloadable, and the system reverts to ad-hoc behavior. Kernel changes are rare and require explicit justification.

The kernel is not documentation. It is the constitution. Runtime documents reference it. Behavior that contradicts it is a violation. The kernel defines the game; everything else plays within its rules.

now.md is the process table and boot surface. On cold start, loading now.md should yield the next correct action quickly. It shows current project state, active tasks, blockers, and pointers to relevant artifacts. now.md is the operator's entry point after any time gap.

now.md must be current. Stale now.md causes wrong moves. After any material state change, now.md should be updated. The discipline is: if someone read only now.md, would they know what to do next? If not, now.md is incomplete.

Specs are structured requests from Port B to Port A. A spec is the syscall analogy: a standardized interface for asking execution to perform changes. Specs have required structure: summary, scope (in and out), requirements (must, should, may), interfaces, constraints, OPEN items, and verification criteria.

The spec must be precise enough that Port A can execute without inventing meaning. Ambiguity in the spec becomes friction at execution. The spec is a contract: Port B commits to what it says, Port A commits to implementing what it says and only what it says.

OPEN items in specs mark decisions not yet made. They have a description and a closure condition. Port A does not resolve OPEN items; it frictions on them. This prevents hidden assumptions from entering execution.

Specs have lifecycle status: draft, active, superseded, archived. Draft specs are not yet approved for execution. Active specs are the current contract. Superseded specs have been replaced by newer versions. Archived specs are historical record. Status must be explicit.

The friction log records blocked state. Each friction item has structure: identifier, pointer to source, what is missing, options if known, impact, status, and resolution when closed. Friction is not a bug tracker. It is the system's representation of decisions that must be made before work can proceed.

Friction items route to operator. Operator either decides directly or sends to Port B for elaboration. Closing a friction item means making the decision and recording the resolution. Friction that remains open blocks dependent work.

The changelog is the append-only audit spine. Each entry records: what changed, why (spec reference), verification status, remaining friction, and session pointer. The changelog enables reconstruction of project history without relying on memory.

Changelog entries are not summaries. They are structured records. The discipline is: given only the changelog, could someone understand what happened and why? If the changelog omits key information, the audit trail is broken.

Session briefs are compressed memory. They are written at session end to enable re-entry without reading the full transcript. A session brief contains: intent, actions taken, outcomes, decisions made, diff summary, verification results, remaining friction, and next pointers.

Session briefs must preserve the horizon. They record not just what happened but why choices were made. Without rationale, future sessions reinterpret past work under different assumptions, and drift enters.

Patterns capture recurring pitfalls and idioms. The pattern library accumulates across projects. Port A consults patterns before execution and updates them after encountering issues. High-frequency patterns may warrant tooling or automation.

Patterns are structured: identifier, description, fix, count. The count tracks how often the pattern has been encountered. Rising counts signal systemic issues that may need architectural attention.

Packs are curated working sets. A pack defines what artifacts to load for a specific operation. Packs manage context: instead of loading everything, load what is relevant. This prevents context overflow and keeps operations bounded.

The hot set is the always-loaded minimum: kernel and now.md. These must load on every boot. The hot set must stay small enough to actually load under any conditions.

The warm set is the per-task working set: spec, relevant source files, recent changelog, relevant friction. A task pack specifies exactly what enters context for that task.

The cold set is archival: old sessions, superseded specs, resolved friction. Cold artifacts are retrievable but not loaded by default.

Pack discipline prevents two failure modes. Loading too little causes Port A to guess or friction unnecessarily. Loading too much causes context overflow and attention dilution. Packs are the tuning mechanism.

---

## Schema

[O-001] ABI defines artifact shapes
  Type: O-claim
  Summary: The ABI specifies required structure so components compose.

[O-002] Kernel is minimal invariant set
  Type: O-claim
  Summary: Kernel contains only what must remain true for system function.

[O-003] Kernel must stay short
  Type: O-claim
  Summary: Unloadable kernel causes reversion to ad-hoc behavior.
  Depends-on: [O-002]

[O-004] Kernel is constitution
  Type: O-claim
  Summary: Runtime documents reference kernel; contradictions are violations.
  Depends-on: [O-002]

[O-005] now.md is boot surface
  Type: O-claim
  Summary: Loading now.md yields next correct action on cold start.

[O-006] now.md must be current
  Type: O-claim
  Summary: Stale now.md causes wrong moves.
  Depends-on: [O-005]

[O-007] Specs are structured requests
  Type: O-claim
  Summary: Specs have required structure enabling execution without invention.

[O-008] Spec structure is defined
  Type: O-claim
  Summary: Summary, scope, requirements, interfaces, constraints, OPEN, verification.
  Depends-on: [O-007]

[O-009] OPEN items mark undecided matters
  Type: O-claim
  Summary: Port A frictions on OPEN items rather than resolving them.
  Depends-on: [O-007]

[O-010] Specs have lifecycle status
  Type: O-claim
  Summary: Draft, active, superseded, archived -- status must be explicit.
  Depends-on: [O-007]

[O-011] Friction log records blocked state
  Type: O-claim
  Summary: Friction items have structure and route to operator.

[O-012] Friction item structure
  Type: O-claim
  Summary: Identifier, source, missing element, options, impact, status, resolution.
  Depends-on: [O-011]

[O-013] Changelog is append-only audit
  Type: O-claim
  Summary: Changelog enables reconstruction without relying on memory.

[O-014] Changelog entries are structured
  Type: O-claim
  Summary: What, why, verification, friction, session pointer.
  Depends-on: [O-013]

[O-015] Session briefs are compressed memory
  Type: O-claim
  Summary: Briefs enable re-entry without transcript replay.

[O-016] Briefs preserve horizon
  Type: O-claim
  Summary: Briefs record rationale, not just actions.
  Depends-on: [O-015]

[O-017] Patterns capture recurring issues
  Type: O-claim
  Summary: Pattern library accumulates across projects.

[O-018] Patterns are structured
  Type: O-claim
  Summary: Identifier, description, fix, count.
  Depends-on: [O-017]

[O-019] Packs are curated working sets
  Type: O-claim
  Summary: Packs define what artifacts to load for an operation.

[O-020] Hot set is always-loaded minimum
  Type: O-claim
  Summary: Kernel and now.md must load on every boot.
  Depends-on: [O-019]

[O-021] Warm set is per-task working set
  Type: O-claim
  Summary: Task pack specifies what enters context for that task.
  Depends-on: [O-019]

[O-022] Cold set is archival
  Type: O-claim
  Summary: Old artifacts are retrievable but not loaded by default.
  Depends-on: [O-019]

[R-001] Transcript replay does not scale
  Type: R-claim
  Summary: Re-reading full conversations is prohibitively expensive.
  Supports: [O-001], [O-015]

[R-002] Context overflow dilutes attention
  Type: R-claim
  Summary: Loading too much impairs model performance.
  Supports: [O-019]

[C:abi] ABI
  Type: concept
  Definition: Required artifact shapes enabling composition across tools.

[C:kernel] Kernel
  Type: concept
  Definition: Minimal invariant set; the system's constitution.

[C:now] now.md
  Type: concept
  Definition: Process table and boot surface; entry point after time gap.

[C:spec] Spec
  Type: concept
  Definition: Structured request from Port B to Port A.

[C:friction-log] Friction log
  Type: concept
  Definition: Record of blocked state requiring operator decision.

[C:changelog] Changelog
  Type: concept
  Definition: Append-only audit record of execution history.

[C:session-brief] Session brief
  Type: concept
  Definition: Compressed memory enabling re-entry.

[C:pattern] Pattern
  Type: concept
  Definition: Recurring pitfall or idiom captured for reuse.

[C:pack] Pack
  Type: concept
  Definition: Curated working set defining what to load.

[C:hot-set] Hot set
  Type: concept
  Definition: Always-loaded minimum (kernel, now.md).

---

## Binding

[O-001]
  Anchor: "The artifact ABI defines the shapes"
  Scope: sentence

[O-002]
  Anchor: "The kernel is the minimal invariant set"
  Scope: sentence

[O-003]
  Anchor: "The kernel must stay short"
  Scope: sentence

[O-004]
  Anchor: "The kernel is not documentation"
  Scope: sentence

[O-005]
  Anchor: "now.md is the process table and boot surface"
  Scope: sentence

[O-006]
  Anchor: "now.md must be current"
  Scope: sentence

[O-007]
  Anchor: "Specs are structured requests from Port B to Port A"
  Scope: sentence

[O-008]
  Anchor: "summary, scope (in and out), requirements (must, should, may)"
  Scope: phrase

[O-009]
  Anchor: "OPEN items in specs mark decisions not yet made"
  Scope: sentence

[O-010]
  Anchor: "Specs have lifecycle status"
  Scope: sentence

[O-011]
  Anchor: "The friction log records blocked state"
  Scope: sentence

[O-012]
  Anchor: "identifier, pointer to source, what is missing"
  Scope: phrase

[O-013]
  Anchor: "The changelog is the append-only audit spine"
  Scope: sentence

[O-014]
  Anchor: "what changed, why (spec reference), verification status"
  Scope: phrase

[O-015]
  Anchor: "Session briefs are compressed memory"
  Scope: sentence

[O-016]
  Anchor: "Session briefs must preserve the horizon"
  Scope: sentence

[O-017]
  Anchor: "Patterns capture recurring pitfalls and idioms"
  Scope: sentence

[O-018]
  Anchor: "identifier, description, fix, count"
  Scope: phrase

[O-019]
  Anchor: "Packs are curated working sets"
  Scope: sentence

[O-020]
  Anchor: "The hot set is the always-loaded minimum"
  Scope: sentence

[O-021]
  Anchor: "The warm set is the per-task working set"
  Scope: sentence

[O-022]
  Anchor: "The cold set is archival"
  Scope: sentence

[R-001]
  Anchor: "without reading the full transcript"
  Scope: phrase

[R-002]
  Anchor: "context overflow and attention dilution"
  Scope: phrase

[C:abi]
  Anchor: "so that work composes across tools, sessions, and time"
  Scope: phrase

[C:kernel]
  Anchor: "It is the constitution"
  Scope: sentence

[C:now]
  Anchor: "the operator's entry point after any time gap"
  Scope: phrase

[C:spec]
  Anchor: "the syscall analogy"
  Scope: phrase

[C:friction-log]
  Anchor: "Friction is not a bug tracker"
  Scope: sentence

[C:changelog]
  Anchor: "enables reconstruction of project history"
  Scope: phrase

[C:session-brief]
  Anchor: "enable re-entry without reading the full transcript"
  Scope: phrase

[C:pattern]
  Anchor: "The pattern library accumulates across projects"
  Scope: sentence

[C:pack]
  Anchor: "A pack defines what artifacts to load"
  Scope: sentence

[C:hot-set]
  Anchor: "kernel and now.md"
  Scope: phrase
