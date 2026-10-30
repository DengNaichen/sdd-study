---
name: standard-sdd-workflow
description: 当需要管理 Standard SDD workflow registry 和功能目录时使用：创建带编号的 specs/active workflow、选择 active workflow、更新 specs/index.md 阶段/状态元数据，或把完成的 workflow 移动到 specs/complete。
---

# Standard SDD Workflow

目标：管理带编号的 workflow 目录和 `specs/index.md`，避免为了选择任务而加载全部 feature artifact。

## 布局

使用这个结构：

```text
specs/
├── index.md
├── active/
│   └── 0001-feature-slug/
│       ├── requirement.md
│       ├── plan.md
│       ├── research.md      # 可选
│       ├── contracts/       # 可选
│       └── tasks.md
└── complete/
    └── 0000-example-done/
```

## Registry

`specs/index.md` 是 workflow registry。选择、创建或完成 workflow 前先读它。

如果 `specs/index.md` 不存在，使用 `templates/specs-index-template.zh-CN.md` 或 `templates/specs-index-template.md` 创建。

Registry 必须记录：

- ID
- 状态
- 功能
- 路径
- 当前阶段
- 创建日期
- 更新日期
- 备注

## 目录规则

- 使用 `NNNN-kebab-slug`，例如 `0007-billing-webhook`。
- 下一个 ID 从 `specs/index.md`、`specs/active/`、`specs/complete/` 中已有最大 ID 加一。
- 新 workflow 从 `specs/active/<id-slug>/` 开始。
- 完成后的 workflow 移动到 `specs/complete/<id-slug>/`。
- 不复用 ID。
- artifact 已存在后不要静默重命名 workflow 目录；用户明确要求重命名时，同步更新 `specs/index.md`。

## 选择规则

当某个阶段需要 feature directory 时：

1. 如果用户指定 ID、slug 或路径，使用该 workflow。
2. 否则读取 `specs/index.md`，按当前上下文匹配。
3. 否则如果只有一个 active workflow，使用它。
4. 否则如果没有 active workflow 且用户正在开始新功能，创建新的 active workflow。
5. 否则请用户选择；不要在多个 active workflow 中猜。

## 阶段规则

- 创建 Requirement 时默认创建新的 active workflow，除非用户明确是在更新已有 workflow。
- Plan、Tasks、Implement 默认要求 active workflow，除非用户明确要审查或更新 complete workflow。
- 实现完成不自动移动到 `complete`；只有验收或 review 完成后才移动。
- 移动到 `complete` 时，同步更新 `specs/index.md` 中的状态、路径、阶段和更新时间。

## 输出

- 选中或创建的 workflow 路径
- 已更新的 registry 行
- 建议下一阶段
