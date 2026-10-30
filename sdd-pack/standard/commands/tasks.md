---
description: Legacy command wrapper for the Standard SDD Tasks stage.
---

# Tasks

This command file is retained for compatibility/reference. The canonical workflow lives in `standard/SKILL.md` and `standard/tasks/SKILL.md`.

## User Input

```text
$ARGUMENTS
```

Read:

```text
specs/active/<id-slug>/requirement.md
specs/active/<id-slug>/plan.md
```

Create or update:

```text
specs/active/<id-slug>/tasks.md
```

Update `specs/index.md` after task generation.

Use `standard/tasks/templates/tasks-template.md` or `standard/tasks/templates/tasks-template.zh-CN.md`.

Tasks must be organized by user story and phase. Standard task blocks must include:

- task header with ID
- `Files`
- `Interfaces`
- TDD micro-steps
- Review Gate at phase end

Avoid vague placeholders, undefined interfaces, missing file paths, and "implement later" tasks.
