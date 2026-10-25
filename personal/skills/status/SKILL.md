---
name: status
description: "Report the concise recorded status of a workstream from its indexed handoff or a numbered item in the latest still-valid `$workstreams` overview without refreshing live systems or continuing the work. Manual invocation only: apply only if the user explicitly invokes `$status` with no argument, a workstream slug, or a recent workstream number; never select automatically from a natural-language request."
---

# Report recorded workstream status

Remain strictly read-only. Do not edit handoffs or the index, refresh any live task, binding,
workspace, or version-control state, enrich context, or continue work. This recorded-only boundary
applies even when normal repository orientation requests live queries.

## Resolve the workstream

1. Read repository guidance and locate its handoff index through that guidance or the existing
   handoff directory convention.
2. For `$status <n>`, accept only a positive decimal integer from the latest still-valid, non-empty
   numbered `$workstreams` overview in this conversation. It remains valid across zero or more
   successful `$status <n>` inspections resolved from that same overview, with no other intervening
   user or assistant interaction. Any other interaction makes it stale; a later overview supersedes
   it even when empty. Resolve the exact entry, preserving its handoff slug or opaque qualified task
   identity and recorded snapshot. Reject absent, stale, superseded, ambiguous, or out-of-range
   selectors without reconstructing or rerunning the overview.
3. For `$status <slug>`, require an exact lowercase kebab-case slug and indexed match. Reject paths,
   `.md` suffixes, malformed slugs, and similarly named substitutes.
4. For bare `$status`, select the sole live handoff; report none when the index has no live entries.
   If several exist, list their slugs and one-line purposes, ask the user to choose, and stop.
5. For a handoff-backed selection, read only that handoff after resolving it. Report an absent file
   or index/file mismatch rather than guessing. For a task-only numeric selection, use only the
   selected overview's snapshot; do not query a tracker or resolve its context.

## Report

Summarize the handoff as recorded:

- workstream slug and objective;
- recorded status and updated date;
- current phase or checkpoint;
- the next one to three actions;
- blocker and reason, if blocked;
- pending decision, prerequisite, or human gate.

Mark missing fields as `unknown`. Optionally name durable references already recorded, without
following them to enrich the report. Keep relative or unresolved task references exactly as
recorded; do not inspect live context to complete their identity. Explicitly identify the result
as recorded status, not freshly verified state.

For a task-only numeric selection, report only its recorded qualified identity, objective, state,
native priority, `Next:` action, and warning. Mark other requested fields as `unknown` and label the
result as the selected overview's status snapshot. A successful `$status <n>` read preserves that
overview's selector mapping for another numeric inspection or resume.
