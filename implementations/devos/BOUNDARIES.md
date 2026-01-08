# Boundaries

## Contents
- port_separation.md
- operator_termination.md
- terse_architecture.md

---

## port_separation.md

> Source: `port_separation.md`

# Port Separation

## Entry

Interpretation and execution are different functions with different failure modes. Port B interprets (thinks with operator, drafts specs). Port A executes (writes code, returns friction). They don't share context.

The boundary localizes failure: spec wrong Port B. Execution wrong Port A. Mixed interpretation/execution hides the source.

**Interface:** The spec. Port B produces it; operator approves it; Port A consumes it.

---

## Synthesis

Interpretation and execution are different functions with different failure modes. Mixing them creates ambiguity about where problems originate.

Port B interprets. It thinks with the operator, analyzes situations, surfaces options, drafts specifications. It operates in the space of meaning, structure, and decision.

Port A executes. It takes specifications and produces artifacts -- code, files, changes. It operates in the space of implementation, precision, and friction.

They don't share context. Port B doesn't know Port A's execution state unless operator provides it. Port A doesn't interpret ambiguity -- it returns friction.

The boundary localizes failure:
- Spec has wrong requirements Port B problem.
- Code doesn't match spec Port A problem.
- Requirements were ambiguous Friction reveals it.

The spec is the interface. It's a contract: Port B produces it, operator approves it, Port A consumes it. The contract creates accountability on both sides.

Friction is the return channel. When Port A can't proceed, it signals what's missing. Friction routes to operator, who either decides or sends to Port B for elaboration.

---

## See also

- [[operator_termination]] -- who receives the friction
- [[observable_state]] -- how friction becomes visible
- [[terse_architecture]] -- how specs achieve precision

## operator_termination.md

> Source: `operator_termination.md`

# Operator Termination

## Entry

All decision loops close with the human operator. Models produce options, drafts, and analysis. The operator decides, approves, and accepts.

This is architectural, not ethical or sentimental. It creates accountability (responsibility is localizable), quality control (errors caught before propagation), sustainability (operator stays competent), and reversibility (decision points are natural checkpoints).

**Not:** Operator does everything. **Yes:** Operator authorizes everything that matters.

---

## Synthesis

All decision loops close with the human operator. This is architectural, not ethical.

**Accountability:** When something goes wrong, responsibility is localizable. The operator approved it. No diffusion of responsibility across autonomous agents.

**Quality control:** Errors are caught at decision points before they propagate. The operator review is a natural quality gate.

**Sustainability:** The operator stays competent because the operator stays engaged. Cognitive atrophy from over-delegation is avoided.

**Reversibility:** Decision points are natural checkpoints. Rolling back to "before operator approved X" is meaningful. Rolling back autonomous agent choices is murky.

Operator termination doesn't mean operator does everything. Models do heavy lifting: analysis, drafting, exploration, execution. But crossing from "proposal" to "committed" requires operator action.

The system is designed so this constraint is lightweight. Specs are concise. Friction is structured. Review is fast. Operator termination adds minimal overhead while preserving maximum control.

---

## See also

- [[port_separation]] -- where loops get routed
- [[cognitive_exoskeleton]] -- the containing design philosophy
- [[observable_state]] -- what operator needs to decide

## terse_architecture.md

> Source: `terse_architecture.md`

# Terse Architecture

## Entry

Terse is high structure-per-token, not brevity. Grammar carries hierarchy. Subordination expresses scope. Parallel syntax expresses coordination. Artifacts carry their own map.

Terse matches operator cognition (aphantasia, high language facility) and LLM processing (attention on token sequences). Dense prose for dense processing.

**Diagnostic:** If it can't be stated tersely, it's not stable yet.

---

## Synthesis

Terse is high structure-per-token, not brevity. Many tokens do double duty -- carrying semantic content while encoding relation (contrast, causality, modification, reference).

Grammar carries hierarchy. Subordination expresses scope. Parallel syntax expresses coordination. Declarative sentences establish frame. The structure is in the prose, not in formatting.

Artifacts carry their own map. Parseable on re-read without private context. A terse document can be understood by a future reader (or a different model instance) without access to the conversation that produced it.

Terse is diagnostic. If a concept can't be stated tersely without spawning new nouns, caveats, or connective tissue not anchored to decisions -- the state is liquid. Noun proliferation signals instability. Caveat chains signal uncertainty. Terse forces clarity.

Terse matches operator cognition. Aphantasia means structure through language, not imagery. High language facility means dense text is native, not burdensome. ADHD re-entry cost means artifacts must carry their own context.

Terse matches LLM processing. Transformers attend to token sequences. Dense prose with grammatical structure gives them what they process well. Sparse bullets with implicit relationships give them less to work with.

---

## See also

- [[cognitive_load]] -- terse reduces extraneous load
- [[extended_cognition]] -- terse artifacts as cognitive scaffolds
- [[observable_state]] -- terse enables inspection
