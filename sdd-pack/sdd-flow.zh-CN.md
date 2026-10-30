# Standard SDD Artifact Flow

```mermaid
flowchart TD
    W[Workflow Registry<br/>specs/index.md<br/>active / complete] --> A
    A[Requirement<br/>需求事实] --> B

    subgraph plan_subgraph ["Plan"]
        B[Plan<br/>实现策略 / 技术设计]
        C{是否需要 research?}
        D[research.md<br/>调研 / 决策依据]
        E{是否需要 contracts?}
        F[contracts/<br/>API / Event / CLI / Library Contract]
        G[Test Strategy<br/>测试策略]

        B --> C
        C -- 是 --> D
        C -- 否 --> G
        D --> B

        B --> E
        E -- 是 --> F
        E -- 否 --> G
        F --> B

        B --> G
    end

    subgraph archive_subgraph ["沉淀"]
        N[ADR<br/>Architecture Decision Record]
        M[正式契约目录 / 代码仓库]
    end

    D -. 长期关键决策 .-> N
    B -. 长期关键决策 .-> N
    F -. 稳定后回流 .-> M

    G --> H

    subgraph tasks_subgraph ["Tasks"]
        H[Task 拆解<br/>按 User Story 组织<br/>按组件细化]

        H --> H1[Phase 1: Setup]
        H --> H2[Phase 2: Foundational]
        H2 --> H3[Phase 3+: Story Phases]
        H3 --> H4[Final: Polish]

        H3 --> T

        subgraph tdd_subgraph ["每个 Task 的执行纪律"]
            T[Task N<br/>Files / Interfaces<br/>Consumes / Produces]
            T --> I[Red<br/>先写失败测试]
            I --> J[Green<br/>最小实现通过测试]
            J --> K[Refactor<br/>保持测试通过]
            K --> TR[Task Review<br/>规格 + 质量 + 验证]
        end

        TR --> RV{Review Gate}
        RV -- 不通过 --> T
        RV -- 通过 --> NEXT{还有 Task?}
        NEXT -- 是 --> T
    end

    NEXT -- 否 --> L[Implementation<br/>完成变更]
    L -. 已接受的非阻塞遗留 .-> O[Debt<br/>技术债 / 产品债 / 运营债]
```

## 核心链路

```text
Workflow -> Requirement -> Plan / Research -> ADR? -> Tasks -> Implementation -> Debt?
```

## Artifact 规则

| Artifact | 策略 | 说明 |
|---|---|---|
| `specs/index.md` | 必需 | workflow registry，管理编号、active/complete、当前阶段和路径 |
| `specs/active/<id-slug>/` | 必需 | 当前进行中的 workflow 目录 |
| `specs/complete/<id-slug>/` | 完成后必需 | 已验收或 review 完成的 workflow 目录 |
| `requirement.md` | 必需 | 长期需求资产，描述系统应该是什么 |
| `plan.md` | 必需 | 实现策略、技术设计、测试策略 |
| `research.md` | 可选 | 只有存在不确定性、选型、外部约束或风险验证时生成 |
| `contracts/` | 可选 | 有外部接口、事件、CLI、library contract 时生成 |
| `ADR` | 可选回流 | `research.md` / `plan.md` 中仍有长期解释价值的关键决策，用 `adr-template.md` 沉淀，并用 `docs/adr/index.md` 管理 |
| `tasks.md` | 必需 | 按 User Story 分 Phase 组织，每个 Task 声明 Files/Interfaces，承载 TDD 微循环和 Review Gate |
| `debt` | 可选回流 | 实现后仍未解决、被明确接受或延后的事项，用 `debt-template.md` 沉淀 |

## 分工原则

`Workflow` 负责编号、active/complete 状态和 `specs/index.md`。

`Requirement` 负责需求事实。

`Plan` 负责设计判断。

`Research` 负责决策证据。

`ADR` 负责长期架构决策记录；`docs/adr/index.md` 负责快速检索和状态管理。

`Contracts` 负责外部契约。

`Tasks` 负责拆解、执行纪律和质量门禁。

`Implement` 负责按任务、TDD、Review Gate 和验证证据完成代码。

`Debt` 负责记录实现后遗留的、已接受的未来事项。
