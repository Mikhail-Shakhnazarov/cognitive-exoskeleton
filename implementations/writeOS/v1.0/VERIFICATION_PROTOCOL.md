---
title: Verification Protocol
type: protocol-specification
format-version: 0.1
status: draft
created: 2026-01-11
copyright: Mikhail Shakhnazarov 2026
license: CC BY 4.0
---

## Body

Verification is coherence checking across the three layers of a mapped prose document. The body, schema, and binding must agree. Disagreement is drift. The protocol makes drift detectable and locatable.

Schema completeness is the first check. Every entity in the schema must have required fields: identifier, type, and summary for claims; identifier, type, and definition for concepts. Relations must reference existing entities. Missing fields are structural errors.

Binding coverage is the second check. Every entity in the schema must have a corresponding binding entry. An entity without a binding cannot be located. This is not a style violation; it breaks the format's promise. The schema-binding relationship is one-to-one.

Anchor grounding is the third check. Every anchor phrase in the binding must exist in the body. Search the body for the anchor text. If it does not appear, the binding is stale or the body has drifted. This is the most common failure mode under editing.

Anchor uniqueness is the fourth check. Each anchor phrase must appear exactly once in the body. If an anchor matches multiple locations, the binding is ambiguous. If an anchor matches zero locations, the binding is broken. Both are failures.

Relation validity is the fifth check. Every relation in the schema must reference entities that exist in the schema. A depends-on relation pointing to a non-existent claim is a dangling reference. This check is internal to the schema.

Type consistency is the sixth check. Entities must be typed correctly. An O-claim asserts a design decision; an R-claim asserts an empirical observation. Conflating these corrupts verification authority. The type determines who or what can verify the claim.

These checks compose into a verification pass. Run all six. Collect failures. Each failure is a friction item with specific location: which entity, which check, what is wrong. Friction enables targeted repair.

Verification is not validation. It does not assess whether claims are true, whether prose is good, or whether the document achieves its purpose. It assesses only whether the three layers are internally coherent. A coherent document can still be wrong. An incoherent document cannot be trusted even if parts are right.

Two verification modes serve different purposes. Full verification runs all checks, produces a complete report, suits periodic review or post-edit confirmation. Incremental verification checks only changed entities after a patch, suits rapid iteration. The protocol supports both.

Verification produces a report. The report lists: checks run, entities examined, failures found, friction items generated. A clean report means the document is coherent. A report with failures means specific repairs are needed. The report is itself prose, readable by operator, parseable by tooling.

Repair follows verification. For each friction item, determine cause: body drifted, binding is stale, schema is outdated, anchor is ambiguous. Apply appropriate fix: update anchor phrase, revise binding entry, correct schema relation, split or merge entities. After repair, verify again. The loop closes when the report is clean.

Automation is possible but not required. An LLM can run verification by following this protocol: parse schema, parse binding, search body for anchors, check relations. A script can do the same for most checks. Human review remains appropriate for judgment calls: is this anchor sufficiently unique? Does this summary capture the claim?

Verification frequency depends on edit intensity. A document under active revision should verify after each significant change. A stable document should verify periodically to catch environmental drift. A document being mapped for the first time should verify incrementally as schema and binding are built.

---

## Schema

[O-001] Verification is coherence checking
  Type: O-claim
  Summary: Verification checks agreement across body, schema, and binding.

[O-002] Six verification checks
  Type: O-claim
  Summary: The protocol comprises six specific checks.
  Depends-on: [O-001]

[O-003] Schema completeness check
  Type: O-claim
  Summary: Every schema entity must have required fields.
  Depends-on: [O-002]

[O-004] Binding coverage check
  Type: O-claim
  Summary: Every schema entity must have a binding entry.
  Depends-on: [O-002]

[O-005] Anchor grounding check
  Type: O-claim
  Summary: Every binding anchor must exist in body.
  Depends-on: [O-002]

[O-006] Anchor uniqueness check
  Type: O-claim
  Summary: Each anchor must match exactly once.
  Depends-on: [O-002]

[O-007] Relation validity check
  Type: O-claim
  Summary: All schema relations must reference existing entities.
  Depends-on: [O-002]

[O-008] Type consistency check
  Type: O-claim
  Summary: Entity types must be correctly assigned.
  Depends-on: [O-002]

[O-009] Verification is not validation
  Type: O-claim
  Summary: Coherence checking does not assess truth or quality.

[O-010] Two verification modes
  Type: O-claim
  Summary: Full and incremental verification serve different purposes.
  Depends-on: [O-001]

[O-011] Verification produces report
  Type: O-claim
  Summary: Output is a structured list of checks, entities, and failures.
  Depends-on: [O-001]

[O-012] Repair follows verification
  Type: O-claim
  Summary: Friction items from verification guide targeted fixes.
  Depends-on: [O-011]

[R-001] Anchor grounding is common failure mode
  Type: R-claim
  Summary: Body edits frequently break anchor bindings.
  Supports: [O-005]

[R-002] Automation is possible
  Type: R-claim
  Summary: Most checks can be run by LLM or script.
  Supports: [O-002]

[C:verification] Verification
  Type: concept
  Definition: Coherence checking across mapped prose layers.

[C:friction-item] Friction item
  Type: concept
  Definition: Specific failure with location and cause, enabling targeted repair.

[C:verification-report] Verification report
  Type: concept
  Definition: Structured output listing checks run, entities examined, failures found.

[C:full-verification] Full verification
  Type: concept
  Definition: Complete check of all entities, suitable for periodic review.

[C:incremental-verification] Incremental verification
  Type: concept
  Definition: Check of changed entities only, suitable for rapid iteration.

---

## Binding

[O-001]
  Anchor: "Verification is coherence checking across the three layers"
  Scope: sentence

[O-002]
  Anchor: "These checks compose into a verification pass"
  Scope: sentence

[O-003]
  Anchor: "Schema completeness is the first check"
  Scope: sentence

[O-004]
  Anchor: "Binding coverage is the second check"
  Scope: sentence

[O-005]
  Anchor: "Anchor grounding is the third check"
  Scope: sentence

[O-006]
  Anchor: "Anchor uniqueness is the fourth check"
  Scope: sentence

[O-007]
  Anchor: "Relation validity is the fifth check"
  Scope: sentence

[O-008]
  Anchor: "Type consistency is the sixth check"
  Scope: sentence

[O-009]
  Anchor: "Verification is not validation"
  Scope: sentence

[O-010]
  Anchor: "Two verification modes serve different purposes"
  Scope: sentence

[O-011]
  Anchor: "Verification produces a report"
  Scope: sentence

[O-012]
  Anchor: "Repair follows verification"
  Scope: sentence

[R-001]
  Anchor: "This is the most common failure mode under editing"
  Scope: sentence

[R-002]
  Anchor: "Automation is possible but not required"
  Scope: sentence

[C:verification]
  Anchor: "Verification is coherence checking"
  Scope: phrase

[C:friction-item]
  Anchor: "Each failure is a friction item with specific location"
  Scope: sentence

[C:verification-report]
  Anchor: "The report lists: checks run, entities examined, failures found"
  Scope: sentence

[C:full-verification]
  Anchor: "Full verification runs all checks"
  Scope: phrase

[C:incremental-verification]
  Anchor: "Incremental verification checks only changed entities"
  Scope: phrase
