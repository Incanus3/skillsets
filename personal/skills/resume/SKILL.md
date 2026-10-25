---
name: resume
description: "Reorient to a workstream from its indexed handoff or a numbered item in the latest still-valid `$workstreams` overview, refresh relevant live state, reconcile stale statements, and continue its next action. Manual invocation only: apply only if the user explicitly invokes `$resume` with no argument, a workstream slug, or a recent workstream number; never select automatically from a natural-language request."
---

# Resume a workstream

Use the handoff as a short-lived recovery aid, not proof of current state. Refresh relevant
authoritative systems before continuing.

## Resolve the workstream

1. Read repository guidance and locate its handoff index through that guidance or the existing
   handoff directory convention.
2. For `$resume <n>`, accept only a positive decimal integer from the latest still-valid, non-empty
   numbered `$workstreams` overview in this conversation. It remains valid across zero or more
   successful `$status <n>` inspections resolved from that same overview, with no other intervening
   user or assistant interaction. Any other interaction makes it stale; a later overview supersedes
   it even when empty. Resolve the exact entry, preserving its handoff slug or opaque qualified task
   identity. Reject absent, stale, superseded, ambiguous, or out-of-range selectors without
   reconstructing or rerunning the overview.
3. For `$resume <slug>`, require an exact lowercase kebab-case slug and indexed match. Reject paths,
   `.md` suffixes, malformed slugs, and similarly named substitutes.
4. For bare `$resume`, select the sole live handoff; report none when the index has no live entries.
   If several exist, list their slugs and one-line purposes, ask the user to choose, and stop.
5. Report an absent handoff or index/file mismatch rather than guessing.

## Reorient and refresh

1. For a handoff-backed selection, read its handoff and only the durable references needed for its
   immediate next action. Preserve its objective, agreed sequence, dependencies, and gates. A task-only
   selection uses the current authoritative task and workspace as its checkpoint.
2. Determine the authoritative task source from repository guidance. When Taskman applies, read
   `taskman-cli` for context discovery, commands, identity resolution, lifecycle, priorities, and
   failure semantics. Validate the exact qualified or relative reference under that source's rules;
   never guess by title or substitute an unqualified identity. Keep unresolved references visible.
3. Refresh the relevant task, thread, blockers, workspace, and version-control state, following
   repository tool precedence and safety guidance. Refresh external systems only when the next
   action depends on them. If authority, context, identity, or access is unresolved, stop affected
   operations and report the problem; do not choose an alternative writable queue or continue work
   dependent on missing evidence.
4. Compare live evidence with the recorded checkpoint. Reconcile stale statements in the system
   that owns them. If only the handoff's resume delta is stale, update only the handoff; never change
   authoritative task state merely to match it. Preserve unresolved conflicts and warnings.
5. Establish assignment authority before acting. An explicit operator resume request selecting a
   nonterminal task may assign its already agreed scope, subject to existing gates. Discovery,
   readiness, configuration, or an old handoff alone does not assign work. Read the task, thread,
   and blockers before authorized bounded updates or evidence comments, and verify mutations.
   Coordinate ownership before concurrent work; progress state is not a claim or lock. A resume
   request does not authorize terminal decisions, reopening, deletion, new tasks, or material scope
   or priority changes; those need their own operator decisions.
6. State the recovered objective, checkpoint, and immediate next action, then continue the scoped,
   authorized work unless a recorded gate or newly discovered blocker requires input.

Keep durable specifications, task state, full logs, and transient dirty-file lists out of the
handoff. Preserve a selected handoff slug for subsequent `$handoff` use.

## Complete the workstream

Persist durable results and verification evidence in their canonical owners and maintain the
handoff through the handoff skill. Report technical readiness separately from operator acceptance;
finished implementation or passing checks do not authorize task completion or other terminal
changes. Follow the authoritative source's skill for any separately authorized task mutation.

Retire a handoff only after the operator explicitly confirms that the workstream is complete,
following global policy and the handoff skill. Until then preserve the current baseline, remaining
actions and gates, or pending next-step decision. After confirmation, remove the handoff and its
index entry together; do not keep a handoff archive by default.
