---
title: writeOS v1 patch 1
type: patch-plan
created: 2026-01-11
status: applied
---

## Goal

Normalize non-ASCII punctuation that renders inconsistently across tooling, while keeping mapped-prose anchors coherent between Body and Binding.

## Findings (repo scan)

- `MAPPED_PROSE_FORMAT.md:21` contains `U+2014` (em dash) immediately after the substring `anchor phrases`.
- `MAPPED_PROSE_FORMAT.md:187` contains `U+2014` (em dash) in the `[C:anchor]` binding anchor phrase.
- No other non-ASCII characters were found in `*.md` under `v1.0` by a regex scan (`[^\x00-\x7F]`).

## Patch Plan

1. Replace `U+2014` with ASCII `--` in both `MAPPED_PROSE_FORMAT.md:21` and `MAPPED_PROSE_FORMAT.md:187`, keeping the body text and the `[C:anchor]` binding anchor identical.
2. Re-run the non-ASCII scan to confirm `*.md` is ASCII-only (or at least free of accidental/garbled characters).

## Status

Applied: 2026-01-11

- Updated `MAPPED_PROSE_FORMAT.md:21` and `MAPPED_PROSE_FORMAT.md:187` to replace `U+2014` (em dash) with `--`.
- Re-scan: no remaining non-ASCII characters found in `*.md` under `v1.0`.
