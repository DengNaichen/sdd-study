# Debt 阶段

目标：在实现完成后记录已接受的非阻塞后续事项。

Debt 不是隐藏必修问题的地方。

## 什么时候记录 Debt

- 某个非阻塞问题被明确接受。
- 有 workaround 被有意交付。
- 测试、监控、迁移、文档或清理工作被延后。
- ADR/plan 风险产生了后续工作。
- Review Gate 通过，但存在已接受的残留事项。

## 不要把这些记为 Debt

- 失败测试
- 未满足的验收标准
- 不清楚的需求
- 选中任务必须完成的修复
- 完成前必须修复的 bug

## 流程

1. 使用 `templates/debt-template.zh-CN.md`。
2. 创建或更新 `docs/debt/<workflow-id-slug>-debt.md`。
3. 链接相关 requirement、plan、task ID、ADR 和验证缺口。
4. 写清关闭标准。

## 输出

- `docs/debt/<workflow-id-slug>-debt.md`
