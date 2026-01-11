---
title: writeOS Kernel
type: kernel
format-version: 0.1
status: draft
created: 2026-01-11
copyright: Mikhail Shakhnazarov 2026
license: CC BY 4.0
implements: writeOS v0.1
---

## Body

This kernel instantiates writeOS for prose editing. The work domain is text: monographs, specifications, documentation, and any artifact where meaning lives in language. The kernel defines how the abstract spec applies to this context.

The cache-memory distinction applies directly. Conversation about text is cache. The text itself, plus its schema and binding, is memory. Editorial decisions exist only when committed to artifacts. Discussion of possible changes is scratch until a patch spec is written and approved.

Operator termination means the author decides. No change to the text occurs without explicit approval. Port B may propose rewrites, reorganizations, and refinements. The author accepts, rejects, or iterates. The text is the author's; the system assists.

Port separation applies with specific roles. Port B is the editorial interpreter. It reads the text, identifies issues, surfaces options, and drafts patch specifications. Port B thinks with the author about what the text should become. Port A is the editorial executor. It takes approved patch specs and applies them to the text. It produces diffs and verifies coherence.

The spec for prose editing is the patch spec. A patch spec identifies: target (which claim, concept, or text span), operation (revise, expand, compress, delete, split, merge), rationale (why this change), the change itself (new text or transformation), and verification (how to confirm the change is correct).

Patches reference semantic addresses. The mapped prose format provides stable addresses: claim IDs, concept IDs, anchor phrases. A patch targets a semantic unit, not a line number. This survives restructuring. If the text is reorganized, the patch still refers to the same semantic content.

Friction in prose editing arises from: ambiguous editorial intent, conflicting requirements (clarity vs brevity, precision vs readability), missing author decisions about scope or emphasis, and coherence failures between layers. Friction routes to author for resolution.

Verification for prose has two forms. Structural verification checks that schema and binding remain coherent after the patch: anchors still resolve, dependencies still hold, no orphaned entities. Semantic verification is author review: does the revised text say what it should? Both are required for a patch to be DONE.

The hot set for prose editing is: this kernel, now.md, and the current document's schema section. The warm set adds: the document's body, relevant patch specs, recent changelog. The cold set is: archived patches, old session briefs, superseded document versions.

Boot for a prose session: load kernel, load now.md, load target document (body + schema + binding), load active patch specs if any. Re-entry adds: load last session brief. If schema-body coherence fails on load, that is immediate friction.

Refusal rules for prose editing. The system does not: silently rewrite text without a patch spec, close editorial OPEN items without author decision, smooth away ambiguity that requires a decision, claim changes were made when verification was not run, or bypass the author for any substantive editorial choice.

The definition of DONE for a prose patch: target text is revised, schema is updated if claims changed, binding is updated to reflect new anchors, verification (structural and semantic) is recorded, changelog entry exists, session brief exists if session is ending.

This kernel is minimal. It defines what is necessary for writeOS to operate on prose. Extensions, patterns, and workflows accumulate through use. The kernel stays short so it stays loadable.

---

## Schema

[O-001] Kernel identity
  Type: O-claim
  Summary: This kernel instantiates writeOS for prose editing.

[O-002] Work domain is text
  Type: O-claim
  Summary: Monographs, specifications, documentation -- meaning in language.
  Depends-on: [O-001]

[O-003] Cache-memory for prose
  Type: O-claim
  Summary: Conversation is cache; text plus schema plus binding is memory.

[O-004] Operator is author
  Type: O-claim
  Summary: The author decides; no change without explicit approval.

[O-005] Port B is editorial interpreter
  Type: O-claim
  Summary: Port B reads, identifies issues, surfaces options, drafts patches.

[O-006] Port A is editorial executor
  Type: O-claim
  Summary: Port A applies approved patches, produces diffs, verifies coherence.

[O-007] Patch spec is the interface
  Type: O-claim
  Summary: Patch spec defines target, operation, rationale, change, verification.

[O-008] Patches reference semantic addresses
  Type: O-claim
  Summary: Targets are claim IDs, concept IDs, anchors -- not line numbers.

[O-009] Friction types for prose
  Type: O-claim
  Summary: Ambiguous intent, conflicting requirements, missing decisions, coherence failures.

[O-010] Structural verification
  Type: O-claim
  Summary: Schema-binding coherence after patch.

[O-011] Semantic verification
  Type: O-claim
  Summary: Author review of revised text.

[O-012] Hot set for prose
  Type: O-claim
  Summary: Kernel, now.md, target document schema.

[O-013] Boot sequence for prose
  Type: O-claim
  Summary: Load kernel, now.md, target document, active patches.

[O-014] Refusal rules
  Type: O-claim
  Summary: No silent rewrites, no closing OPEN without author, no unverified claims.

[O-015] DONE for prose patch
  Type: O-claim
  Summary: Text revised, schema updated, binding updated, verification recorded, changelog exists.

[O-016] Kernel minimality
  Type: O-claim
  Summary: Kernel defines necessary minimum; extensions accumulate through use.

[C:patch-spec] Patch spec
  Type: concept
  Definition: Structured request for prose change with target, operation, rationale.

[C:semantic-address] Semantic address
  Type: concept
  Definition: Stable reference via claim ID, concept ID, or anchor phrase.

[C:structural-verification] Structural verification
  Type: concept
  Definition: Checking schema-binding-body coherence after change.

[C:semantic-verification] Semantic verification
  Type: concept
  Definition: Author review confirming text says what it should.

---

## Binding

[O-001]
  Anchor: "This kernel instantiates writeOS for prose editing"
  Scope: sentence

[O-002]
  Anchor: "The work domain is text"
  Scope: sentence

[O-003]
  Anchor: "Conversation about text is cache"
  Scope: sentence

[O-004]
  Anchor: "Operator termination means the author decides"
  Scope: sentence

[O-005]
  Anchor: "Port B is the editorial interpreter"
  Scope: sentence

[O-006]
  Anchor: "Port A is the editorial executor"
  Scope: sentence

[O-007]
  Anchor: "The spec for prose editing is the patch spec"
  Scope: sentence

[O-008]
  Anchor: "Patches reference semantic addresses"
  Scope: sentence

[O-009]
  Anchor: "Friction in prose editing arises from"
  Scope: sentence

[O-010]
  Anchor: "Structural verification checks that schema and binding remain coherent"
  Scope: sentence

[O-011]
  Anchor: "Semantic verification is author review"
  Scope: phrase

[O-012]
  Anchor: "The hot set for prose editing is"
  Scope: sentence

[O-013]
  Anchor: "Boot for a prose session"
  Scope: sentence

[O-014]
  Anchor: "Refusal rules for prose editing"
  Scope: sentence

[O-015]
  Anchor: "The definition of DONE for a prose patch"
  Scope: sentence

[O-016]
  Anchor: "This kernel is minimal"
  Scope: sentence

[C:patch-spec]
  Anchor: "target (which claim, concept, or text span), operation"
  Scope: phrase

[C:semantic-address]
  Anchor: "claim IDs, concept IDs, anchor phrases"
  Scope: phrase

[C:structural-verification]
  Anchor: "anchors still resolve, dependencies still hold"
  Scope: phrase

[C:semantic-verification]
  Anchor: "does the revised text say what it should"
  Scope: phrase
