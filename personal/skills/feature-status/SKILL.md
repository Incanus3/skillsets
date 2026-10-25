---
name: feature-status
description: "Assess the current feature's status from branch documentation and its authoritative repository tracker, then identify next steps. Manual invocation only: apply only if the user explicitly invokes `$feature-status`; never select automatically from a natural-language request."
---

# Assess the current feature

Keep the assessment read-only. Read repository guidance and its documentation index, then inspect
feature documentation changed on the current branch and the exact related authoritative tasks.
Follow only the references needed for scope, acceptance criteria, evidence, blockers, and next actions.

Follow repository version-control tool precedence before inspection. Use the actual comparison
target rather than assuming a branch name. Stop on stale working-copy state; do not change branches,
repair the workspace, or perform version-control writes.

Determine the authoritative task source from repository guidance. When Taskman applies, read
`taskman-cli` for context discovery, commands, identity resolution, lifecycle, priorities, and failure
semantics. Preserve each task's full qualified identity and validate relative references using the
source's rules. Never guess by title or an unqualified identifier. Inspect relevant tasks, threads,
and blockers; preserve native priority and context. Progress state is not an exclusive claim.

If authority, context, identity, or access is unresolved, stop affected queries and report the problem
without choosing an alternative writable queue. Keep unresolved references and warnings visible.
Documentation-only findings may still be reported with the resulting uncertainty.

Report the feature objective, documented checkpoint, completed evidence, remaining work, blockers
or human gates, and immediate next steps. Distinguish documented assertions from verified current
task state; mark unavailable evidence as `unknown`. Technical readiness does not authorize lifecycle
changes, completion, publication, or handoff retirement. Do not mutate tasks or retire handoffs.
