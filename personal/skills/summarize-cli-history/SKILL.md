---
name: summarize-cli-history
description: Reconstruct or summarize work from historical Augment, Codex, or other CLI session archives across multiple days. Manual invocation only: apply only if the user explicitly invokes `$summarize-cli-history`; never select automatically from a natural-language request.
---

# Summarize CLI History

Produce a trustworthy, privacy-preserving timeline from local CLI session archives. Do not mistake a sampled or
context-truncated review for an exhaustive one.

## Contract

Confirm the date range, reporting timezone, and whether the user wants session envelopes or demonstrated active
intervals. Treat creation/modification timestamps as an envelope unless the archive supplies per-turn timestamps.

Never expose secrets, credentials, raw transcripts, or full prompts. Report only the requested summaries.

## Required workflow

1. **Discover and inventory.** Locate archive roots; ledger every in-range file with source, stable ID/path,
   start, end, size, and state (`empty`, `pending`, `reviewed`, or `unreadable`). Place cross-midnight activity on
   the correct day when event timestamps exist.
2. **Choose bounded units.** Read short sessions directly. Split large sessions by outer conversation turns or
   chronological slices, never nested tool/exchange counts. Never delegate an entire long archive or open-ended
   date range.
3. **Record as you go.** After each unit, add a terse topic/outcome and coverage state. Delegates must return
   exact IDs/ranges plus uncertainty; sampling is not coverage.
4. **Reconcile coverage.** Account for every inventory entry before synthesis; explicitly mark zero-content
   sessions. Re-read unreadable, mismatched, or contradictory records in smaller units. Do not call the result
   exhaustive while any substantive entry is pending.
5. **Merge deliberately.** Convert times to the requested timezone. Merge concurrent sessions only when clearly
   the same work; retain distinct themes and meaningful gaps. Mark broad/incomplete envelopes as intermittent.
6. **Report.** Group by day. Each record has a local hour range and one factual work summary; state empty days.

## Ledger shape

Keep only metadata and distilled findings, never copied transcripts:

| Source | ID | Local range | Coverage | Topic/outcome | Timing caveat |
|---|---|---|---|---|---|

For large audits, keep the ledger in coordinator notes or a compact scratch artifact so parallel reviewers cannot
lose findings. Remove or omit it after reporting unless the user asks to retain it.

## Quality gates

- Ledger count matches inventory after explicit empty/unreadable exclusions.
- Every non-empty session is directly reviewed or covered by a named bounded result.
- Reject conclusions from reviewers that sampled, ran out of context, or cannot identify covered IDs.
- Replace an incomplete prior answer plainly; do not blend in unverified claims.

## Common mistakes

| Mistake | Required correction |
|---|---|
| Delegate a full week of multi-megabyte logs | Partition by identified sessions/turn slices and collect a ledger. |
| Use filesystem modification time as active work time | Call it a session envelope unless event timestamps prove activity. |
| Merge overlapping but unrelated work | Keep distinct thematic records under the same day. |
| Trust a plausible aggregate without coverage IDs | Treat it as a lead, not evidence; review the missing sessions. |