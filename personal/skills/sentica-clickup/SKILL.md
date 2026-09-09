---
name: sentica-clickup
description: Use when reading, prioritizing, reporting on, or managing Sentica ClickUp tasks.
---

# Sentica ClickUp

Use these conventions when interpreting Sentica ClickUp task state.

## B2 space

- Treat `in verification` as done from Jakub's point of view. Implementation ownership has passed to QA, which owns the transition from `in verification` to `done`.
- Exclude `in verification` tasks from Jakub's active focus list by default.
- Include such a task only when Jakub explicitly asks about verification work, when QA has returned it for changes, or when the task contains evidence that Jakub is currently blocking verification.
- Do not generalize this status meaning to other ClickUp spaces unless their workflow is documented separately.

## Checklist management

Use the authenticated local `clickup-cli` for checklist operations when the ClickUp connector lacks the required
action. Confirm task and assignee IDs from read-only ClickUp data and inspect the relevant CLI help:

```bash
clickup-cli checklist create --task <task-id> --name '<checklist-name>' --output json
clickup-cli checklist add-item <checklist-id> --name '<item-name>' --assignee <user-id> --output json
```

Read the task back with `clickup-cli task get <task-id> --output json` and verify the checklist name, item text,
completion state, and assignee. Never expose an API token.
