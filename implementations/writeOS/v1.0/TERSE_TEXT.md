---
title: Terse Text
type: seed-document
format-version: 0.1
status: draft
created: 2026-01-11
copyright: Mikhail Shakhnazarov 2026
license: CC BY 4.0
---

## Body

Terse text is dense prose where grammar carries structure. It is not brevity for its own sake. It is high structure-per-token: each word does semantic work, and syntactic arrangement does organizational work.

Grammar carries hierarchy. Subordinate clauses express scope; parallel constructions express coordination; declarative sentences establish frame. The structure is in the syntax, not in formatting overlays. A well-formed terse sentence encodes its own position in the argument.

Artifacts written in terse text carry their own map. They are parseable on re-read without access to the conversation that produced them. A future reader, or a different model instance, can reconstruct the logic from the prose alone. Private context is not required.

Terse is diagnostic. If a concept cannot be stated tersely without spawning unmoored nouns, cascading caveats, or connective tissue that references nothing decided, the concept is not yet stable. Noun proliferation signals incomplete analysis. Caveat chains signal unresolved uncertainty. The inability to compress is evidence of liquid state.

Terse text favors prose over formatting. Bullet lists fragment attention. Headers proliferate hierarchy without meaning. Tables encode structure that could live in sentences. When these formats are used, they should earn their place by clarifying what prose cannot. The default is dense paragraphs.

Token efficiency is a consequence, not a goal. Terse prose achieves higher semantic density because it eliminates redundancy: no filler phrases, no hedging, no performative connectives. The same meaning fits in fewer tokens. This matters for context-limited environments. It matters more as a discipline that forces clarity.

Terse text matches certain cognitive profiles. Aphantasia routes structure through language rather than imagery; dense prose is native, not burdensome. High verbal facility makes complex sentences tractable. ADHD re-entry cost makes self-contained artifacts valuable; if the text requires external context, re-entry fails.

Terse text matches transformer processing. Attention mechanisms operate over token sequences. Dense prose with explicit grammatical structure provides more signal per position. Sparse formatting with implicit relationships provides less. This is an empirical property of the architecture, not an aesthetic preference.

A terse text that cannot be understood is not terse; it is merely short. Compression without fidelity is lossy. The goal is maximum meaning per token, not minimum tokens per document. If compression loses structure, decompress.

Terse text is a medium choice. It is not universally correct. Conversational contexts may favor redundancy for clarity. Pedagogical contexts may favor repetition for retention. Legal contexts may favor explicitness over compression. The choice of terse text is a choice for contexts where density, re-entry, and machine processing matter.

---

## Schema

[O-001] Grammar carries structure
  Type: O-claim
  Summary: Syntactic arrangement encodes organizational hierarchy.

[O-002] Subordination expresses scope
  Type: O-claim
  Summary: Subordinate clauses delimit what applies to what.
  Depends-on: [O-001]

[O-003] Parallel construction expresses coordination
  Type: O-claim
  Summary: Syntactically parallel elements are semantically coordinate.
  Depends-on: [O-001]

[O-004] Artifacts self-map
  Type: O-claim
  Summary: Terse artifacts are parseable without private context.
  Depends-on: [O-001]

[O-005] Terse is diagnostic
  Type: O-claim
  Summary: Inability to compress signals conceptual instability.

[O-006] Prose over formatting
  Type: O-claim
  Summary: Dense paragraphs are default; formatting must earn its place.
  Depends-on: [O-001]

[O-007] Compression without fidelity is lossy
  Type: O-claim
  Summary: Terse means maximum meaning per token, not minimum tokens.

[O-008] Terse is medium choice
  Type: O-claim
  Summary: Terse text suits specific contexts, not all contexts.

[R-001] Token efficiency
  Type: R-claim
  Summary: Terse prose achieves higher semantic density per token.
  Supports: [O-006]

[R-002] Cognitive profile match
  Type: R-claim
  Summary: Terse text suits aphantasia, high verbal facility, ADHD re-entry needs.
  Supports: [O-004]

[R-003] Transformer processing match
  Type: R-claim
  Summary: Dense grammatical prose provides more signal per attention position.
  Supports: [O-001], [R-001]

[R-004] Noun proliferation signals instability
  Type: R-claim
  Summary: Unmoored nouns indicate incomplete analysis.
  Supports: [O-005]

[R-005] Caveat chains signal uncertainty
  Type: R-claim
  Summary: Cascading qualifications indicate unresolved decisions.
  Supports: [O-005]

[C:terse-text] Terse text
  Type: concept
  Definition: Dense prose where grammar carries structure.

[C:structure-per-token] Structure-per-token
  Type: concept
  Definition: Ratio of organizational information to token count.

[C:self-mapping] Self-mapping
  Type: concept
  Definition: Property of artifacts parseable without external context.

[C:diagnostic-compression] Diagnostic compression
  Type: concept
  Definition: Using ability to compress as test for conceptual stability.

---

## Binding

[O-001]
  Anchor: "Grammar carries hierarchy"
  Scope: sentence

[O-002]
  Anchor: "Subordinate clauses express scope"
  Scope: phrase

[O-003]
  Anchor: "parallel constructions express coordination"
  Scope: phrase

[O-004]
  Anchor: "Artifacts written in terse text carry their own map"
  Scope: sentence

[O-005]
  Anchor: "Terse is diagnostic"
  Scope: sentence

[O-006]
  Anchor: "Terse text favors prose over formatting"
  Scope: sentence

[O-007]
  Anchor: "Compression without fidelity is lossy"
  Scope: sentence

[O-008]
  Anchor: "Terse text is a medium choice"
  Scope: sentence

[R-001]
  Anchor: "higher semantic density because it eliminates redundancy"
  Scope: phrase

[R-002]
  Anchor: "Terse text matches certain cognitive profiles"
  Scope: sentence

[R-003]
  Anchor: "Terse text matches transformer processing"
  Scope: sentence

[R-004]
  Anchor: "Noun proliferation signals incomplete analysis"
  Scope: sentence

[R-005]
  Anchor: "Caveat chains signal unresolved uncertainty"
  Scope: sentence

[C:terse-text]
  Anchor: "Terse text is dense prose where grammar carries structure"
  Scope: sentence

[C:structure-per-token]
  Anchor: "high structure-per-token"
  Scope: phrase

[C:self-mapping]
  Anchor: "parseable on re-read without access to the conversation"
  Scope: phrase

[C:diagnostic-compression]
  Anchor: "If a concept cannot be stated tersely"
  Scope: sentence
