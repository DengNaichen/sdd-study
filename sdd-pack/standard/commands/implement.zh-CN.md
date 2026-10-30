---
description: Standard SDD Implement 阶段的兼容/参考 command 包装。
---

# Implement

此文件仅作为兼容和参考保留。规范流程以 `standard/SKILL.md` 和 `standard/implement/SKILL.zh-CN.md` 为准。

## 用户输入

```text
$ARGUMENTS
```

执行选中的未完成任务：

```text
specs/active/<id-slug>/tasks.md
```

实现过程中同步更新 `specs/index.md`。只有验收或 review 完成后，才移动到 `specs/complete/<id-slug>/`。

使用：

- `requirement.md` 确认预期行为和验收标准
- `plan.md` 确认设计约束和验证策略
- 相关 ADR 确认长期设计约束

执行纪律：

- 编辑前审查选中范围
- 严格遵循任务步骤
- 行为变更使用 TDD
- 意外失败先找根因
- 标记完成前运行 task review
- Phase 完成后运行 Review Gate
- 声明完成前必须有验证证据
- 实现后捕获已接受的非阻塞 debt
