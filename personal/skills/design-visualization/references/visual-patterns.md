# Review presentation patterns

Use `assets/review.css` with local HTML. `assets/shell.html` is a substitution template; `assets/reference.html` is a complete fictional worked example. Copy the CSS beside generated HTML (or embed its contents), keeping the output usable offline. No fonts, scripts, libraries or remote resources are required.

## Choose components by the review question

| Question | Component | Required content |
| --- | --- | --- |
| Who owns or changes what? | `.panel-grid`, `.panel`, `.boundary-primary`, `.boundary-secondary`, `.boundary-note` | Named owner, resource and authority boundary; labels explain stripes. |
| What happens next, including failure? | `.flow`, `.flow-step`, `.flow-edge`, `.flow-branches`, `.state` | Ordered operation, condition on each edge, resulting state and recovery path. Name branch destinations; link them when distant. |
| Which approach meets the requirement? | `.comparison` inside `.comparison-wrap` | Shared criteria, benefits, costs and alternatives; no invented preference. |
| What does an outcome establish? | `.outcome-ready`, `.outcome-pending`, `.outcome-failed`, `.outcome-unknown` | Explicit outcome text, supporting evidence and what remains unresolved. |
| What is decided? | `.status` plus `.status-accepted`, `.status-proposed`, `.status-rejected`, `.status-unresolved`, `.status-superseded` | Textual decision status drawn from the source. |
| Where is an assumption or boundary? | `.callout`, `.callout-warning`, `.source-note` | Specific constraint and source link; do not manufacture warnings. |

These are available patterns, not required sections. Use a small diagram or comparison alone when it answers the question. For multiple substantive sections, retain the familiar `.review-wrap`, `.review-mast`, `.review-layout`, `.review-nav`, `main` and `.review-footer` shell. Use direct technical headings naming the operation, condition or comparison.

## Usage contract

- Replace every shell slot before sharing. Plain text must be HTML-escaped; inserted markup must be constructed deliberately. Navigation links must resolve to unique section IDs. Source links must point to actual source locations or a clearly labeled embedded example contract.
- Preserve the dark palette, system typography, generous spacing and bordered component boundaries. Use selective stripes only where the boundary has meaning. Do not add unrelated decoration or force source content into the reference example's outline.
- Decision status and operation outcome are different dimensions. Use `status-*` for approval/decision state and `outcome-*` for observed or described execution state. An accepted decision is not a successful operation. Use text labels alongside color, including in flows and comparisons. Inherited describes provenance, not approval: show it with `.provenance-label` alongside an established decision status only when the source supports that status. Label an assumption as an assumption.
- Flow cards alone do not communicate a flow. Add labeled transitions with conditions and failure paths. State what a failed or lost operation proves, what remains unknown and whether recovery changes only prepared state or active state.
- State source revision/provenance and distinguish assumptions, proposals and verified evidence. The presentation does not itself authorize implementation or external action.
- Mark literal paths, commands, identifiers, configuration keys and raw values with `<code>`. Inline literals use a neutral bordered background and monospace text; use `.code-block` for standalone snippets, or semantic `pre`/`code` for preformatted blocks. Preserve exact text and allow long inline strings to wrap. Do not apply code styling to ordinary prose or use status colors for literals.
- Keep semantic headings, real anchors, table headers/captions and meaningful navigation labels. CSS provides visible keyboard focus, reduced-motion support and print styling.
- At widths below 1100px state columns fold beneath steps. Below 760px panels stack and sticky navigation becomes an inline link group; source/authority notes remain visible. Inspect a desktop and narrow viewport after adapting content. Check readability, overflow, transition labels, source links and decision/outcome labels. A dense table may scroll inside its wrapper, never the whole page.

## Optional comparison layouts on narrow screens

Choose a mode per table; do not apply either modifier globally or combine them. Use dense scrolling when readers need to compare columns across rows. Use stacked labeled rows when each row is a self-contained state or alternative and narrow columns would fragment its explanation. The base `.comparison` remains suitable for short, sparse tables.

For dense scrolling, keep the hint outside the scrolling region so it stays visible. The table has a 620px minimum width; override `--comparison-min-width` only when its content needs more room. Provide a descriptive region label and keyboard focus, and connect the hint with `aria-describedby`.

```html
<p id="exchange-hint" class="comparison-scroll-hint source-note">Scroll horizontally to read every exchange column.</p>
<div class="comparison-wrap comparison-scroll" tabindex="0" role="region"
     aria-label="Participant exchange comparison" aria-describedby="exchange-hint">
  <table class="comparison">
    <!-- Retain the caption, semantic column headers and complete body rows. -->
  </table>
</div>
```

For labeled mobile rows, add `.comparison-stack` to the table and `data-label` to every body `td`, with text matching its column header. Keep the actual headers and caption: at widths up to 760px the header is visually hidden, each row becomes a bordered block, and labels precede each cell. A body `th scope="row"` can name the row and does not need `data-label`. At desktop widths the original table remains unchanged.

```html
<div class="comparison-wrap">
  <table class="comparison comparison-stack">
    <caption>Illustrative publication states</caption>
    <thead><tr><th scope="col">State</th><th scope="col">Active revision</th><th scope="col">Next condition</th></tr></thead>
    <tbody><tr><th scope="row">Prepared</th><td data-label="Active revision">Previous revision</td><td data-label="Next condition">Validation passes → switch conditionally.</td></tr></tbody>
  </table>
</div>
```

Inspect the actual chosen mode at a narrow viewport. Confirm the scroll hint is visible, the scroll region is keyboard accessible, and stacked labels match the headers without hiding decision or outcome text. Preserve the desktop comparison and source links.
