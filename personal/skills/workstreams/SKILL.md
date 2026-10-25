---
name: workstreams
description: "List current and ready repository workstreams by merging indexed handoffs with live authoritative task state into a concise read-only overview. Manual invocation only: apply only if the user explicitly invokes `$workstreams`; never select automatically from a natural-language request."
---

# List repository workstreams

Produce a source-neutral, read-only overview. Do not edit handoffs, update task state or
configuration, continue work, or perform version-control writes.

## Collect current work

1. Read repository guidance and locate the handoff index through that guidance or the existing
   handoff directory convention. Read every indexed handoff, extracting its slug, recorded state,
   objective, first explicit next action, and exact linked task reference.
2. Determine the authoritative task source from repository guidance. When Taskman applies, read
   `taskman-cli` for context discovery, commands, identity resolution, lifecycle, priorities, and
   failure semantics. Do not infer authority from an old task link.
3. Read live tasks and blocker evidence covering the whole relevant repository scope, including
   nested locations. Collect all current in-progress work and eligible unstarted candidates, plus
   the exact tasks linked from handoffs. Do not infer eligibility when blocker evidence is missing.
4. Preserve each task's complete qualified identity as an opaque reference. Validate incomplete or
   relative links using the authoritative source's rules before merging; never guess by title or
   an unqualified identifier. Keep unresolved references visible with a warning.
5. If authority, context, identity, or access cannot be established, stop affected queries and
   report the problem. Do not switch to an alternative writable queue. Handoff-only reporting may
   continue as a recorded partial view; do not invent task-only entries or pending counts. If the
   repository has no task source, report handoff-backed workstreams alone.

## Merge and normalize

Merge each handoff with the exact authoritative task it references. Deduplicate by its full
qualified identity, never by title. Exclude linked identities from task-only candidates; leave
unresolved links unmerged and warn. A progress state does not establish exclusive ownership.

Use exactly four overview states, with this precedence:

- `blocked`: a handoff or included task has a current blocker;
- `parked`: otherwise, the handoff is intentionally parked;
- `in-progress`: otherwise, the handoff is active or the authoritative source identifies the task
  as current in-progress work;
- `pending`: an eligible, unstarted task selected for the overview.

Handoff focus and task eligibility describe different scopes: a parked handoff linked to an
eligible task is not itself a conflict. For material conflicts, use the normalized state and
append a short warning. A terminal task linked from an unfinished handoff keeps the handoff-derived
state with a warning; it does not authorize retirement. Do not invent a fifth state or repair
source inconsistencies. When live state is unavailable, label handoff-derived results as recorded.

## Select and order entries

1. Include every handoff-backed workstream and every additional task-only in-progress workstream,
   including those normalized as blocked. Never truncate either group.
2. Count entries normalized as `in-progress`. Show no pending tasks when that count is five or more.
3. Otherwise, if fewer than eight non-pending entries exist, append the highest-priority eligible
   pending tasks until there are eight entries. Do not impose another pending cap.
4. Deduplicate all selected task identities and report how many eligible pending tasks were omitted.

Order non-pending entries as `in-progress`, `blocked`, then `parked`; within a state, use native
priority when known and then qualified identity. Put pending entries last, ordered by native
priority with a stable order for ties. Preserve the source's priority names and ordering rather
than inventing a cross-tracker scale.

## Format the overview

Number entries consecutively from 1 in final display order. Use one physical line per workstream
when practical, with state and known native priority in brackets, followed by the handoff slug or
qualified task reference, objective, and `Next:` action. Derive `Next:` from the first explicit
handoff action or current task evidence; use `Next: unknown` rather than inventing an action.
Retain the full linked task identity and its context in the overview snapshot even when a slug
is displayed. Preserve any unresolved-reference or source-conflict warning. Do not expose raw
source labels or lifecycle values as extra overview states.

Numbers are ephemeral selectors for `$status <n>` or `$resume <n>` in this conversation. Successful
read-only `$status <n>` inspections resolved from this same overview preserve its mapping for
another `$status <n>` or `$resume <n>`. Any other intervening user or assistant interaction makes
it stale. A later `$workstreams` response supersedes it even when the later overview is empty.
The snapshot must retain each entry's exact identity, objective, state, priority, next action, and
warning so numeric status needs no live lookup.

After a non-empty overview, report `Resume with $resume <n> or inspect with $status <n>; after an
inspection, the same number remains available to $resume <n>.` If empty, report `No current or ready
workstreams.` without the selector hint.
