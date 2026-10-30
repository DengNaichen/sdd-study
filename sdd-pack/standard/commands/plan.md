---
description: Legacy command wrapper for the Standard SDD Plan stage.
---

# Plan

This command file is retained for compatibility/reference. The canonical workflow lives in `standard/SKILL.md` and `standard/plan/SKILL.md`.

## User Input

```text
$ARGUMENTS
```

Read:

```text
specs/active/<id-slug>/requirement.md
```

Create or update:

```text
specs/active/<id-slug>/plan.md
```

Update `specs/index.md` after planning.

Use `standard/plan/templates/plan-template.md` or `standard/plan/templates/plan-template.zh-CN.md`.

Generate optional artifacts only when justified:

- `research.md`: unresolved decisions, technology choices, external constraints, or risk validation
- `contracts/`: external API, event, CLI, library, or UI contracts

After planning, recommend ADR only when the plan/research contains a durable decision with long-term explanatory value. Do not create ADR automatically.
