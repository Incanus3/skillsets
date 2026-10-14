# Document visualization: rationale and evidence

Accepted approach as of 2026-10-14. This record explains the choices and their evidence; maintained instructions live
in the [document visualization skill](../../personal/skills/document-visualization/SKILL.md),
[design visualization adapter](../../personal/skills/design-visualization/SKILL.md), and
[design specification writing policy](/home/jakub/.agents/policies/design-spec-writing.md).

## Keep presentation familiar while adapting the explanation

The operator preferred the original Caddy experiment's revised C presentation: dark styling, a persistent sidebar,
and clear component borders/backgrounds, combined with B's direct technical language. Explicit disk/runtime state
comparisons added useful explanation; long decorated prose and slogan-like headings did not. Shared CSS and a shell
preserve that visual vocabulary while allowing different central representations and section structures.

The accepted presentation does not require Caddy's outline, branch count, or state sequence. The operator later
requested smaller page titles and distinct inline-code styling, both retained in the shared assets. Routine mobile
adaptation was rejected as unnecessary generation overhead; existing responsive CSS remains available when requested.
These choices reflect operator preference, not measured improvement in review speed.

## Use a diagram specialist within the document companion

On 2026-10-06 the operator selected diagram-design as the default specialist after three different-source comparisons
and a repeat of the cooperative-updates case. Operator preference favored diagram-design for Caddy and cooperative
updates, but slightly favored html-diagram for repository bindings. The final repeat favored diagram-design's proper
participant sequence and consistency. A dated maintenance audit supplied additional supporting evidence.

Keep the specialist unmodified and retain the companion's presentation and source-fidelity rules. This avoids upstream
patch maintenance and conflicting style/onboarding defaults. Html-diagram remains a credible alternative; the trials
showed meaningful author variation and no universal winner. The repeat outputs were longer and not uniformly better.
Old pending-adoption statements in the experiment records are superseded by the final operator selection.

## Separate generic documents from design review

On 2026-10-14 the operator reported that the skill worked well but mixed generic visualization with design-specific
review concerns. The shared workflow and assets moved to document-visualization. Design-visualization remains a small
adapter for behavioral contracts, decision inventories and approval boundaries, preserving its established invocation
and policy routing. Keeping the adapter avoids duplicating presentation rules or turning the writing policy into a
rendering procedure. Non-design documents can now retain their own terminology and organization.

The split landed in the skillsets repository at `702b6bf42de755d14bbc260c91499578f834581f`. Both skill validators,
relative resource links and skillset discovery checks passed. A bounded fictional lending-report shell check was
visually inspected in Chromium at 1440×1080: source anchors resolved, qualifications remained visible, and there was
no page overflow or design approval inventory. This checked the moved shell, not independent agent behavior.

## Verification scope and evidence owners

Detailed local experiment artifacts remain at `/home/jakub/.local/share/caddy-design-views/2026-10-03/`:

- [Original comparison and operator feedback](/home/jakub/.local/share/caddy-design-views/2026-10-03/comparison.md),
  [revised C verification](/home/jakub/.local/share/caddy-design-views/2026-10-03/variant-c-revised/changes.md).
- [Delivery and rotation forward trials](/home/jakub/.local/share/caddy-design-views/2026-10-03/skill-tests/verification.md).
- [Specialist source audit](/home/jakub/.local/share/caddy-design-views/2026-10-03/existing-skills-comparison.md),
  [Caddy comparison](/home/jakub/.local/share/caddy-design-views/2026-10-03/skill-comparison-2026-10-06/assessment.md),
  [repository bindings](/home/jakub/.local/share/caddy-design-views/2026-10-03/repository-bindings-comparison-2026-10-06/assessment.md),
  [cooperative updates](/home/jakub/.local/share/caddy-design-views/2026-10-03/live-updates-comparison-2026-10-06/assessment.md),
  [final repeat and accepted specialist](/home/jakub/.local/share/caddy-design-views/2026-10-03/live-updates-repeat-2026-10-06/assessment.md).
- [Dated maintenance audit](/home/jakub/.local/share/caddy-design-views/2026-10-03/maintenance-comparison-2026-10-06.md).

The comparison artifacts retain their own source snapshots and pinned upstream revisions; they are not current
product specifications. The preview server was stopped and is not a continuing service. These qualitative trials
checked source fidelity, links and rendered layouts, not live host/product behavior, statistical reliability, human
review speed, exhaustive accessibility, or every browser. Later desktop-only and optional-highlighting decisions
supersede the earlier trial requirements for mobile checks and entirely script-free output.

Development checks recorded on 2026-10-07 covered the optional highlighting loader with live CDN, blocked CDN and
JavaScript disabled: code text/layout survived, only explicitly supported languages were highlighted, and inline and
unknown-language code remained unchanged. These historical outcomes were not reproduced during the split. The
operator explicitly limited ordinary generation to rendering inspection; repeat integration checks only when changing
the loader or fallback. Current loader behavior and verification instructions are owned by document-visualization.
