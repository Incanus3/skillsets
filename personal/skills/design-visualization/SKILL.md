---
name: design-visualization
description: Use when creating or updating an HTML review companion for a design specification, or when a complex design needs a visual explanation of relationships, flows, states, recovery or trade-offs. Not for product UI, presentations, or a simple requirement already clear in Markdown.
---

# Design visualization

Create a source-linked review companion with familiar presentation and a representation fitted to the design.
Keep the Markdown specification authoritative. Apply the design-specification writing policy when available.

## Choose the explanation

Read the complete current specification. Identify the questions the reviewer needs to answer and the relationships
that are difficult to inspect in Markdown or existing diagrams. Choose the simplest view that exposes those
relationships. Make this choice autonomously; ask only for missing design intent or requirements.

| Reviewer question | Suitable representation |
|---|---|
| Who owns or may change what? | Boundary panels or labeled relationship graph |
| Which condition selects which outcome? | Branching flow or scenario comparison |
| Who communicates with whom, and in which order? | Participant sequence or swimlanes |
| How do states change, including failure and recovery? | State graph or transition rows with explicit before/after state |
| How do alternatives differ? | Comparison table on shared dimensions |

Select and combine patterns as needed. Include conditions, direction, failure paths and recovery limits where they
change the meaning. If a small design is already clear, explain that briefly instead of generating a redundant page.
An explicit request for HTML still receives a proportionate companion.

## Use the diagram specialist

When a diagram helps, read and apply the installed `diagram-design` skill for type selection, layout, connectors and
accessible SVG. In this setup it lives at `~/.agents/skillsets/always-on/skills/diagram-design/SKILL.md`.
Load only the relevant type and semantic-pattern references. Draw the relationships, participants or state transitions
explicitly; a stack of prose rows with arrows is not a substitute when those relationships are the review question.
Keep ordinary comparisons and exact contracts in tables where they work better.

This skill owns the companion's presentation and review contract. Our assets are the already-selected style guide:
use their dark palette, system fonts, local CSS, static default and desktop verification rather than upstream branding,
font, single-file or viewport defaults. Choose type and size autonomously; do not repeat onboarding, profile-save or
type-confirmation prompts when the design supplies enough context. Leave the managed upstream skill unmodified.

When updating an existing companion, retain its diagram type, participant positions and visual conventions while they
still explain the design clearly. Change them when the design or review question warrants it, rather than for variety.

## Reuse the presentation

Use [assets/shell.html](assets/shell.html) and [assets/review.css](assets/review.css) as the presentation foundation.
Copy the CSS alongside the generated HTML; use relative local assets so output also works offline. Keep the dark
palette, type scale, spacing, navigation placement, component boundaries and semantic cues familiar. Adapt or extend
the components for the explanation without redesigning the page's visual vocabulary.

Read [visual-patterns.md](references/visual-patterns.md) for component usage and selection. Inspect
[reference.html](assets/reference.html) for a complete worked example of the shared presentation.

Desktop review is the default. Do not spend generation or verification effort on mobile layouts, responsive
adaptations or small-viewport checks unless the operator explicitly requests them. Existing responsive CSS may
remain in the shared assets; it does not create a requirement to adapt or test narrow layouts.

Use the sidebar on multi-section desktop views. Choose section titles
for actual content. Where applicable, keep recurring topics in a familiar order: scope/ownership, behavior,
failure/recovery, trade-offs, evidence. Merge, omit or rearrange topics when the design requires it; do not fill empty
sections or reproduce the example's section count, branch count or central diagram.

Headings name the operation, boundary, condition or comparison. Write direct technical copy with enough explanation
to understand it; avoid slogans, metaphors, persuasive claims and excessive shorthand. Use borders/backgrounds to
separate meaningful units, not a separate card for every sentence. Keep decision status distinct from operational
outcome; accompany every color cue with text. Costs, failure conditions and uncertainty remain visible without clicks.

Static views are the default. Add interaction only when it answers a concrete question better than concurrent static
views. Essential reasoning remains readable without the interaction. A visualization should expose relationships,
not duplicate the specification as a long decorated page.

## Highlight code blocks optionally

For fenced code, use `<pre class="code-block"><code class="language-json">…</code></pre>` with the actual language
and HTML-escaped source text. Keep inline literals unchanged. Retain the shell's pinned, asynchronous Highlight.js
CDN script when code blocks benefit from highlighting; omit it when there are no such blocks. The local CSS owns
layout and token colors. Highlight only explicitly labeled languages supported by the loaded bundle; unknown or
unlabeled blocks remain plain text, without auto-detection or extra grammar downloads.

Highlighting is an optional network enhancement, not a requirement for reading the artifact. Preserve code text and
layout when the CDN is unavailable or JavaScript is disabled. Do not add loading indicators or wait for highlighting
before rendering content. The bundled integration's online, blocked-CDN and JavaScript-disabled behavior has been
verified during skill development. During ordinary companion generation, inspect the page's rendering; do not repeat
offline, blocked-CDN or JavaScript-disabled tests, probe CDN availability, or install a local fallback. Repeat these
integration checks only when changing the highlighting loader or fallback behavior.

## Preserve authority and verify

- Show source title/link and revision or snapshot provenance. Link condensed claims to exact source sections. State
  the companion's scope; omitted exact contracts remain accessible in the source. For decision inventories, retain the policy’s separate ID then Status columns and status-group/ID ordering.
  Keep IDs, statuses, conditions,
  ordering, authority boundaries and uncertainty faithful. Do not imply design approval or implementation evidence.
- If Markdown source anchors do not work in the browser, provide a local HTML source snapshot with faithful text
  and section anchors, plus the unchanged Markdown. Identify its source revision or hash; keep private source local.
- Update the companion when its source changes; make a stale snapshot explicit rather than silently presenting it
  as current. Preserve useful section anchors across revisions. Keep generation instructions out of final output.
- Render and inspect the top and central/lower views at a representative desktop width. Check wrapping, overflow,
  navigation, status legibility and diagram labels. Check source anchors and compare summaries against the source,
  especially failures, recovery and proposed versus accepted decisions. Report material limitations.
- Deliver a standalone local artifact and preview when available. Use the host's relevant browser capability; this
  skill requires no particular browser tool. Creating a companion does not authorize publication or external actions.
