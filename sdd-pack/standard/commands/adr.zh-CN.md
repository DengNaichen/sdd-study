---
description: Standard SDD ADR 阶段的兼容/参考 command 包装。
---

# ADR

此文件仅作为兼容和参考保留。规范流程以 `standard/SKILL.md` 和 `standard/adr/SKILL.zh-CN.md` 为准。

## 用户输入

```text
$ARGUMENTS
```

只有长期决策才创建 ADR：

- 架构或模块边界变化
- public interface、contract、event 或 CLI 选择
- 数据模型、schema、部署、运行时或运维策略决策
- 否决了另一个可信方案
- 会影响多个 feature 的取舍

不要把每一条 research note 都转成 ADR。

输出：

```text
docs/adr/index.md
docs/adr/ADR-XXXX-kebab-title.md
```

使用 `standard/adr/templates/adr-template.zh-CN.md`；英文 artifact 使用 `standard/adr/templates/adr-template.md`。

创建、接受、拒绝或替代 ADR 时，必须同步维护 `docs/adr/index.md`。如果 index 不存在，使用 `standard/adr/templates/adr-index-template.zh-CN.md` 创建。
