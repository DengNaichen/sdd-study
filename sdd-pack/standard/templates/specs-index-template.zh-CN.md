# Specs Index

此文件是 Standard SDD workflow registry。选择、创建或完成 workflow 前先读本文件。

## Workflows

| ID | 状态 | 功能 | 路径 | 阶段 | 创建时间 | 更新时间 | 备注 |
|---|---|---|---|---|---|---|---|
| 0000 | complete | 示例已完成 workflow | specs/complete/0000-example-done | complete | YYYY-MM-DD | YYYY-MM-DD | 示例行；有真实 workflow 后删除 |

## 状态

- active：正在进行。
- blocked：缺少输入或外部变化，暂时无法继续。
- complete：已通过验收或 review，并移动到 `specs/complete/`。

## 阶段

- requirement
- plan
- adr-check
- tasks
- implement
- review
- complete

## 维护规则

- 每个 workflow 目录一行。
- 从 `specs/active/` 移动到 `specs/complete/` 时，同步更新 `路径`。
- workflow 前进时更新 `阶段`。
- 任何 workflow artifact 变化时更新 `更新时间`。
- 不要把 requirement、plan、tasks 或 ADR 正文复制到本 index。
