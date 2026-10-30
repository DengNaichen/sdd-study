---
description: Standard SDD Plan 阶段的兼容/参考 command 包装。
---

# Plan

此文件仅作为兼容和参考保留。规范流程以 `standard/SKILL.md` 和 `standard/plan/SKILL.zh-CN.md` 为准。

## 用户输入

```text
$ARGUMENTS
```

读取：

```text
specs/active/<id-slug>/requirement.md
```

生成或更新：

```text
specs/active/<id-slug>/plan.md
```

Plan 完成后同步更新 `specs/index.md`。

使用 `standard/plan/templates/plan-template.zh-CN.md`；英文 artifact 使用 `standard/plan/templates/plan-template.md`。

只有在有充分理由时才生成可选工件：

- `research.md`：未解决决策、技术选型、外部约束或风险验证
- `contracts/`：外部 API、事件、CLI、library 或 UI contract

Plan 完成后，只有当 plan/research 包含长期需要解释的关键决策时，才推荐 ADR。不要自动创建 ADR。
