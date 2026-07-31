---
name: status
description: "Report the concise recorded status of a workstream from its indexed handoff or a numbered item in the immediately preceding `$workstreams` overview without refreshing live systems or continuing the work. Manual invocation only: apply only if the user explicitly invokes `$status` with no argument, a workstream slug, or a recent workstream number; never select automatically from a natural-language request."
---

# Report recorded workstream status

Remain strictly read-only. Do not edit the handoff or index, refresh task or workspace state, make
version-control changes, or continue the workstream.

## Resolve the workstream

1. Read the repository guidance and `docs/handoffs/INDEX.md`.
2. For `$status <n>`, accept only a positive decimal integer when the immediately preceding assistant
   response in the same conversation was a non-empty numbered `$workstreams` overview. Resolve the
   number to the exact entry at that position:
   - preserve a handoff-backed entry's slug and use its indexed handoff;
   - preserve a bead-only entry's exact `br` issue ID and the status snapshot in that overview;
   - reject an absent, stale, ambiguous, or out-of-range list instead of reconstructing or rerunning
     `$workstreams`.
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
`unknown`. Explicitly identify the result as the immediately preceding overview's status snapshot,
not freshly verified live state.
