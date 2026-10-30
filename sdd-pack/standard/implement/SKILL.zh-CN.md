---
name: standard-sdd-implement
description: 当需要执行 Standard SDD tasks.md、继续实现、选择未完成任务、应用 TDD、进行 task review、运行 Review Gate，并在实现后记录已接受 debt 时使用。
---

# Standard SDD Implement

目标：使用 Spec Kit 风格 artifacts 和 Superpowers 风格执行纪律来执行 `tasks.md`。

## 输入

- `<workflow_directory>/requirement.md`
- `<workflow_directory>/plan.md`
- `<workflow_directory>/tasks.md`
- 相关 ADR
- 相关已接受 debt

## 执行纪律

- 编辑前审查选中的任务范围。
- 严格遵循任务步骤。
- 行为变更使用 TDD：
  - 写失败测试
  - 验证失败原因符合预期
  - 实现最小代码
  - 验证通过
  - 只有 green 后才重构
- 如果验证意外失败，先找根因再修复。
- 不基于假设标记任务完成。
- 没有新鲜验证证据，不声明完成。

## 流程

1. 使用 `../workflow/SKILL.zh-CN.md` 规则解析 active workflow。
2. 读取 `specs/index.md`、`<workflow_directory>/requirement.md`、`<workflow_directory>/plan.md` 和 `<workflow_directory>/tasks.md`。
3. 选择范围：
   - 用户请求为空：执行下一个未勾选任务
   - `all`：按依赖顺序执行全部未勾选任务
   - phase/story/task ID：仅执行选中范围
4. 审查选中任务是否有阻塞：
   - 与 requirement/plan/ADR 冲突
   - 缺少 Files/Interfaces/TDD 步骤
   - 缺少依赖
5. 执行每个任务。
6. 勾选任务前运行 task review：
   - 变更文件匹配 Files block
   - 产出接口匹配 Interfaces block
   - 相关验收条件被覆盖
   - 验证输出是新鲜的
7. 完成一个 Phase 后运行 Review Gate。
8. 根据剩余工作更新 `specs/index.md` 中对应 workflow 行，阶段设为 `implement` 或 `review`。
9. 选中范围完成后运行 debt capture check；如果存在已接受的非阻塞后续事项，使用 Debt skill。
10. 只有验收或 review 完成后，才把 workflow 移动到 `specs/complete/<id-slug>/`，并更新 `specs/index.md` 的状态、路径和阶段。

## 停止条件

遇到以下情况时停止并报告，不要猜：

- 任务描述不足
- 缺少依赖
- 验证反复失败
- plan 和 task 相互矛盾
- 修复需要重新设计功能

## 输出

- 更新后的代码
- 更新后的 `tasks.md` checkbox
- 更新后的 `specs/index.md`
- 验证结果
- Review Gate 状态
- 可选 `docs/debt/<workflow-id-slug>-debt.md`
