# Glossary

Key terms and concepts in the Cognitive Exoskeleton framework.

---

## Core Concepts

**Cognitive Exoskeleton**  
Infrastructure for LLM-mediated knowledge work that preserves operator agency while exploiting transformation capability. Coordination discipline that prevents semantic drift through port separation, artifact contracts, operator termination, and verification.

**Semantic Drift**  
The tendency of meaning to slide under iteration when transformation is cheap. Includes: terms changing definition, scope expanding invisibly, requirements shifting without documentation, decisions being rewritten retroactively.

**Second-Order Writing**  
Writing where the primary operation is specification of transformations rather than production of final text. Working at meta-level: defining semantic cores, transformation rules, and verification criteria rather than directly producing documents.

**Augmented Cognition**  
Amplification of human cognitive capability through external structures and tools. Distinct from automation—preserves human judgment and authority while delegating routine transformations.

---

## System Architecture

**Operator (Root)**  
The human authority who terminates decisions. Final responsibility and accountability. Not constant intervention, but binding authority. All decision loops close with operator.

**Port**  
A constrained role with explicit contract. Not a person or model, but a function that a runtime performs under specific rules. Prevents contamination between different kinds of work.

**Port B (Interpretation/Meaning)**  
The role that stabilizes intent, writes specifications, records decisions, identifies unknowns, and produces session memory. Works with ambiguity explicitly.

**Port A (Execution/Implementation)**  
The role that implements from specifications, produces diffs and verification results, refuses to invent requirements. Returns friction when ambiguous.

**Runtime**  
Concrete environment where a model is invoked (web chat, CLI agent, IDE). Treated as replaceable—system must not depend on specific runtime.

---

## Artifacts

**Spec (Specification)**  
Structured request from Port B to Port A. Contains: summary, scope (IN/OUT), requirements (MUST/SHOULD/MAY), interfaces, constraints, OPEN items, verification criteria.

**Friction**  
Typed blocked state. The system's refusal channel. Surfaces when work cannot proceed without operator decision. Types: semantic, scope, feasibility, environment, safety, governance.

**Changelog**  
Append-only journal of state transitions. Records: what changed, why, verification status, remaining friction, session pointer. Audit spine of the system.

**Session Brief**  
Compressed memory written at session end. Contains: intent → action → outcome, decisions made, diff summary, verification results, remaining friction, next pointers. Enables re-entry without transcript replay.

**Pattern**  
Reusable constraint or pitfall captured after repeat failures. Promotes learning into structure. Accumulates across projects.

**Domain Model**  
Captured understanding of client/project context. Business domain, entities, relationships, workflows, terminology, implicit requirements, pain points. Updated as understanding deepens.

---

## Memory and State

**Cache vs Memory**  
Fundamental distinction. Model context = cache (fast, volatile, non-authoritative). Repo artifacts = memory (durable, diffable, re-enterable). System treats conversation as scratch unless committed to artifacts.

**Hot Set**  
Minimal file set loaded on every boot. Required to restore correct behavior. Must remain small (if boot requires reading ten files, system reverts to cache-continuity).

**Pack**  
Curated working set loaded for specific operation. Bundle of files/artifacts that defines context scope. Types: BOOT_PACK (always), TASK_PACK (per task), SESSION_PACK (end-of-session writeout).

**Kernel**  
Smallest invariant rule set. Defines port contracts, artifact shapes, refusal modes. Must stay short—if kernel bloats, system becomes unbootable.

---

## Operations

**Operator Termination**  
All decision loops close with human operator. Decisions become binding when operator terminates ambiguity into commitment. Architectural principle, not preference.

**Commit**  
Writing durable state to artifacts: spec, decision, friction closure, changelog entry, session brief. Without commits, work does not accumulate—it merely continues.

**Verification**  
Explicit checks that define "done." Can be: tests pass, commands run successfully, manual review checklist, domain-specific validation. Reality anchor that prevents "seems done" from becoming DONE.

**Re-entry**  
Returning to work after time gap. Protocol: load kernel, load now, load last session brief, load task pack. Goal: <5 minute cold start to full context.

**DONE**  
Auditable completion state. Requirements satisfied or deferred, verification run and recorded, changelog entry appended, session brief exists, now.md updated to next action.

---

## Learning and Evolution

**Learning Flywheel**  
Systematic capability development across projects. Pattern: Project N → capture understanding → distill learnings → Operator more capable → Project N+1 faster/better.

**Learning Artifacts**  
Structured knowledge capture. Includes: patterns (failure modes), deep-dives (technical understanding), architecture decisions (design templates), domain knowledge (business context).

**Pattern Maturity**  
Progression of pattern confidence. Appears once = noted. Appears 3× = confirmed standard practice. Appears 6+× = consider automation/tooling.

---

## Failure Modes

**Coherence Bias**  
LLM tendency to fill gaps with plausible-sounding text even when uncertain. Creates drift by converting ambiguity into smooth narrative without explicit decisions.

**Authority Laundering**  
Gradual slide where model confidence becomes treated as truth without operator judgment. System appears to make decisions autonomously.

**Artifact Theater**  
Specs exist but don't constrain behavior. Verification skipped. Changelogs are narrative. System looks structured but doesn't prevent drift.

**Port Collapse**  
One context does both interpretation and execution. Separation becomes ceremonial. Category errors return.

---

## Philosophical Foundations

**Tool vs Solver**  
Fundamental distinction in system design. Solver: problem → black box → answer (operator atrophies). Tool: operator solves with amplification (judgment preserved and exercised).

**Operator Agency**  
Human authority and responsibility remains central. System amplifies but does not replace. Every decision point exercises judgment rather than delegating it.

**Provenance**  
Chain of authority for decisions and transformations. Who decided, when, under what understanding, based on what evidence. Enables auditability and revision.

**Subsidiarity**  
Decisions made at lowest competent level, escalated only when necessary. Prevents both micromanagement and authority drift. Explicit delegation rules define boundaries.

---

## Related Concepts

**Memex**  
Vannevar Bush's 1945 vision of associative information trails. Relevant as precedent for second-order operations on knowledge.

**Hypertext**  
Ted Nelson's concept of non-linear documents with typed links. Relevant for understanding transformation operations.

**Extended Cognition**  
Clark and Chalmers' framework treating external artifacts as part of cognitive system. Theoretical foundation for exoskeleton metaphor.

**Hermeneutic Circle**  
Parts and wholes constantly reshaping each other's meaning. Relevant for understanding how interpretation works across sessions.

---

## Implementation-Specific Terms (devOS)

**devOS**  
Development Operator/Operating System. Specialized implementation of cognitive exoskeleton for software development and freelance delivery. Adds: domain modeling, learning capture, client communication.

**Development as Learning**  
Each project increases capability through: patterns preventing failures, domain knowledge compounding, architecture decisions becoming templates, skills systematically developing.

**Portfolio as Proof**  
Projects serve dual purpose: delivery (immediate value) + demonstration (credibility object). Each project validates methodology while producing income.

---

*For complete theoretical treatment, see the [full monograph](MONOGRAPH.md).*  
*For practical application, see [devOS implementation](../implementations/devos/).*
