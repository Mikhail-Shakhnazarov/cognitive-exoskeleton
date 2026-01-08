# devOS: Development Operator/Operating System

devOS is a specialized implementation of the Cognitive Exoskeleton framework for software development and freelance delivery.

## What devOS Is

devOS extends the base cognitive exoskeleton coordination protocol with three integrated goals:

1. **Reliable delivery**: Ship working software through drift-resistant governance
2. **Deep understanding**: Model client domains, not just requirements
3. **Systematic learning**: Increase capability across projects through structured knowledge capture

This creates a defensible freelance position: not competing on "cheap code generation" but on reliability + understanding + knowledge transfer.

## Core Architecture

### Port Separation for Software

**Port B (Design/Interpretation)**:
- Domain analysis and modeling
- Specification writing
- Architecture decisions
- Client communication
- Learning capture

**Port A (Execution/Implementation)**:
- Code implementation from specs
- Test execution and verification
- Bug pattern consultation and updating
- Changelog maintenance

The boundary prevents "smoothing over" ambiguity during execution. Friction surfaces explicitly when specs are underspecified.

### New Artifact Types

Beyond base Work-OS artifacts, devOS adds:

**Domain Model** (`domain_model.md` per project):
- Client's business context
- Key entities and workflows
- Terminology and definitions
- Implicit requirements and constraints
- Updated as understanding deepens

**Bug Patterns** (`patterns/BUG_PATTERNS.md`):
- Cross-project failure memory
- Language-specific common errors
- Pattern count -> automation threshold
- Checked before coding, updated after bugs

**Architecture Decisions** (`learnings/architecture_decisions/ADR-NNN-*.md`):
- Design choices with rationale
- Become templates for similar contexts
- Compound across projects

**Client Communication** (`question_log.md`, `handoff_doc.md`):
- Structured questions showing understanding
- Knowledge transfer documentation
- Education, not just delivery

### Learning Flywheel

```
Project N:
  Execute with discipline
    v
  Deliver + capture domain understanding
    v
  Distill learnings (patterns, deep-dives, decisions)
    v
  Operator more capable
    v
Project N+1:
  Faster understanding (reference prior learnings)
    v
  Better questions (domain knowledge compounds)
    v
  Higher quality (patterns prevent pitfalls)
    v
  More valuable (educate, not just execute)
```

## Quick Start

### For New Projects

1. **Initialize project structure**:
   ```bash
   mkdir my-project
   cd my-project
   cp -r path/to/devos/templates/* .
   ```

2. **Create domain model**:
   - Start with client/project context
   - Document key terms and entities
   - Update as you learn more

3. **Port B: Write first spec**:
   - Use `SPEC_TEMPLATE.md`
   - Define scope explicitly (IN/OUT)
   - Mark unknowns as OPEN items
   - Specify verification criteria

4. **Port A: Execute**:
   - Load: KERNEL, now, spec, relevant patterns
   - Check bug patterns for language
   - Implement strictly from spec
   - Return friction if ambiguous
   - Update changelog

5. **Session end**:
   - Write session brief
   - Update domain model if understanding shifted
   - Capture learnings (patterns, deep-dives, decisions)
   - Update now.md

### For Existing Work

1. **Boot from now.md**: Shows current state, next action
2. **Load last session brief**: Compressed context
3. **Load task pack**: Files + specs in scope
4. **Check relevant learnings**: Patterns, domain knowledge
5. **Proceed**: Port B or Port A as appropriate

## Core Documents

**Governance**:
- [KERNEL.md](KERNEL.md) - Invariants and port contracts
- [DOCTRINE.md](DOCTRINE.md) - Operating principles
- [PORT_A_PROTOCOL.md](PORT_A_PROTOCOL.md) - Execution substrate rules
- [PORT_B_SYSTEM.md](PORT_B_SYSTEM.md) - Interpretation substrate context

**Templates**:
- [SPEC_TEMPLATE.md](templates/SPEC_TEMPLATE.md) - Specification format
- [TASK_PACK_TEMPLATE.md](templates/TASK_PACK_TEMPLATE.md) - Working set definition
- [SESSION_PACK_TEMPLATE.md](templates/SESSION_PACK_TEMPLATE.md) - End-of-session writeout

**Reference**:
- [WORKING_PAPER.md](WORKING_PAPER.md) - Technical overview of devOS
- [BOUNDARIES.md](BOUNDARIES.md) - Key boundaries and separations
- [MEMORY.md](MEMORY.md) - Memory and learning systems

## Key Principles

### Bounded Curiosity

- **Port B phase**: Maximal exploration and understanding
- **Port A phase**: Strict discipline and execution
- **Between projects**: Generalization and learning synthesis

Curiosity is channeled, not suppressed. This prevents scope creep while ensuring deep engagement.

### Understanding as Architecture

Domain modeling is not optional documentation. It's:
- Required for writing grounded specs
- Updated as understanding shifts
- Part of DONE criteria
- Client deliverable (knowledge transfer)

### Learning as Structural Output

Every session produces:
- Deliverable (code, docs, etc.)
- Learning artifacts (patterns, deep-dives, decisions)

The learning artifacts compound across projects, making each project increase operator capability.

## Value Proposition

**For clients**:
- Reliable delivery (drift prevention through governance)
- Clear communication (structured questions, documented understanding)
- Knowledge transfer (handoffs explain why, not just what)
- Domain insight (spot inconsistencies, clarify requirements)

**For operator**:
- Systematic capability development (learning flywheel)
- Context switch efficiency (re-entry discipline)
- Portfolio building (each project is credibility object)
- Tool independence (coordination above vendor surfaces)
- Sustainable practice (bounded curiosity prevents burnout)

## Status

devOS is operational and being used for actual software development work. It's being refined through active use on freelance projects.

## Examples

See [examples](../../examples/) directory for sample artifacts showing the system in use.

## Contributing

This is part of the larger Cognitive Exoskeleton framework. See main repository [CONTRIBUTING.md](../../CONTRIBUTING.md) for how to contribute.

## License

- Code and templates: MIT License
- Documentation: CC BY 4.0

See [LICENSES.md](../../LICENSES.md) for complete license text.

---

*devOS is a specialized distribution of the [Cognitive Exoskeleton framework](../..) for software development. For the general coordination protocol, see the main repository documentation.*
