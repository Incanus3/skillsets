---
name: status
description: "Report the concise recorded status of a workstream from its indexed handoff or a numbered item in the latest still-valid `$workstreams` overview without refreshing live systems or continuing the work. Manual invocation only: apply only if the user explicitly invokes `$status` with no argument, a workstream slug, or a recent workstream number; never select automatically from a natural-language request."
---

# Report recorded workstream status

Remain strictly read-only. Do not edit the handoff or index, refresh task or workspace state, make
version-control changes, or continue the workstream.

## Resolve the workstream

1. Read the repository guidance and `docs/handoffs/INDEX.md`.
2. For `$status <n>`, accept only a positive decimal integer from the latest still-valid, non-empty
   numbered `$workstreams` overview in the same conversation. An overview remains valid across zero
   or more completed `$status <n>` exchanges only when every inspection resolved successfully from
   that same overview and no other user or assistant interaction intervened. A later `$workstreams`
   response supersedes it even when the later overview is empty; any other intervening interaction
   makes it stale. Resolve the number to the exact entry at that position:
   - preserve a handoff-backed entry's slug and use its indexed handoff;
   - preserve a bead-only entry's exact `br` issue ID and the status snapshot in that overview;
   - reject an absent, stale, superseded, ambiguous, or out-of-range overview instead of
     reconstructing or rerunning `$workstreams`.
3. For `$status <slug>`, require an exact lowercase kebab-case slug and an exact indexed match.
   Reject paths, `.md` suffixes, and malformed slugs. Do not fall back to similarly named entries.
4. For bare `$status`:
   - report that no active handoff exists when the index has no live entries;
   - select the sole live entry when exactly one exists;
   - when several exist, list their slugs and one-line purposes, ask the user to choose, and stop.
5. For a handoff-backed selection, read only the selected handoff. Treat an absent file or
   index/file mismatch as an inconsistency; report it instead of guessing. Do not query `br` for a
   bead-only numeric selection.

## Report

Summarize the handoff as recorded:

- workstream slug and objective;
- recorded status and updated date;
- current phase or checkpoint;
- the next one to three actions;
- blocker and reason, if blocked;
- pending decision, prerequisite, or human gate.

Mark missing fields as `unknown`; do not infer them from external or live state. Optionally name the
primary durable references needed for context. Explicitly say that the result is recorded status,
not freshly verified live state.

For a bead-only numeric selection, report only the exact issue ID, objective, state, priority,
`Next:` action, and warning available in the selected overview entry. Mark other requested fields as
`unknown`. Explicitly identify the result as the selected overview's status snapshot, not freshly
verified live state.
