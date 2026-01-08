# Examples

Sample artifacts demonstrating the Cognitive Exoskeleton framework and devOS implementation in action.

## Sample Artifacts

The `sample_artifacts/` directory contains example files showing the system's artifact types:

### [sample_spec.md](sample_artifacts/sample_spec.md)
Complete specification for a user authentication module. Demonstrates:
- Structured requirements (MUST/SHOULD/MAY)
- Explicit scope boundaries (IN/OUT)
- OPEN items requiring operator decisions
- Verification criteria
- Lifecycle tracking

**Key features:**
- Clear acceptance criteria for each requirement
- Constraints and security considerations documented
- Pattern references (linking to bug pattern database)
- Related architecture decision references

### [sample_friction_log.md](sample_artifacts/sample_friction_log.md)
Friction log showing typed blocked states. Demonstrates:
- Different friction types (semantic, feasibility, scope)
- Structured decision options with trade-offs
- Resolution tracking with rationale
- Status progression (OPEN → RESOLVED)

**Key features:**
- Explicit options enumeration (no hidden choices)
- Impact analysis for each option
- Provenance (who decided, when, why)
- Links to relevant specs and decisions

### [sample_changelog.md](sample_artifacts/sample_changelog.md)
Append-only state transition journal. Demonstrates:
- Concrete change documentation
- Verification status tracking
- Friction linkage
- Audit trail maintenance

**Key features:**
- Timestamp and artifact type for each entry
- Spec references showing requirement satisfaction
- Verification checkboxes (passed, failed, pending)
- Friction creation and resolution tracking

## How These Connect

These artifacts form a coordinated system:

1. **Spec defines** what should be built (requirements, scope, verification)
2. **Friction surfaces** when execution can't proceed (ambiguity, unknowns)
3. **Changelog records** what actually happened (diffs, decisions, evidence)
4. **Session briefs** (not shown) compress these for re-entry

Together they create:
- **Auditability**: Can trace decisions back to requirements
- **Re-enterability**: Can resume work after time gaps
- **Learning**: Can extract patterns from successes/failures
- **Verification**: Can confirm claims against evidence

## Using These Examples

### As Templates

Copy and modify for your own projects:
```bash
cp examples/sample_artifacts/sample_spec.md my-project/specs/SPEC-001.md
# Edit to match your requirements
```

### As Reference

Study these to understand:
- How detailed specifications should be
- What makes good friction items
- How to write audit-trail changelogs
- How artifacts cross-reference each other

### As Validation

Check your own artifacts against these:
- Are your specs similarly structured?
- Do your friction items enumerate options?
- Do your changelogs link to specs?
- Is verification status explicit?

## Additional Examples

More examples will be added as the framework is used in real projects:
- Complete project case studies
- Domain model examples
- Architecture decision records
- Session brief samples
- Learning artifact examples (patterns, deep-dives)

## Contributing Examples

Have you used the framework and want to share sanitized examples? 

See [CONTRIBUTING.md](../CONTRIBUTING.md) for how to submit. Good examples:
- Show real problems and solutions
- Include both successes and failures
- Preserve the reasoning and decisions
- Are sanitized for any confidential content

---

*Part of the [Cognitive Exoskeleton](../) framework documentation.*
