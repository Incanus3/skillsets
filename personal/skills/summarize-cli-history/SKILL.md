---
name: summarize-cli-history
description: "Reconstruct or summarize work from historical Augment, Codex, or other CLI session archives across multiple days. Manual invocation only: apply only if the user explicitly invokes `$summarize-cli-history`; never select automatically from a natural-language request."
---

# Summarize CLI History

Produce a trustworthy, privacy-preserving timeline from local CLI session archives. Do not mistake a sampled or
context-truncated review for an exhaustive one.

## Contract

Require a date range. Default the reporting timezone to `Europe/Prague` unless the user specifies another timezone.
Default to demonstrated active intervals when per-turn or event timestamps exist and to session envelopes otherwise;
do not ask the user to confirm these defaults. Treat creation/modification timestamps as an envelope unless the
archive supplies per-turn timestamps.

Never expose secrets, credentials, raw transcripts, or full prompts. Report only the requested summaries.

## Required workflow

1. **Discover and inventory.** Locate archive roots; ledger every in-range file with source, stable ID/path,
   start, end, size, and state (`empty`, `pending`, `reviewed`, or `unreadable`). Place cross-midnight activity on
   the correct day when event timestamps exist.
2. **Choose bounded units.** Read short sessions directly. Split large sessions by outer conversation turns or
   chronological slices, never nested tool/exchange counts. Never delegate an entire long archive or open-ended
   date range.
3. **Record as you go.** After each unit, add its project, a terse topic/outcome, and coverage state. Derive the
   project from the final non-empty path segment of the archive's recorded workspace root. Prefer the workspace root
   over a transient command working directory; use `unknown` when no trustworthy workspace path exists. Delegates
   must return exact IDs/ranges plus uncertainty; sampling is not coverage.
4. **Reconcile coverage.** Account for every inventory entry before synthesis; explicitly mark zero-content
   sessions. Re-read unreadable, mismatched, or contradictory records in smaller units. Do not call the result
   exhaustive while any substantive entry is pending.
5. **Merge deliberately.** Convert times to the requested timezone. Merge concurrent sessions only when clearly
   the same work in the same project; retain distinct projects, themes, and meaningful gaps. Mark broad/incomplete
   envelopes as intermittent.
6. **Report.** Group by day. Format every record as `local hour range — project — factual work summary`, placing the
   project immediately after the time range and before the description. State empty days.

## Ledger shape

Keep only metadata and distilled findings, never copied transcripts:

| Source | ID | Local range | Project | Coverage | Topic/outcome | Timing caveat |
|---|---|---|---|---|---|---|

For large audits, keep the ledger in coordinator notes or a compact scratch artifact so parallel reviewers cannot
lose findings. Remove or omit it after reporting unless the user asks to retain it.

## Quality gates

- Ledger count matches inventory after explicit empty/unreadable exclusions.
- Every non-empty session is directly reviewed or covered by a named bounded result.
- Every reported record has a project derived from a trustworthy workspace root or explicitly marked `unknown`.
- Reject conclusions from reviewers that sampled, ran out of context, or cannot identify covered IDs.
- Replace an incomplete prior answer plainly; do not blend in unverified claims.

## Common mistakes

| Mistake | Required correction |
|---|---|
| Delegate a full week of multi-megabyte logs | Partition by identified sessions/turn slices and collect a ledger. |
| Use filesystem modification time as active work time | Call it a session envelope unless event timestamps prove activity. |
| Merge overlapping but unrelated work | Keep distinct thematic records under the same day. |
| Merge related work from different projects into one record | Keep separate records so each has one accurate project. |
| Trust a plausible aggregate without coverage IDs | Treat it as a lead, not evidence; review the missing sessions. |
