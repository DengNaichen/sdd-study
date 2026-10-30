---
description: Standard SDD Requirement 阶段的兼容/参考 command 包装。
---

# Requirement

此文件仅作为兼容和参考保留。规范流程以 `standard/SKILL.md` 和 `standard/requirement/SKILL.zh-CN.md` 为准。

## 用户输入

```text
$ARGUMENTS
```

生成或更新：

```text
specs/active/<id-slug>/requirement.md
```

创建或更新 workflow 时同步更新 `specs/index.md`。

使用 `standard/requirement/templates/requirement-template.zh-CN.md`；英文 artifact 使用 `standard/requirement/templates/requirement-template.md`。

Requirement 记录长期需求事实：

- Purpose & Scope
- User Stories & Priorities
- Functional Requirements
- Business Rules & Constraints
- Non-Functional Requirements
- Data & Interfaces
- Acceptance Criteria
- Assumptions & Open Questions
- Traceability & Change Log

不要写实现计划、任务拆解、分支状态或对话历史。
