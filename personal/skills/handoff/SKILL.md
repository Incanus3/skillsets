---
name: handoff
description: "Maintain concise, short-lived workstream handoffs in `docs/handoffs/`. Use automatically when meaningful work changes what a fresh session needs to continue, including after completing a design, plan, or implementation phase, changing direction, finding a blocker, or making relevant decisions or discoveries; when a session resumed from a handoff and its continuation state changes; when a workstream with an existing handoff completes; or when context-window pressure threatens continuity. Also use for `$handoff` and explicit natural-language requests to prepare work for a new session."
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
resumption. Do not create one when the workstream is complete and nothing remains to resume.

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

## Write only the resume delta

Keep the handoff concise and current. Include:

- status (`active`, `blocked`, or `parked`), updated date, and `$resume <slug>`;
- objective and intended outcome;
- durable references, including the relevant task identifier when one exists;
- current checkpoint and what is already complete;
- immediate next actions in order;
- blockers, pending decisions, prerequisites, and constraints;
- latest verification evidence and unresolved uncertainty;
- failed attempts or temporary assumptions only when needed to prevent repeated work;
- relevant skill requirements or environment cautions when they materially affect continuation.

Do not include secrets, chat transcripts, full logs, copied acceptance criteria, or a transient list
of dirty files. When repository state materially affects continuation, record only the stable
revision, bookmark, branch, or caution needed to resume safely.

## Retire completed handoffs

When a workstream completes, first capture any remaining durable information and update its
authoritative task state. Then remove or archive its handoff according to repository policy and
synchronize any handoff index or resume-command registry. Do not leave an active handoff for work
that has nothing left to resume.

## Synchronize and verify

Add or update one grep-friendly line in `docs/handoffs/INDEX.md` with the file link, recorded state,
purpose, and the command that uses it. Verify that linked durable references resolve and that the
handoff contains no sensitive or duplicated canonical material.

For an explicit handoff request, finish by returning `$resume <slug>` without block-quote
formatting. Under context pressure, phrase it conditionally, such as: "If you decide to continue in
a fresh session: `$resume <slug>`." For automatic maintenance, do not print the command.

Do not commit, push, or alter unrelated task state unless separately requested.
