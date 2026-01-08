# packs/SESSION_PACK_TEMPLATE.md
SESSION_PACK template v0.1. SESSION_PACK is the durable end-of-session writeout that preserves re-entry and auditability.

Session id: S-YYYYMMDD-HHMM_<project>_<slug>
Task: <task id / name>
Runtimes used: <Port B runtime> + <Port A runtime> (or explicit port switching)

Summary (terse; 5-10 lines): intent -> action -> outcome.

Diff summary (files touched + one-line notes):
- <path>: <change note>
- <path>: <change note>

Decisions (operator/root; explicit):
- <decision id>: <decision>
- <decision id>: <decision>

Friction:
- New: <FR-...>, <FR-...>
- Remaining: <FR-...>, <FR-...>

Verification:
- Commands run: <...>
- Results: <pass/fail + brief notes>

Next actions (what now.md should point to next):
- <action + pointers to spec/changelog/friction/session>
