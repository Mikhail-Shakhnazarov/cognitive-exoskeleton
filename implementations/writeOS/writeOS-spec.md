# writeOS v1 Specification

> [!info] Document Status
> **Status:** DRAFT  
> **Version:** 0.1  
> **Date:** 2025-01-11

---

## Problem

Editing prose through LLM conversation produces changes whose rationale exists only in volatile chat history. Over multiple sessions:

- Tracking *why* edits were made becomes impossible
- Alternatives considered are lost
- Editorial intent drifts from textual reality
- The decision chain cannot be reconstructed or audited

The core failure mode is **semantic drift under iteration**—text changes accumulate without traceable intent, and continuity breaks down.

---

## Solution

writeOS is a discipline for prose editing that separates interpretation from execution and maintains parallel artifacts linking intent to change to outcome.

### Architecture

Two processes, one interface:

```
┌─────────────────┐         ┌─────────────────┐
│   INTERPRETER   │         │    EXECUTOR     │
│                 │         │                 │
│ - analyzes text │         │ - applies patch │
│ - surfaces opts │  PATCH  │ - produces diff │
│ - drafts patch  │────────▶│ - verifies app. │
│                 │         │                 │
└────────┬────────┘         └────────┬────────┘
         │                           │
         │         OPERATOR          │
         └───────────┬───────────────┘
                     │
              reviews / approves
              all decision loops
              terminate here
```

**Interpreter**: Structures editorial analysis, surfaces options and trade-offs, drafts patch specifications. Operates in the space of meaning and intent.

**Executor**: Applies approved patches mechanically, produces git diffs, verifies changes landed as specified. Operates in the space of text transformation. Does not interpret—returns friction when specification is ambiguous or unapplicable.

**Patch**: The interface artifact. A forward-looking specification of changes *before* they occur—analogous to code patches specifying transformations before application. Carries both intent (for humans, for history) and specification (for executor).

**Operator**: Reviews and approves patches before execution, reviews diffs before commit. All decision loops terminate with the operator. Processes propose; operator decides.

### Artifact Chain

Each editing operation produces three linked artifacts:

| Artifact | Purpose |
|----------|---------|
| **Patch** | What should change and why (intent + specification) |
| **Diff** | What actually changed (git diff) |
| **Commit** | Why it changed (message referencing patch) |

This chain makes editing traceable, reversible, and auditable. Patches accumulate in `patches/`, forming a historical record of editorial decisions independent of git history.

---

## Location Addressing

### The Problem

Patches must specify *where* changes occur. Code has stable anchors (function names, line numbers). Prose lacks these. Different solutions have emerged historically:

| Tradition | Solution | Insight |
|-----------|----------|---------|
| **Biblical** | book/chapter/verse | Intrinsic numbering surviving translation and edition changes |
| **Philosophical** | Paragraph or proposition numbers (Wittgenstein's Tractatus decimals, Spinoza's propositions, Bekker numbers for Aristotle) | Stable reference for commentary traditions |
| **Legal** | section/subsection/clause | Hierarchical path with numbered nodes |

The common pattern: **intrinsic identifiers that travel with the text**, not imposed by pagination or external tooling.

### writeOS Approach: Hybrid Addressing

For texts under active editing, impose paragraph identifiers as part of the editorial process. These IDs are embedded in the text (as comments or markers) and travel with content through restructuring.

Location addresses combine three elements:

```
[path] / [paragraph-id] / [anchor]
```

**Path**: Hierarchical location via headings/sections

```
Part II / 1.1 "The coherence bias"
```

**Paragraph ID**: Stable identifier assigned during editorial process

```
¶023
```

**Anchor**: Content-based disambiguation (first N words, or semantic label)

```
p:"A common drift pattern is"
```

Full address example:

```
Part II / 1.1 / ¶023 / p:"A common drift pattern is"
```

### Address Resolution

Addresses resolve left-to-right with increasing specificity:

1. Path narrows to section
2. Paragraph ID identifies specific paragraph (if present)
3. Anchor disambiguates within section (if ID absent or for spans within paragraph)

> [!warning] Resolution Failure
> If any component fails to resolve, executor returns friction—does not guess.

### Location Types

| Type | Use | Format |
|------|-----|--------|
| `section` | Structural operations (reorder, delete section) | `path` |
| `paragraph` | Whole-paragraph operations | `path / ¶ID` or `path / anchor` |
| `span` | Inline edits within paragraph | `path / ¶ID / anchor...end-anchor` |
| `position` | Insertions | `after:path/¶ID` or `before:path/¶ID` |

### Paragraph ID Convention

IDs are assigned sequentially during initial indexing: `¶001`, `¶002`, etc.

| Event | Convention |
|-------|------------|
| Paragraph added | Sub-numbering: `¶023a`, `¶023b` |
| Paragraph deleted | ID retired (not reused) |
| Paragraph split | Original ID stays with first fragment; new fragments get sub-numbers |
| Paragraph merged | Lower ID survives |

This mimics how biblical versification handles textual variation—IDs are stable anchors, not sequential counters.

---

## Change Types

Minimal taxonomy of primitive operations:

| Type | Description | Spec Fields |
|------|-------------|-------------|
| `replace` | Swap text span | location, before, after |
| `insert-after` | Add content after location | location, content |
| `insert-before` | Add content before location | location, content |
| `delete` | Remove span | location, before |
| `move` | Relocate span | from-location, to-location, content |

Complex operations compose from primitives. Restructuring a section is a sequence of moves. Splitting a paragraph is delete + insert-after + insert-after.

The executor applies primitives mechanically. It does not interpret "strengthen this argument" or "clarify this passage"—those are intent, translated by the interpreter into primitive specs before the patch reaches the executor.

