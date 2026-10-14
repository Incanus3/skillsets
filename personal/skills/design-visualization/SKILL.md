---
name: design-visualization
description: Create or update an HTML review companion for a design specification, preserving design decisions, behavioral contracts and approval boundaries. Use document-visualization directly for non-design documents. Not for product UI or presentations.
---

# Design visualization

Read and apply [document-visualization](../document-visualization/SKILL.md) for representation selection, shared
presentation assets, diagram integration, source links and rendering verification. It owns the generic workflow;
this skill adds the design review context below. Reuse its assets rather than maintaining a separate presentation.

Read the complete current specification and apply the design-specification writing policy when available
(in this setup, `~/.agents/policies/design-spec-writing.md`). Keep the Markdown specification authoritative and
self-contained. An HTML companion is useful when reviewer questions about relationships, flows, states, recovery
or trade-offs benefit from a coordinated layout beyond the specification and its existing diagrams.

- Choose sections for the actual design. Where useful, retain the familiar order: scope/ownership, behavior,
  failure/recovery, trade-offs, evidence. Omit or rearrange topics as needed; do not create empty sections.
- Preserve decision IDs and statuses. For decision inventories, follow the policy's separate ID then Status columns,
  status-group ordering and natural ID ordering within each group. Inherited constraints retain their provenance;
  do not imply acceptance of proposals or implementation evidence.
- Preserve exact conditions, ordering, authority boundaries, failure paths and recovery limits. Keep contracts
  accessible in the source rather than requiring readers to infer API or error semantics from a diagram.
- Keep concrete costs, unresolved choices and uncertainty visible without interaction. Distinguish decision approval
  from operational outcome and technical readiness from authorization.
- If a companion reveals a substantive source problem, apply the specification's normal revision and approval rules
  before synchronizing the companion, snapshots and provenance. Never introduce behavior or approval statuses through
  the companion alone. Verify summaries especially against failures, recovery and proposed versus accepted decisions.
