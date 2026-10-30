---
description: Standard SDD Tasks 阶段的兼容/参考 command 包装。
---

# Tasks

此文件仅作为兼容和参考保留。规范流程以 `standard/SKILL.md` 和 `standard/tasks/SKILL.zh-CN.md` 为准。

## 用户输入

```text
$ARGUMENTS
```

读取：

```text
specs/active/<id-slug>/requirement.md
specs/active/<id-slug>/plan.md
```

生成或更新：

```text
specs/active/<id-slug>/tasks.md
```

生成 tasks 后同步更新 `specs/index.md`。

使用 `standard/tasks/templates/tasks-template.zh-CN.md`；英文 artifact 使用 `standard/tasks/templates/tasks-template.md`。

任务必须按 User Story 和 Phase 组织。标准任务块必须包含：

- 任务标题和 ID
- `Files`
- `Interfaces`
- TDD 微步骤
- 每个 Phase 末尾的 Review Gate

避免模糊占位、未定义接口、缺少文件路径和“之后再实现”。
