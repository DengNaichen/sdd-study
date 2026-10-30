---
name: standard-sdd-tasks
description: 当 requirement.md 和 plan.md 已存在，需要生成 Standard SDD tasks.md，并包含用户故事阶段、Files、Interfaces、TDD 微步骤、依赖和 Review Gate 时使用。
---

# Standard SDD Tasks

目标：基于 `requirement.md` 和 `plan.md` 创建 `<workflow_directory>/tasks.md`。

在 `plan.md` 存在且 File Structure Mapping 完成后使用。

## 输入

- `<workflow_directory>/requirement.md`
- `<workflow_directory>/plan.md`
- 可选 `research.md`
- 可选 `contracts/`
- plan 中引用的已有 ADR

## 流程

1. 使用 `../workflow/SKILL.zh-CN.md` 规则解析 active workflow。
2. 读取 `specs/index.md`、`<workflow_directory>/requirement.md` 和 `<workflow_directory>/plan.md`。
3. 中文 artifact 使用 `templates/tasks-template.zh-CN.md`；英文 artifact 使用 `templates/tasks-template.md`。
4. 从 `requirement.md` 提取用户故事和优先级。
5. 从 `plan.md` 提取技术上下文和 File Structure Mapping。
6. 将 contracts 和决策映射到受影响的用户故事。
7. 生成阶段：
   - Phase 1: Setup
   - Phase 2: Foundational
   - Phase 3+: 每个用户故事一个 Phase，按优先级排序
   - Final Phase: Polish & Cross-Cutting Concerns
8. 每个标准任务必须包含：
   - H3 任务标题和连续 ID
   - 只有可并行时才标记 `[P]`
   - 用户故事任务标记 `[US#]`
   - Files block
   - Interfaces block
   - TDD 微步骤
9. 每个 Phase 必须以 Review Gate 结束。
10. 更新 `specs/index.md` 中对应 workflow 行，阶段设为 `tasks` 并刷新更新时间。

## 禁止模式

- TBD / TODO / fill in later
- 模糊的“添加校验”或“处理错误”
- 缺少文件路径
- 缺少具体测试或验证步骤
- Interfaces 引用了未定义的类型或函数

## 输出

- `<workflow_directory>/tasks.md`
- 更新后的 `specs/index.md`
- 任务总数、故事拆解、并行机会和 MVP 范围摘要
