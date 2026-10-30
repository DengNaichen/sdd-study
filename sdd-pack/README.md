# Standard SDD Pure Skill

这个仓库保留 SDD 相关材料；当前主要集成目标是 **Standard SDD pure skill**。

核心链路：

```text
workflow -> requirement.md -> plan.md / research.md -> ADR? -> tasks.md -> implementation -> debt?
```

## 目录结构

```text
sdd-pack/
├── README.md
├── sdd-flow.zh-CN.md
├── sdd-flow-presentation.html   # 可选展示材料，不属于 skill 运行时
├── lean/                         # 保留的轻量流程参考材料
└── standard/
    ├── SKILL.md                  # router skill
    ├── SKILL.zh-CN.md
    ├── workflow/
    │   ├── SKILL.md
    │   ├── SKILL.zh-CN.md
    │   └── templates/
    ├── requirement/
    │   ├── SKILL.md
    │   ├── SKILL.zh-CN.md
    │   └── templates/
    ├── plan/
    │   ├── SKILL.md
    │   ├── SKILL.zh-CN.md
    │   └── templates/
    ├── adr/
    │   ├── SKILL.md
    │   ├── SKILL.zh-CN.md
    │   └── templates/
    ├── tasks/
    │   ├── SKILL.md
    │   ├── SKILL.zh-CN.md
    │   └── templates/
    ├── implement/
    │   ├── SKILL.md
    │   └── SKILL.zh-CN.md
    ├── debt/
    │   ├── SKILL.md
    │   ├── SKILL.zh-CN.md
    │   └── templates/
    ├── scripts/
    │   └── install-templates     # 可选：复制模板到目标仓库 .sdd/templates/
    ├── references/                 # 兼容保留：旧 stage notes
    ├── templates/                  # 兼容保留：旧共享模板
    └── commands/                  # 保留的兼容/参考 command，不是 skill 主入口
```

## 使用方式

把 `standard/` 作为一个 skill 目录集成到目标仓库或目标系统中。

根目录下的 `README.md`、`sdd-flow.zh-CN.md`、`sdd-flow-presentation.html` 都是说明或展示材料。

`lean/`、`standard/commands/`、`standard/references/` 和顶层 `standard/templates/` 先保留为参考/兼容材料。

真正的 pure skill 入口是 `standard/SKILL.md`；各阶段也可以作为独立 skill 使用。

`standard/` 下的 stage skill、templates 和保留材料都提供英文版与中文版；中文文件使用 `.zh-CN.md` 后缀。

入口是：

```text
standard/SKILL.md
```

阶段 skill 是：

```text
standard/workflow/SKILL.md
standard/requirement/SKILL.md
standard/plan/SKILL.md
standard/adr/SKILL.md
standard/tasks/SKILL.md
standard/implement/SKILL.md
standard/debt/SKILL.md
```

如果目标仓库还没有本地模板，先运行：

```bash
standard/scripts/install-templates <target-repo>
```

模板会复制到：

```text
<target-repo>/.sdd/templates/
```

脚本默认跳过已有模板；升级或重置模板时使用 `--force`。

这个 skill 会根据用户意图和现有 artifact 自动选择阶段：

| 用户意图 | 阶段 | 主要输入 | 主要输出 |
|---|---|---|---|
| 开始 / 选择 / 完成 workflow | Workflow | 用户描述 / `specs/index.md` | `specs/index.md`, `specs/active/<id-slug>/`, `specs/complete/<id-slug>/` |
| 定义需求 / 开始功能 | Requirement | 用户描述 / PRD / issue | `specs/active/<id-slug>/requirement.md` |
| 做技术方案 / 调研 / 设计 | Plan | `requirement.md` | `plan.md`, 可选 `research.md`, `contracts/` |
| 沉淀长期技术决策 | ADR | `plan.md`, `research.md` | `docs/adr/index.md`, `docs/adr/ADR-XXXX-title.md` |
| 拆任务 | Tasks | `requirement.md`, `plan.md` | `tasks.md` |
| 执行任务 | Implement | `tasks.md`, `plan.md`, `requirement.md` | 代码变更、更新后的 `tasks.md` |
| 记录延后事项 | Debt | 实现后的已接受遗留问题 | `docs/debt/<id-slug>-debt.md` |

## 工作流

### 0. Workflow

每个工作单元都有编号，并记录在：

```text
specs/index.md
```

新任务默认进入：

```text
specs/active/<id-slug>/
```

完成并验收后移动到：

```text
specs/complete/<id-slug>/
```

如果只有一个 active workflow，可以默认选择它；如果有多个且无法从上下文判断，必须询问用户。

### 1. Requirement

生成或更新：

```text
specs/active/<id-slug>/requirement.md
```

Requirement 是长期需求事实，不写实现方案、不写任务拆解。

### 2. Plan

基于 `requirement.md` 生成：

```text
specs/active/<id-slug>/plan.md
```

必要时生成：

```text
specs/active/<id-slug>/research.md
specs/active/<id-slug>/contracts/
```

`research.md` 只用于真实不确定性：选型、外部约束、风险验证、契约探索。

### 3. ADR

不是所有 research 都进入 ADR。只有长期需要解释的关键决策才沉淀为：

```text
docs/adr/index.md
docs/adr/ADR-XXXX-title.md
```

`docs/adr/index.md` 是 ADR 管理入口，列出决策、状态、日期、文件和替代关系。需要理解已有决策时先读 index，再按需打开具体 ADR。

### 4. Tasks

基于 `requirement.md` 和 `plan.md` 生成：

```text
specs/active/<id-slug>/tasks.md
```

Standard tasks 使用块状结构：`Files`、`Interfaces`、TDD 微步骤、Review Gate。

### 5. Implement

执行 `tasks.md` 时，skill 使用 Superpowers 风格的执行纪律：

- 执行前审查任务和设计是否冲突
- 行为变更先写失败测试
- 先看红，再写最小实现，再看绿
- 意外失败先找根因，不猜
- 任务完成前做 task review
- 阶段完成后跑 Review Gate
- 没有新鲜验证证据，不声明完成

### 6. Debt

Debt 只在实现后记录，并且只记录已接受的非阻塞遗留问题。

不要把失败测试、未满足验收标准、模糊需求或必须修的问题塞进 debt。

## 设计原则

- Requirement 负责需求事实。
- Workflow 负责编号、active/complete 状态和 `specs/index.md`。
- Plan 负责设计判断。
- Research 负责决策证据。
- ADR 负责长期架构决策。
- Tasks 负责可执行拆解和质量门禁。
- Implement 负责按任务和验证纪律落地。
- Debt 负责记录已接受的后续事项。

详细流程见 [sdd-flow.zh-CN.md](sdd-flow.zh-CN.md)。
