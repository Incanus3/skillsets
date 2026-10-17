# Decision records

Keep collection documentation under `personal/docs/`, outside `personal/skills/`. The repository root is the configured
`skillset` collection directory: a non-hidden root directory is treated as a collection. Root-level `docs/` broke
`skillset list` and `skillset doctor` by being validated as a collection. After relocation on 2026-10-17, both commands
and `skillset show personal` succeeded; the documentation does not appear in skill discovery.

- [Document visualization](document-visualization.md) — accepted presentation, specialist selection, generic/design split, and bounded verification evidence.
