---
name: handoff
description: "Maintain concise, short-lived workstream handoffs in `docs/handoffs/`. Use automatically when meaningful work changes what a fresh session needs to continue, including after completing a design, plan, or implementation phase, changing direction, finding a blocker, or making relevant decisions or discoveries; when a session resumed from a handoff and its continuation state changes; when the operator explicitly confirms completion of a workstream with an existing handoff; or when context-window pressure threatens continuity. Also use for `$handoff` and explicit natural-language requests to prepare work for a new session."
---

# Maintain a workstream handoff

Treat the workstream slug as the public identity. Store it internally at
`docs/handoffs/<slug>.md`, and keep `docs/handoffs/INDEX.md` synchronized.

## Choose the operating mode

- **Automatic maintenance:** Create or update the handoff after a meaningful checkpoint that
  changes the immediate continuation state. If the session resumed from a handoff, keep that
  handoff current as meaningful work, decisions, or discoveries accumulate. Do not announce a
  resume command or interrupt ongoing work merely because the file was refreshed.
- **Explicit handoff:** Treat `$handoff`, "do a handoff", or a request to continue the work in a
  new session as an immediate handoff request. Update the handoff and finish by returning its
  copy-ready resume command.
- **Context pressure:** When the remaining context appears likely to endanger continuity, update or
  create the handoff promptly. Prefer the nearest clean checkpoint when it is close and safe, but
  do not risk compaction while waiting for one. Tell the requester that the assessment is
  heuristic, recommend a fresh session now or at the identified checkpoint, and offer the resume
  command conditionally.

Do not create or refresh a handoff for routine progress, small edits, or details that do not affect
resumption. Do not create one when the operator has explicitly confirmed workstream completion and nothing
remains to resume.

## Resolve the workstream

1. Read the repository guidance and its handoff workflow when present.
2. For `$handoff <slug>`, require an exact lowercase kebab-case slug. Reject paths, `.md`
   suffixes, malformed slugs, and silent fallback to a similar name.
3. For any trigger without an explicit slug, reuse the slug from which the current session resumed.
   If the session did not resume from a handoff, derive a meaningful non-colliding slug and report
   it only when the handoff was explicitly requested.
4. Update an existing matching handoff in place; otherwise create its file and index entry.
5. Never overwrite an unrelated handoff or silently fall back to a similar slug.

## Preserve authority

Before writing the handoff, harvest durable results into their owning systems:

- specifications, decisions, reusable findings, and experiment evidence into canonical documents;
- repository-local tasks, dependencies, and evidence into the repository task tracker;
- higher-level commitments into their designated system when it is operational.

Link those authorities from the handoff. Do not copy their full content or turn the handoff into a
task tracker.

## Preserve agreed continuation state

Preserve the operator-agreed execution sequence, dependencies, pending decisions, and
authorization or verification gates across handoff updates. Agreed remaining work is not
speculative backlog.

Every updated handoff must include the agreed remaining steps in order and the current position,
or link to a canonical document containing the complete sequence. Keep agreed unfinished steps
even when they lie beyond the immediate next increment. Preserve each step's dependencies and gates.
When asked to shorten a handoff, compress each agreed unfinished step rather than omitting it.

Update the current position and retire completed instructions without dropping unfinished
commitments. Concision must not erase information needed to continue the agreed work.

Before removing or materially shortening such information, verify that it is completed,
explicitly superseded, or preserved in a canonical document linked from the handoff. Repository
history alone is not sufficient preservation.

Review the handoff diff before finishing: account for every removed commitment or gate and verify
that the remaining sequence is still discoverable.

## Write the current resume state

Keep the handoff concise and current. Include:

- status (`active`, `blocked`, or `parked`), updated date, and `$resume <slug>`;
- objective and intended outcome;
- durable references, including the relevant task identifier when one exists;
- current checkpoint and what is already complete;
- immediate next actions in order, the operator-agreed remaining sequence, and current position;
- blockers, pending decisions, prerequisites, and constraints;
- latest verification evidence and unresolved uncertainty;
- failed attempts or temporary assumptions only when needed to prevent repeated work;
- relevant skill requirements or environment cautions when they materially affect continuation.

Do not include secrets, chat transcripts, full logs, copied acceptance criteria, or a transient list
of dirty files. When repository state materially affects continuation, record only the stable
revision, bookmark, branch, or caution needed to resume safely.

## Retire completed handoffs

Retire a handoff only after the operator explicitly confirms that the workstream is complete.
Passed checks, completed plan steps, closed tasks, commits, pushes, merge or deployment do not
substitute for that confirmation. Without it, keep the handoff current with the verified baseline,
remaining steps and gates, or the pending decision about what comes next.

After explicit confirmation, capture remaining durable information and update authoritative task
state before removing or archiving the handoff according to repository policy. Synchronize its
index or resume-command registry. Retire completed handoffs only when nothing remains to resume;
if confirmation conflicts with known unfinished commitments, resolve that scope with the operator.

## Synchronize and verify

Add or update one grep-friendly line in `docs/handoffs/INDEX.md` with the file link, recorded state,
purpose, and the command that uses it. Verify that linked durable references resolve and that the
handoff contains no sensitive or duplicated canonical material.

For an explicit handoff request, finish by returning `$resume <slug>` without block-quote
formatting. Under context pressure, phrase it conditionally, such as: "If you decide to continue in
a fresh session: `$resume <slug>`." For automatic maintenance, do not print the command.

Handoff maintenance does not itself authorize committing or pushing. Preserve any authorization
already established by the user or active workflow. Do not alter unrelated task state.
