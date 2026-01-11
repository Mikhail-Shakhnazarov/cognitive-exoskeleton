---
title: Mapped Prose Format
type: format-specification
format-version: 0.1
status: draft
created: 2026-01-11
copyright: Mikhail Shakhnazarov 2026
license: CC BY 4.0
---

## Body

Mapped prose is a document format for texts that carry their own semantic map. The format separates content from structure while maintaining verifiable coherence between them.

A mapped prose document has three layers. The body is pure prose, readable without annotation, containing the work itself. The schema names the semantic units and their relations. The binding connects schema to body through anchor phrases that locate each unit in the text.

The body is the territory. Dense prose, terse where appropriate, carrying meaning through grammar and structure rather than through formatting. No identifiers interrupt the reading surface. A reader encounters only the text.

The schema is the map. It names what the body contains: claims, concepts, definitions. Each entity has an identifier, a type, and may have relations to other entities. The schema makes explicit what the prose implies.

The binding is the legend. It answers: where in the body does each schema entity live? Bindings use anchor phrases—short, distinctive text spans that appear exactly once in the body. To find an entity, search for its anchor.

The three layers form a triple structure. Schema relates to body through binding. This is not metaphor: the format itself is a knowledge triple, subject-predicate-object, where schema is subject, binding is predicate, body is object.

Every binding entry is a triple: entity located-at anchor. Every schema relation is a triple: entity relates-to entity. The document is a graph. The body is the root node to which all structure refers.

Verification follows from this structure. Schema completeness: every entity has required fields. Binding coverage: every schema entity has a binding. Anchor grounding: every anchor exists in body. Anchor uniqueness: each anchor matches exactly once. Relation validity: all referenced entities exist. These checks are mechanical. Failure produces specific friction, not vague unease.

Rendering is a separate concern. The format specifies structure, not presentation. A rendering doctrine translates format to a specific environment. For Obsidian: schema identifiers may become wikilinks for graph integration, claim types may become tags for filtering, navigation between layers follows vault conventions. The doctrine is optional. The format works as plain markdown.

Conventions for identifiers: operator-verified claims use O-prefix, research-verified claims use R-prefix, concepts use C-prefix. The distinction matters because verification authority differs. An O-claim is true by design decision; the operator is the authority. An R-claim is true by evidence; external reality is the authority.

Frontmatter carries document metadata: title, type, format-version, status, created date. This enables tooling without polluting the body.

A mapped prose document is self-contained. Body plus schema plus binding, in one file, readable as prose, verifiable as structure, renderable in multiple environments. The format earns its complexity by making coherence checkable.

---

## Schema

[O-001] Three-layer structure
  Type: O-claim
  Summary: Mapped prose consists of body, schema, and binding layers.

[O-002] Body is pure prose
  Type: O-claim
  Summary: The body contains no identifiers or structural annotation.
  Depends-on: [O-001]

[O-003] Schema names semantic units
  Type: O-claim
  Summary: The schema explicitly identifies claims, concepts, and relations.
  Depends-on: [O-001]

[O-004] Binding connects via anchors
  Type: O-claim
  Summary: Bindings use anchor phrases to locate schema entities in body.
  Depends-on: [O-001], [O-003]

[O-005] Format is triple structure
  Type: O-claim
  Summary: The format itself is a knowledge triple: schema-binding-body.
  Depends-on: [O-001]

[O-006] Verification is mechanical
  Type: O-claim
  Summary: Coherence checks are specifiable and runnable.
  Depends-on: [O-004], [O-005]

[O-007] Rendering is separate concern
  Type: O-claim
  Summary: Presentation rules are decoupled from format structure.
  Depends-on: [O-001]

[O-008] O-claims vs R-claims distinction
  Type: O-claim
  Summary: Claim types differ by verification authority.

[O-009] Self-contained document
  Type: O-claim
  Summary: All three layers exist in one file.
  Depends-on: [O-001]

