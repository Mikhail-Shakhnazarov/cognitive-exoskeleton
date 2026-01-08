# KERNEL.md
Work-OS kernel v0.1. Kernel = the minimal invariant set (must remain true) plus the minimal interface set (artifact shapes) that keeps the system bootable, resumable, and auditable.

Model context window = cache: fast, limited, volatile working space. Repo files = memory: durable state that can be reloaded and diffed. Correctness must not depend on vendor-side conversation memory or hidden compaction; chat is scratch unless committed into artifacts.

Operator = root (final authority). All decision loops terminate at the operator: accept, defer (OPEN), or refuse. Nothing becomes true by vibe; decisions become true only when committed into canonical artifacts.

Port = a constrained role (process) with a contract. Port separation is process isolation: meaning decisions and execution changes coordinate only through artifacts, not through assumed shared context.

Port B (meaning/spec) stabilizes intent, writes/updates specs, records decisions explicitly, emits friction for missing decisions, and writes session briefs (compressed memory). Port B does not silently close OPEN items. Reference: [Port B system](PORT_B_SYSTEM.md).

Port A (execution/diffs) implements strictly from the spec, produces diffs (exact file changes), runs verification, and appends changelog entries. Port A does not invent requirements; ambiguity returns friction. Reference: [Port A protocol](PORT_A_PROTOCOL.md).

Runtimes are replaceable. â€œModel-agnosticâ€ means: the kernel does not depend on a specific vendor surface. Optional tool shims may exist, but they are non-authoritative bootloaders that only point to canonical artifacts.

Constrained runtimes exist. In some environments only the OS core is mounted (no projects). In such runs, only kernel/packs/templates/patterns are edited; project userland enters only as an explicitly scoped snapshot pack.

## Canonical artifacts (ABI)
ABI = the required shape of artifacts so components compose across tools. The OS runs on artifacts, not on transcript replay.

- [now.md](now.md) is the process table and boot surface. It yields the next correct action quickly on cold start and points to canonical state.
- Specs are structured requests (â€œsyscallâ€ analogy): a standardized request from Port B to Port A so execution proceeds without inventing meaning. Template: [packs/SPEC_TEMPLATE.md](SPEC_TEMPLATE.md).
- Friction is typed blocked state (error-return equivalent, but human-decidable). Log: [friction/FRICTION_LOG.md](FRICTION_LOG.md).
- Changelog is append-only journal of state transitions. Log: [logs/changelog.md](changelog.md).
- Session briefs are compressed memory written at session end for re-entry. Folder: [sessions/](sessions/).
- Patterns are reusable pitfalls/idioms captured after repeat failures. Folder: [patterns/](patterns/).

## Commit cadence
Commit = writing new meaning into canonical artifacts. Without commits, deltas live only in chat and are lost on reboot.

When a requirement/decision appears: commit to the active spec immediately.
When ambiguity appears: create a friction item immediately.
When a session ends: write a session brief, append changelog, update now.md.

## Packs (working sets; cache discipline)
Pack = curated bundle of artifacts loaded into a runtime for a specific operation.

Hot set = always-loaded files that prevent category errors. Warm set = per-task working set. Cold set = archive retrieved on demand.

Packs:
- [packs/BOOT_PACK.md](BOOT_PACK.md)
- [packs/TASK_PACK_TEMPLATE.md](TASK_PACK_TEMPLATE.md)
- [packs/SESSION_PACK_TEMPLATE.md](SESSION_PACK_TEMPLATE.md)

## Definition of DONE
A task is DONE when requirements are satisfied (or explicitly deferred), verification ran and is recorded, a changelog entry is appended, a session brief exists, and now.md reflects the updated next action.

## Kernel change control
Kernel changes are rare and small. A new rule enters the kernel only if it prevents a recurring category error observed in operation. The kernel stays short so it stays loadable.

Reference texts (non-hot by default): [Doctrine](DOCTRINE.md), [Boundaries](BOUNDARIES.md), [Memory](MEMORY.md).
