---
description: Legacy command wrapper for the Standard SDD ADR stage.
---

# ADR

This command file is retained for compatibility/reference. The canonical workflow lives in `standard/SKILL.md` and `standard/adr/SKILL.md`.

## User Input

```text
$ARGUMENTS
```

Create ADR only for durable decisions:

- architecture or module boundary changes
- public interface, contract, event, or CLI choices
- data model, schema, deployment, runtime, or operational policy decisions
- rejection of another credible option
- tradeoffs likely to affect multiple features

Do not convert every research note into an ADR.

Output:

```text
docs/adr/index.md
docs/adr/ADR-XXXX-kebab-title.md
```

Use `standard/adr/templates/adr-template.md` or `standard/adr/templates/adr-template.zh-CN.md`.

Maintain `docs/adr/index.md` whenever an ADR is created, accepted, rejected, or superseded. If the index does not exist, create it from `standard/adr/templates/adr-index-template.md`.