[R-001] Anchor uniqueness enables location
  Type: R-claim
  Summary: Distinctive phrases can reliably locate text spans.
  Supports: [O-004]

[R-002] Verifiable coherence reduces drift
  Type: R-claim
  Summary: Mechanical checks catch structural drift before semantic confusion.
  Supports: [O-006]

[C:mapped-prose] Mapped prose
  Type: concept
  Definition: Document format where content carries its own semantic map.

[C:body] Body
  Type: concept
  Definition: Pure prose layer containing the work itself.

[C:schema] Schema
  Type: concept
  Definition: Layer naming semantic units and their relations.

[C:binding] Binding
  Type: concept
  Definition: Layer connecting schema entities to body locations via anchors.

[C:anchor] Anchor phrase
  Type: concept
  Definition: Distinctive text span appearing exactly once in body, used to locate schema entities.

[C:o-claim] O-claim
  Type: concept
  Definition: Operator-verified claim; true by design decision.

[C:r-claim] R-claim
  Type: concept
  Definition: Research-verified claim; true by external evidence.

---

## Binding

[O-001]
  Anchor: "A mapped prose document has three layers"
  Scope: sentence

[O-002]
  Anchor: "No identifiers interrupt the reading surface"
  Scope: sentence

[O-003]
  Anchor: "The schema makes explicit what the prose implies"
  Scope: sentence

[O-004]
  Anchor: "Bindings use anchor phrases"
  Scope: sentence

[O-005]
  Anchor: "The three layers form a triple structure"
  Scope: sentence

[O-006]
  Anchor: "These checks are mechanical"
  Scope: sentence

[O-007]
  Anchor: "Rendering is a separate concern"
  Scope: sentence

[O-008]
  Anchor: "The distinction matters because verification authority differs"
  Scope: sentence

[O-009]
  Anchor: "A mapped prose document is self-contained"
  Scope: sentence

[R-001]
  Anchor: "search for its anchor"
  Scope: sentence

[R-002]
  Anchor: "Failure produces specific friction"
  Scope: sentence

[C:mapped-prose]
  Anchor: "Mapped prose is a document format"
  Scope: sentence

[C:body]
  Anchor: "The body is the territory"
  Scope: sentence

[C:schema]
  Anchor: "The schema is the map"
  Scope: sentence

[C:binding]
  Anchor: "The binding is the legend"
  Scope: sentence

[C:anchor]
  Anchor: "anchor phrases—short, distinctive text spans"
  Scope: phrase

[C:o-claim]
  Anchor: "An O-claim is true by design decision"
  Scope: sentence

[C:r-claim]
  Anchor: "An R-claim is true by evidence"
  Scope: sentence

---

## Doctrine: Obsidian Rendering

These conventions apply when rendering mapped prose in Obsidian.

Frontmatter uses YAML. Required fields: title, type, format-version, status, created. Obsidian parses this natively.

Section headers use H2 for layers: Body, Schema, Binding. This enables folding and navigation.

Schema identifiers may be converted to wikilinks for graph integration. An identifier like [O-001] becomes [[O-001]] when graph visibility is desired. This is optional; plain brackets work.

Claim types may use tags for filtering. Add #o-claim or #r-claim after type declaration. This enables Obsidian search.

Links between documents use standard wikilinks: [[TERSE_TEXT]] references the terse text specification. Anchor links within documents use [[#heading]] format.

What Obsidian features to avoid: transclusion (![[embed]]) creates hidden dependencies. Dataview queries add runtime complexity. Templater automation obscures provenance. All structural refactoring happens via agentic LLM, not via Obsidian automation.

Graph view shows document relationships when wikilinks are used. Each mapped prose document appears as a node. Links between documents create edges. This is a derived view, not the source of truth.

The body section is the primary reading view. Schema and binding are reference sections. A reader may fold them away and encounter only prose.
