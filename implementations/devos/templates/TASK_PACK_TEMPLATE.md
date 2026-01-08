# packs/TASK_PACK_TEMPLATE.md
TASK_PACK template v0.1. TASK_PACK is the per-task warm working set: the minimum sufficient state to execute coherently without transcript replay.

Task identity: <task id / short name> | <date> | <operator>

Canonical artifacts:
- Spec: spec/<task>.md
- Changelog tail: logs/changelog.md (last N entries; default N=10)
- Friction: friction/FRICTION_LOG.md (only relevant ids)

Files in scope (curated; avoid repo-wide dumps):
- <path 1>
- <path 2>
- <path 3>

Commands/environment:
- build: <command or n/a>
- test: <command or n/a>
- lint/format: <command or n/a>
- run: <command or n/a>

Verification hook (copied from spec):
- <what must be true after execution; include exact commands/checks>
