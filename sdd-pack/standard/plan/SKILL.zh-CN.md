---
name: standard-sdd-plan
description: 当 requirement.md 已存在，需要为 Standard SDD 创建或更新 plan.md、技术上下文、文件结构映射、测试策略、可选 research.md、可选 contracts 和 ADR 建议时使用。
---

# Standard SDD Plan

目标：创建或更新 `<workflow_directory>/plan.md`，并在必要时生成 `research.md` 和 `contracts/`。

在 `requirement.md` 已存在后使用。

## 输入

- `<workflow_directory>/requirement.md`
- 当前项目结构和约定
- 相关架构文档、ADR、contracts 或源代码文件

## 流程

1. 使用 `../workflow/SKILL.zh-CN.md` 规则解析 active workflow。
2. 读取 `specs/index.md` 和 `<workflow_directory>/requirement.md`。
3. 中文 artifact 使用 `templates/plan-template.zh-CN.md`；英文 artifact 使用 `templates/plan-template.md`。
4. 基于真实项目填写 Technical Context。
5. 填写 Test Strategy：
   - 测试框架
   - test-first 范围
   - contract / integration / unit / manual verification
   - tasks 中是否需要 Red/Green 证据
6. 在生成 tasks 前填写 File Structure Mapping。
7. 只有存在真实不确定性时，才生成 `research.md`：
   - 未解决决策
   - 技术选型
   - 外部约束
   - 契约探索
   - 有意义的风险验证
8. 只有存在外部接口时，才生成 `contracts/`：
   - public API
   - event
   - CLI
   - library contract
   - UI contract
9. 默认不生成 `data-model.md`；如有需要，链接项目已有的数据模型文档。
10. 更新 `specs/index.md` 中对应 workflow 行，阶段设为 `plan` 并刷新更新时间。

## ADR 推荐检查

Plan 完成后，只有当 plan/research 包含长期需要解释的关键决策时，才推荐 ADR：

- 架构或模块边界变化
- public interface、contract、event 或 CLI 选择
- 数据模型、schema、部署、运行时或运维策略决策
- 否决了另一个可信方案
- 会影响多个 feature 的取舍

不要自动创建 ADR。

## 输出

- `<workflow_directory>/plan.md`
- 可选 `<workflow_directory>/research.md`
- 可选 `<workflow_directory>/contracts/`
- 更新后的 `specs/index.md`
- 仅在必要时给出 ADR 建议
