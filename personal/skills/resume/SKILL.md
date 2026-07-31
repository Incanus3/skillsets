---
name: resume
description: "Reorient to a workstream from its indexed handoff or a numbered item in the latest still-valid `$workstreams` overview, refresh relevant live state, reconcile stale statements, and continue its next action. Manual invocation only: apply only if the user explicitly invokes `$resume` with no argument, a workstream slug, or a recent workstream number; never select automatically from a natural-language request."
---

# Resume a workstream

Use the handoff as a short-lived recovery aid, not as proof of current state. Refresh the relevant
authoritative systems before continuing.

## Resolve the workstream

1. Read the repository guidance and `docs/handoffs/INDEX.md`.
2. For `$resume <n>`, accept only a positive decimal integer from the latest still-valid, non-empty
   numbered `$workstreams` overview in the same conversation. An overview remains valid across zero
   or more completed `$status <n>` exchanges only when every inspection resolved successfully from
   that same overview and no other user or assistant interaction intervened. A later `$workstreams`
   response supersedes it even when the later overview is empty; any other intervening interaction
   makes it stale. Resolve the number to the exact entry at that position:
   - preserve a handoff-backed entry's slug and use its indexed handoff;
   - preserve a bead-only entry's exact `br` issue ID and use live issue state;
   - reject an absent, stale, superseded, ambiguous, or out-of-range overview instead of
     reconstructing or rerunning `$workstreams`.
3. For `$resume <slug>`, require an exact lowercase kebab-case slug and an exact indexed match.
   Reject paths, `.md` suffixes, and malformed slugs. Do not fall back to similarly named entries.
4. For bare `$resume`:
   - report that no active handoff exists when the index has no live entries;
   - select the sole live entry when exactly one exists;
   - when several exist, list their slugs and one-line purposes, ask the user to choose, and stop.
5. Treat an absent handoff file or index/file mismatch as an inconsistency; report it instead of
   guessing.

## Reorient and refresh

1. For a handoff-backed selection, read the selected handoff and only the durable references needed
   for its immediate next action. For a bead-only numeric selection, read the exact issue with
   `br show <id> --json` and query any live blocker evidence needed to establish its current state.
2. Refresh the relevant live task, workspace, and version-control state. Follow repository tool
   precedence and safety guidance before the first version-control inspection. Refresh external
   systems only when the selected workstream or next action depends on them.
3. Compare the live evidence with the recorded checkpoint. Reconcile each stale statement in the
   system that owns it. For a bead-only selection, treat the current issue and workspace as the
   checkpoint. If only a handoff's resume delta is stale, update only the handoff; never mutate
   authoritative state merely to make it match the handoff.
4. State the recovered objective, checkpoint, and immediate next action.
5. Continue the work unless a recorded human gate or newly discovered blocker requires input.

Do not copy durable specifications, task state, full logs, or transient dirty-file lists into the
handoff. Preserve a selected handoff slug for subsequent `$handoff` use.

## Complete the workstream

When the workstream finishes, first persist durable results and evidence, then close or update its
authoritative tasks. For a handoff-backed workstream, delete `docs/handoffs/<slug>.md` and its index
entry in the same change unless a specific recovery need remains. Do not keep a handoff archive by
default.
