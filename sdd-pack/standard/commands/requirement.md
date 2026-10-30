---
description: Legacy command wrapper for the Standard SDD Requirement stage.
---

# Requirement

This command file is retained for compatibility/reference. The canonical workflow lives in `standard/SKILL.md` and `standard/requirement/SKILL.md`.

## User Input

```text
$ARGUMENTS
```

Create or update:

```text
specs/active/<id-slug>/requirement.md
```

Update `specs/index.md` when creating or updating the workflow.

Use `standard/requirement/templates/requirement-template.md` or `standard/requirement/templates/requirement-template.zh-CN.md`.

Requirement records durable product/system behavior:

- Purpose & Scope
- User Stories & Priorities
- Functional Requirements
- Business Rules & Constraints
- Non-Functional Requirements
- Data & Interfaces
- Acceptance Criteria
- Assumptions & Open Questions
- Traceability & Change Log

Do not include implementation plan, task breakdown, branch status, or conversation history.
