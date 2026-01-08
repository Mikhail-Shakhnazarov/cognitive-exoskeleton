# Memory

## Contents
- CHANGELOG.md
- LEARNINGS.md
- BUG_PATTERNS.md

---

## CHANGELOG.md

> Source: `CHANGELOG.md`

# Changelog

Port A execution log. Append-only.

---

## Log

## [2025-12-30T00:00] BOOTSTRAP
- **Added:** Full exoskeleton infrastructure
- **Added:** Research library (9 concepts x 3 tiers)
- **Added:** PORT_B_SYSTEM.md, PORT_A_PROTOCOL.md, DOCTRINE.md
- **Added:** Templates (now.md, spec.md, session.md, changelog.md)
- **Added:** Patterns (BUG_PATTERNS.md, LEARNINGS.md, idioms/*)
- **Added:** Tooling (install.sh, new-project.sh, save-session.sh)
- **Open:** Session auto-save mechanism not yet tested
- **Open:** Codex integration not yet tested

## LEARNINGS.md

> Source: `LEARNINGS.md`

# Learnings

Cross-project insights. Higher-level than bug patterns. Distilled from sessions.

---

## Process

**Session persistence compounds.** Saved sessions enable "we decided X in the session on Y" rather than reconstruction. Worth the save friction. (2025-01)

**Bugs are data.** Pattern accumulation creates self-correction. A bug fixed once prevents that bug everywhere. (2025-01)

**Context investment pays.** Loading full context on first pass beats clarification roundtrips. Frontier models have capacity; use it. (2025-01)

**Parallel beats pipeline.** Port B and Port A can work simultaneously. Operator coordinates; no need to wait. (2025-01)

---

## Architecture

**Port separation localizes failure.** Spec wrong Port B. Execution wrong Port A. Mixed interpretation/execution hides the source. (2025-01)

**Operator termination is architecture.** Not ethics, not preference. Creates accountability, quality control, reversibility. (2025-01)

---

## Writing

**Terse is diagnostic.** If it can't be stated tersely, it's not stable. Noun proliferation and caveat chains signal unstable concepts. (2025-01)

---

## Anti-Patterns

_(what didn't work and why -- add as discovered)_

## BUG_PATTERNS.md

> Source: `BUG_PATTERNS.md`

# Bug Patterns

Cross-project pattern memory. Port A consults before writing, appends after encountering.

---

## Usage

**Before:** Check section for target language. Note high-count patterns.

**After bug:** Fix it, append here (new row or increment count).

**Count 6+:** Consider tooling or lint solution.

---

## SuperCollider

| ID | Pattern | Fix | Count |
|----|---------|-----|-------|
| SC-001 | var not at function top | All var statements first line of block | 0 |
| SC-002 | SynthDef name as string | Use `\symbol` not `"string"` | 0 |
| SC-003 | Rate mismatch ar/kr | Explicit `.ar` or `.kr` on all UGens | 0 |
| SC-004 | Server not booted | Wrap in `s.waitForBoot { }` | 0 |
| SC-005 | Missing doneAction | Add `doneAction: 2` to EnvGen | 0 |
| SC-006 | Stereo confusion | Use `sig ! 2` for array expansion | 0 |

---

## Python

| ID | Pattern | Fix | Count |
|----|---------|-----|-------|
| PY-001 | OSC type ambiguity | Explicit `float()`, `int()` before send | 0 |
| PY-002 | Mutable default arg | Use `None`, then `x = x or []` | 0 |
| PY-003 | Bare except | Specify exception type | 0 |
| PY-004 | Threading without lock | Use `threading.Lock()` for shared state | 0 |

---

## JavaScript / React

| ID | Pattern | Fix | Count |
|----|---------|-----|-------|
| JS-001 | State mutation | Spread: `{...state, key: val}` | 0 |
| JS-002 | useEffect missing dep | Include all refs in deps array | 0 |
| JS-003 | Missing key in map | Stable unique key prop | 0 |
| JS-004 | Handler recreated each render | Wrap in `useCallback` | 0 |

---

## General

| ID | Pattern | Fix | Count |
|----|---------|-----|-------|
| GEN-001 | Hardcoded config | Extract to constants | 0 |
| GEN-002 | Silent error swallow | Log or surface all errors | 0 |
| GEN-003 | Magic numbers | Comment or named constant | 0 |
