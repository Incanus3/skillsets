---
name: focus-on-goal
description: >-
  Keep extended work aligned with its intended outcome when supporting tasks
  expand, blockers recur, or a detailed plan obscures the main path. Bound
  supporting effort by its value, reassess simpler solutions, and maintain a
  concise roadmap when useful, without weakening durable code or required tests.
---

# Focus on the goal

Keep effort proportional to the outcome and risk. Supporting work can be valuable and worth retaining; its existence,
complexity or already-spent cost does not justify further investment. This skill guides choices, not permission to
change the user's goal, bypass safeguards or reduce necessary production quality.

## Keep the intended outcome visible

Recover the main goal, next observable milestone, definition of done and constraints from the user's request and
canonical project artifacts. Do not repeatedly ask for facts or decisions already established. Read an existing
roadmap before choosing/resuming work. Use project navigation, summaries and headings to identify relevant design,
prerequisites, decisions, cross-cutting constraints and downstream effects. Read required documents and follow references
that could materially affect the approach, correctness, safety or scope. For uncertain references, inspect enough to
assess that relevance; expand when a concrete dependency, constraint or unresolved question warrants it. The roadmap
does not replace required design or procedural reading. Neither uncertainty alone nor a link alone requires reading an
entire document tree; focus is also not a reason to skip context that could change the approach.

Connect the current task to that milestone. Distinguish progress in the delivered system from preparation, tooling,
tests, documents and approvals. Those may be necessary evidence or prerequisites, but counts of them are not proof
that the user-visible outcome advanced. Do not substitute an easier supporting deliverable for the requested result.

## Give supporting work a bounded job

Before starting or expanding a meaningful supporting work package, establish briefly:

- **Contribution:** which parent outcome it unlocks or material risk it reduces, and why that need exists now.
- **Sufficient result:** the smallest adequate proof or capability, with a clear definition of done and known limits.
- **Remaining cost:** rough effort and uncertainty, including integration, verification, review, maintenance and cleanup.
- **Alternatives and boundary:** simpler supported ways to meet the same need, plus an effort limit or concrete condition
  that triggers reassessment. Use existing constraints; do not invent precise estimates or arbitrary time caps.

Keep this lightweight: a few sentences or an existing task entry usually suffice. Do not create a specification,
framework, tracker or approval request for every helper. Prefer existing tools and small explicit procedures for
one-off needs. Build reusable infrastructure when expected future use or required reliability justifies its cost,
not merely because reuse is possible. Required tests for durable behavior are part of the deliverable, not expendable
supporting work.

## Reassess expansion instead of automatically following it

Revisit the approach when a supporting task acquires another prerequisite, exceeds its expected effort, repeatedly
fails in its own machinery, or closes several supporting checkpoints without advancing the main milestone.

First distinguish a real product/safety requirement from a limitation or assumption introduced by the chosen tool or
harness. A failed supporting check does not automatically justify another tool, another abstraction or a product
change. Compare the remaining cost and risk of continuing, narrowing the proof, using a supported alternative or
stopping/deferring that branch. Include the cost of delay to the main goal; do not count sunk effort as future value.

Keep useful completed evidence and procedures so they need not be recreated. Stop once the sufficient result is
achieved. Do not expand verification claims beyond what was demonstrated, or silently turn an experiment into a
production dependency. Explain material changes in route, cost, risk or scope to the user under existing authorization
rules; routine in-scope fixes do not need a new permission gate each time.

## Scale diligence by lifetime and consequences

| Work | Appropriate approach |
| --- | --- |
| One-off, low-impact support | Prefer the simplest reasonably safe and reliable solution, with focused checks and explicit failure behavior. Avoid building a general platform for one task. |
| One-off work with security, data or external-effect risk | Keep implementation narrow, but retain the necessary isolation, secret handling, recovery, authorization and verification. A short lifetime does not make harmful failure cheap. |
| Durable production code, tests or shared tooling | Invest in maintainable boundaries, meaningful regression coverage, error paths and relevant security, compatibility and performance checks. Future change and failure costs are part of its value. Avoid unnecessary generalization here too. |

Do not skip needed tests, weaken acceptance criteria, conceal uncertainty or leave durable code brittle merely to finish
faster. Nor does labeling code "durable" justify unlimited engineering. Use the least complex implementation that
meets its actual long-term requirements. If required assurance makes the route expensive, expose that trade-off;
do not silently remove the assurance. Experimental output needs its own readiness checks before production use.

## Use a short roadmap when the plan hides the goal

For work with enough phases or nested dependencies that the detailed plan is hard to keep in focus, reuse or create
one high-level roadmap in the project's established documentation location. A small task may need only a brief
orientation; do not manufacture a roadmap for it.

Show the main steps and relevant substeps, their state, short outcome-based descriptions, the current position and
next decision. Tie the active supporting branch to its parent and make new depth/cost visible. Keep completed
supporting work summarized rather than expanding its history. Preserve agreed remaining steps and authorization gates.

Default to roughly 100–150 lines and under 200, unless the project establishes another suitable bound. Keep detailed
procedures, commands, logs, evidence and technical contracts in their existing owners and link to them. A roadmap is
a current overview, not an append-only handoff or a second implementation plan. Do not create extra artifacts just to
move clutter elsewhere.

Update it in place at meaningful checkpoints and when the route or scope changes. Replace stale text, roll short recent
changes forward and compress completed branches. Record whether the main outcome advanced or only a prerequisite
closed. Delegated tasks should carry their parent milestone, expected contribution and relevant effort boundary.

Keep user updates similarly focused: what changed toward the goal, what remains blocked, whether supporting work grew,
and what the next action will achieve. Avoid fake completion percentages, invented delivery dates and progress claims
based solely on activity. Keep this focus practice cheaper than the drift it prevents.