---

## Patch Format

```markdown
# PATCH-{{NNN}}: {{Title}}

> Status: DRAFT | APPROVED | APPLIED | REJECTED
> Created: {{YYYY-MM-DD}}
> Target: {{file path}}
> Depends: {{PATCH-NNN if any}}
> Session: {{session link if relevant}}

## Intent

{{Editorial rationale—what this change accomplishes and why. What you'd say 
explaining the edit to a colleague. This field is for humans and history; 
the executor ignores it.}}

## Specification

### Change 1: {{brief label}}

- **type**: replace | insert-after | insert-before | delete | move
- **location**: {{path / ¶ID / anchor}}
- **before**: |
    {{exact text being replaced/deleted — empty for inserts}}
- **after**: |
    {{exact new text — empty for deletes}}

### Change 2: {{brief label}}
...

## Verification

- [ ] All locations resolve (no anchor mismatch)
- [ ] Before-text matches actual text
- [ ] After-text applies cleanly
- [ ] Surrounding context remains coherent
- [ ] {{domain-specific checks}}

## Alternatives Considered

{{Optional: other approaches rejected and why. Preserves decision context.}}

## Notes

{{Implementation notes, cross-references, open questions.}}
```

---

## Index Structure

For large texts, maintain a navigable index as a separate artifact. The index:

- Provides overview without loading full text
- Maps paragraph IDs to structural locations
- Captures core claims per section (for semantic navigation)
- Stays small enough to fit in working memory

### Index Template

```markdown
# {{Document}} Index

> Updated: {{YYYY-MM-DD}}
> Paragraphs: {{total count}}
> Words: {{approximate}}

## Structure

### Part I — {{Title}}
Core claim: {{one sentence}}

#### 1. {{Section}}
¶001-¶012
- {{key point}}
- {{key point}}

#### 2. {{Section}}
¶013-¶025
...

## Paragraph Registry

| ID | Location | First Words | Status |
|----|----------|-------------|--------|
| ¶001 | Part I / intro | "A Work-OS is a" | active |
| ¶002 | Part I / intro | "Model context behaves" | active |
| ... | ... | ... | ... |
| ¶047 | Part II / 1.1 | — | deleted |
```

The registry is the canonical map from IDs to content. Updated after each editing session.

---

## Workflow

### Session Flow

```
1. Operator states editorial intent
   "The Ashby section needs a concrete example"

2. Interpreter analyzes
   - Loads index, locates section
   - Loads section full text
   - Surfaces options, trade-offs
   - Drafts patch specification

3. Operator reviews patch
   - Approves → proceed to execution
   - Requests changes → interpreter revises
   - Rejects → patch marked REJECTED, end

4. Executor applies patch
   - Resolves locations
   - Verifies before-text matches
   - Applies changes
   - Produces diff
   - Returns friction if any step fails

5. Operator reviews diff
   - Approves → commit with message referencing patch
   - Rejects → revert, patch marked REJECTED or revised

6. Update index
   - New/deleted/moved paragraphs reflected
   - Patch marked APPLIED
```

### File Organization

```
project/
├── text/
│   └── monograph.md          # the text being edited
├── index/
│   └── monograph-index.md    # navigable index + paragraph registry
├── patches/
│   ├── PATCH-001.md
│   ├── PATCH-002.md
│   └── ...
└── sessions/
    └── ...                   # session records if kept
```

### Commit Convention

```
edit(§location): brief description

Applies PATCH-NNN: {{patch title}}

{{Intent from patch, condensed}}

Changes:
- {{change 1 summary}}
- {{change 2 summary}}
```

---

## Verification (v1)

v1 verification is **operator review only**:

- Operator reviews patch before approval
- Operator reviews diff before commit
- System does not claim automated verification capabilities

> [!note] Future Versions
> May add:
> - Citation/reference checking
> - Internal consistency validation
> - Style/terminology consistency
> - Peer review workflows

---

## Constraints

### Self-Hosting Requirement

writeOS must be usable to edit its own documentation from v1. This forces the architecture to handle real editing needs and prevents specification drift from implementation reality.

### Operator Termination

All decision loops terminate with the operator. The interpreter proposes patches; it does not apply them. The executor applies patches; it does not interpret ambiguity. Neither process proceeds without operator approval at the relevant gate.

### Friction Over Guessing

When the executor cannot resolve a location, match before-text, or apply a change cleanly, it returns friction—a structured description of what failed and why. It does not guess, interpolate, or "do its best." Silent failures are worse than loud ones.

---

## Glossary

| Term | Definition |
|------|------------|
| **Anchor** | Content-based location marker (first words of paragraph, semantic label) |
| **Executor** | Process that applies patches mechanically; does not interpret |
| **Friction** | Structured signal that execution cannot proceed; routes to operator |
| **Index** | Navigable outline of document with paragraph registry |
| **Intent** | Editorial rationale for a change; for humans and history |
| **Interpreter** | Process that analyzes text and drafts patches; operates in meaning-space |
| **Location** | Address specifying where in text a change applies |
| **Operator** | Human authority; all decision loops terminate here |
| **Paragraph ID** | Stable identifier (¶NNN) assigned to paragraph; travels with content |
| **Patch** | Specification of intended changes; interface between interpreter and executor |
| **Path** | Hierarchical location via headings/sections |
| **Specification** | Machine-readable change instructions; consumed by executor |
| **Span** | Contiguous text region within a paragraph |

---

## See Also

- [[KERNEL]] — Work-OS kernel (parent system)
- [[PORT_A_PROTOCOL]] — Executor protocol reference
- [[PORT_B_SYSTEM]] — Interpreter context reference
- [[DOCTRINE]] — Operational principles
