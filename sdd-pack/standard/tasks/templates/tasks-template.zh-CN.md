---
description: "Task list template for feature implementation"
---

# 任务清单：[功能名称]

**输入**：来自 `/specs/[###-feature-name]/` 的设计文档

**前置条件**：plan.md (必须), requirement.md (用户故事、需求和验收标准需要), research.md, data-model.md, contracts/

**组织方式**：任务按用户故事 (User Story) 分组，以便能够对每个故事进行独立的实现和测试。

## 格式规范

每个任务均为一个块结构，包含标题头、Files/Interfaces 声明块以及 TDD 微步骤：

```markdown
### T012 [P] [US1] Create User model

**Files:**
- Create: `src/models/user.py`
- Test: `tests/unit/test_user.py`

**Interfaces:**
- Consumes: N/A
- Produces: `User(id: str, name: str, email: str)`, `UserRepository.get(id: str) -> User`

- [ ] T012.1 Write failing test in tests/unit/test_user.py
- [ ] T012.2 Run: `pytest tests/unit/test_user.py -v` → Expected: FAIL
- [ ] T012.3 Implement minimal code in src/models/user.py
- [ ] T012.4 Run: `pytest tests/unit/test_user.py -v` → Expected: PASS
- [ ] T012.5 Checkpoint: 确认测试通过，保存进度
```

**格式组件说明**：

- **任务 ID (Task ID)**：按执行顺序递增的序号（T001, T002, T003...）
- **[P] 标记**：仅当任务可并行时包含（操作不同的文件且无依赖关系）
- **[Story] 标签**：用户故事阶段的任务**必须**包含（例如，[US1], [US2]）
  - 初始化/基础性/打磨阶段：无 Story 标签
  - 用户故事阶段：**必须**有 Story 标签
- **Files 声明块**：列出该任务创建、修改或测试的每一个文件（精确的相对路径）
- **Interfaces 声明块**：
  - Consumes：该任务消耗自先前任务的哪些内容（精确的签名）
  - Produces：后续任务所依赖的产出内容（精确的函数名、参数和返回类型）
- **子步骤 (Sub-steps)**：TDD 微循环步骤（`TN.1` 到 `TN.5`），每个步骤都是一个 2-5 分钟的单一动作

## 路径约定

- **单一项目**：仓库根目录下的 `src/` 和 `tests/`
- **Web 应用**：`backend/src/` 和 `frontend/src/`
- **移动端**：`api/src/`, `ios/src/` 或 `android/src/`
- 下方示例路径假设为单一项目结构 —— 请根据 plan.md 的实际结构进行调整

## 禁止模式 (Prohibited Patterns)

以下内容**绝对不允许**出现在 tasks.md 中：

- "TBD", "TODO", "稍后实现 (implement later)", "填充细节 (fill in details)"
- "添加适当的错误处理" / "添加校验"（而未指定具体内容）
- "类似于任务 N (Similar to Task N)"（必须重复完整的规格说明 —— 开发者可能会乱序阅读任务）
- 缺少具体文件路径的描述
- 在展开 TDD 微步骤时，缺少具体测试/实现代码块的步骤
- 引用了未在任何任务的 Interfaces 块中定义的类型、函数或方法

<!--
  ============================================================================
  重要提示：以下任务仅作为演示用的 示例任务。

  Standard SDD 的 Tasks 阶段必须根据以下内容，将它们替换为真实的开发任务：
  - 来自 requirement.md 的用户故事（及其优先级 P1, P2, P3...）
  - 来自 requirement.md 的功能需求与验收标准
  - 来自 plan.md 的 File Structure Mapping（驱动 Files 声明）
  - 来自 data-model.md 的实体
  - 来自 contracts/ 的接口端点

  任务必须按用户故事组织，以便每个故事都能：
  - 独立实现
  - 独立测试
  - 作为 MVP 增量交付

  切勿在生成的 tasks.md 文件中保留这些示例任务。
  ============================================================================
-->

## 阶段 1：初始化与准备 (Setup)

**目标**：项目初始化和基础结构搭建

### T001 根据实施计划创建项目结构

**Files:**
- Create: 根据 plan.md 项目结构创建 `src/`, `tests/` 及相关配置文件

**Interfaces:**
- Consumes: N/A
- Produces: 项目目录布局

- [ ] T001.1 根据 plan.md 创建目录结构
- [ ] T001.2 验证目录结构与计划一致
- [ ] T001.3 Checkpoint: 确认测试通过，保存进度

### T002 初始化 [语言] 项目并添加 [框架] 依赖

**Files:**
- Create: `pyproject.toml` (或等效文件)
- Create: `src/__init__.py`

**Interfaces:**
- Consumes: 来自 T001 的项目结构
- Produces: 可导入的包、可运行的测试套件

- [ ] T002.1 初始化项目并添加依赖项
- [ ] T002.2 运行：`[测试命令]` → 预期：收集到 0 个测试，无错误
- [ ] T002.3 Checkpoint: 确认测试通过，保存进度

### T003 [P] 配置代码检查 (Linting) 和格式化 (Formatting) 工具

**Files:**
- Create: `.ruff.toml` / `.eslintrc` (或等效文件)

**Interfaces:**
- Consumes: 来自 T001 的项目结构
- Produces: 可用的 `lint` 和 `format` 命令

- [ ] T003.1 添加代码检查与格式化配置
- [ ] T003.2 运行：`[检查命令]` → 预期：PASS，无警告
- [ ] T003.3 Checkpoint: 确认测试通过，保存进度

**Review Gate**: 确认项目成功初始化，所有工具均能正常运行且无报错。

---

## 阶段 2：基础架构 (Foundational)

**目标**：在开始实现**任何**用户故事之前，必须先完成的核心基础设施

**⚠️ 关键提示**：在完成此阶段之前，不得开始任何用户故事的开发

基础架构任务示例（请根据你的项目进行调整）：

### T004 设置数据库 Schema 和数据库迁移 (Migrations) 框架

**Files:**
- Create: `src/db/schema.py`
- Create: `src/db/migrations/`
- Test: `tests/integration/test_db.py`

**Interfaces:**
- Consumes: 来自 T002 的项目
- Produces: `Database.connect() -> Connection`, `migrate() -> None`

- [ ] T004.1 在 tests/integration/test_db.py 中编写失败的数据库连接测试
- [ ] T004.2 运行：`[测试命令] tests/integration/test_db.py -v` → 预期：FAIL
- [ ] T004.3 在 src/db/schema.py 中实现 schema 和连接逻辑
- [ ] T004.4 运行：`[测试命令] tests/integration/test_db.py -v` → 预期：PASS
- [ ] T004.5 Checkpoint: 确认测试通过，保存进度

### T005 [P] 实现认证与授权 (Authentication/Authorization) 框架

**Files:**
- Create: `src/auth/middleware.py`
- Test: `tests/unit/test_auth.py`

**Interfaces:**
- Consumes: 来自 T002 的项目
- Produces: `AuthMiddleware.authenticate(request: Request) -> User`, `@require_auth` 装饰器

- [ ] T005.1 在 tests/unit/test_auth.py 中编写失败的认证中间件测试
- [ ] T005.2 运行：`[测试命令] tests/unit/test_auth.py -v` → 预期：FAIL
- [ ] T005.3 在 src/auth/middleware.py 中实现认证中间件
- [ ] T005.4 运行：`[测试命令] tests/unit/test_auth.py -v` → 预期：PASS
- [ ] T005.5 Checkpoint: 确认测试通过，保存进度

### T006 [P] 设置 API 路由与中间件结构

**Files:**
- Create: `src/api/router.py`
- Test: `tests/unit/test_router.py`

**Interfaces:**
- Consumes: 来自 T005 的认证模块
- Produces: `Router.register(path: str, handler: Callable) -> None`, `app` ASGI/WSGI 应用

- [ ] T006.1 在 tests/unit/test_router.py 中编写失败的路由测试
- [ ] T006.2 运行：`[测试命令] tests/unit/test_router.py -v` → 预期：FAIL
- [ ] T006.3 在 src/api/router.py 中实现路由逻辑
- [ ] T006.4 运行：`[测试命令] tests/unit/test_router.py -v` → 预期：PASS
- [ ] T006.5 Checkpoint: 确认测试通过，保存进度

**Review Gate**: 基础架构就绪 —— 所有基础阶段任务均已通过测试，实际接口与声明一致。现可并行开始用户故事的开发。

---

## 阶段 3：用户故事 1 - [标题] (优先级: P1) 🎯 MVP

**目标**：[简要描述该故事交付的价值]

**独立测试**：[如何验证该故事能独立工作运行]

### T010 [P] [US1] 创建 [Entity1] 模型

**Files:**
- Create: `src/models/[entity1].py`
- Test: `tests/unit/test_[entity1].py`

**Interfaces:**
- Consumes: 来自 T004 的数据库模块 — `Database.connect() -> Connection`
- Produces: `[Entity1](id: str, field1: type, field2: type)`, `[Entity1]Repository.get(id: str) -> [Entity1]`, `[Entity1]Repository.save(entity: [Entity1]) -> None`

- [ ] T010.1 在 tests/unit/test_[entity1].py 中编写关于 [Entity1] 的失败测试

```python
def test_create_entity1():
    entity = Entity1(id="1", field1="value1", field2="value2")
    assert entity.id == "1"
    assert entity.field1 == "value1"
```

- [ ] T010.2 运行：`[测试命令] tests/unit/test_[entity1].py -v` → 预期：FAIL，报错提示 "Entity1 not defined"
- [ ] T010.3 在 src/models/[entity1].py 中实现 [Entity1] 模型
- [ ] T010.4 运行：`[测试命令] tests/unit/test_[entity1].py -v` → 预期：PASS
- [ ] T010.5 Checkpoint: 确认测试通过，保存进度

### T011 [P] [US1] 创建 [Entity2] 模型

**Files:**
- Create: `src/models/[entity2].py`
- Test: `tests/unit/test_[entity2].py`

**Interfaces:**
- Consumes: 来自 T004 的数据库模块 — `Database.connect() -> Connection`
- Produces: `[Entity2](id: str, ...)`, `[Entity2]Repository.get(id: str) -> [Entity2]`

- [ ] T011.1 在 tests/unit/test_[entity2].py 中编写失败的测试
- [ ] T011.2 运行：`[测试命令] tests/unit/test_[entity2].py -v` → 预期：FAIL
- [ ] T011.3 在 src/models/[entity2].py 中实现 [Entity2]
- [ ] T011.4 运行：`[测试命令] tests/unit/test_[entity2].py -v` → 预期：PASS
- [ ] T011.5 Checkpoint: 确认测试通过，保存进度

### T012 [US1] 实现 [Service] 服务逻辑

**Files:**
- Create: `src/services/[service].py`
- Test: `tests/unit/test_[service].py`

**Interfaces:**
- Consumes: 来自 T010 的 `[Entity1]Repository.get(id: str) -> [Entity1]`，来自 T011 的 `[Entity2]Repository.get(id: str) -> [Entity2]`
- Produces: `[Service].create(params: CreateParams) -> [Entity1]`, `[Service].get(id: str) -> [Entity1]`

- [ ] T012.1 在 tests/unit/test_[service].py 中编写失败的测试
- [ ] T012.2 运行：`[测试命令] tests/unit/test_[service].py -v` → 预期：FAIL
- [ ] T012.3 在 src/services/[service].py 中实现 [Service] (依赖 T010, T011)
- [ ] T012.4 运行：`[测试命令] tests/unit/test_[service].py -v` → 预期：PASS
- [ ] T012.5 Checkpoint: 确认测试通过，保存进度

### T013 [US1] 实现 [endpoint/feature] 接口/功能

**Files:**
- Create: `src/api/[endpoint].py`
- Test: `tests/integration/test_[endpoint].py`

**Interfaces:**
- Consumes: 来自 T012 的 `[Service].create(params) -> [Entity1]`，来自 T006 的 `Router.register()`
- Produces: `POST /api/[resource]` 接口, `GET /api/[resource]/:id` 接口

- [ ] T013.1 在 tests/integration/test_[endpoint].py 中编写失败的集成测试
- [ ] T013.2 运行：`[测试命令] tests/integration/test_[endpoint].py -v` → 预期：FAIL
- [ ] T013.3 在 src/api/[endpoint].py 中实现接口
- [ ] T013.4 运行：`[测试命令] tests/integration/test_[endpoint].py -v` → 预期：PASS
- [ ] T013.5 Checkpoint: 确认测试通过，保存进度

**Review Gate**: 用户故事 1 功能完全实现且可独立测试。所有 Interfaces 声明与实际一致。运行完整测试套件。

---

## 阶段 4：用户故事 2 - [标题] (优先级: P2)

**目标**：[简要描述该故事交付的价值]

**独立测试**：[如何验证该故事能独立工作运行]

### T020 [P] [US2] 创建 [Entity] 模型

**Files:**
- Create: `src/models/[entity].py`
- Test: `tests/unit/test_[entity].py`

**Interfaces:**
- Consumes: 来自 T004 的数据库模块 — `Database.connect() -> Connection`
- Produces: `[Entity](id: str, ...)`, `[Entity]Repository.get(id: str) -> [Entity]`

- [ ] T020.1 在 tests/unit/test_[entity].py 中编写失败的测试
- [ ] T020.2 运行：`[测试命令] tests/unit/test_[entity].py -v` → 预期：FAIL
- [ ] T020.3 在 src/models/[entity].py 中实现 [Entity]
- [ ] T020.4 运行：`[测试命令] tests/unit/test_[entity].py -v` → 预期：PASS
- [ ] T020.5 Checkpoint: 确认测试通过，保存进度

### T021 [US2] 实现 [Service] 服务逻辑

**Files:**
- Create: `src/services/[service].py`
- Test: `tests/unit/test_[service].py`

**Interfaces:**
- Consumes: 来自 T020 的 `[Entity]Repository`
- Produces: `[Service].execute(params: Params) -> Result`

- [ ] T021.1 在 tests/unit/test_[service].py 中编写失败的测试
- [ ] T021.2 运行：`[测试命令] tests/unit/test_[service].py -v` → 预期：FAIL
- [ ] T021.3 在 src/services/[service].py 中实现 [Service]
- [ ] T021.4 运行：`[测试命令] tests/unit/test_[service].py -v` → 预期：PASS
- [ ] T021.5 Checkpoint: 确认测试通过，保存进度

### T022 [US2] 实现 [endpoint/feature] 接口/功能

**Files:**
- Create: `src/api/[endpoint].py`
- Test: `tests/integration/test_[endpoint].py`

**Interfaces:**
- Consumes: 来自 T021 的 `[Service].execute()`，来自 T006 的 `Router.register()`
- Produces: `POST /api/[resource]` 接口

- [ ] T022.1 在 tests/integration/test_[endpoint].py 中编写失败的集成测试
- [ ] T022.2 运行：`[测试命令] tests/integration/test_[endpoint].py -v` → 预期：FAIL
- [ ] T022.3 在 src/api/[endpoint].py 中实现接口
- [ ] T022.4 运行：`[测试命令] tests/integration/test_[endpoint].py -v` → 预期：PASS
- [ ] T022.5 Checkpoint: 确认测试通过，保存进度

**Review Gate**: 用户故事 1 和 2 均可独立运行。所有 Interfaces 声明与实际相符。运行完整测试套件通过。

---

## 阶段 5：用户故事 3 - [标题] (优先级: P3)

**目标**：[简要描述该故事交付的价值]

**独立测试**：[如何验证该故事能独立工作运行]

### T030 [P] [US3] 创建 [Entity] 模型

**Files:**
- Create: `src/models/[entity].py`
- Test: `tests/unit/test_[entity].py`

**Interfaces:**
- Consumes: 来自 T004 的数据库模块
- Produces: `[Entity](id: str, ...)`, `[Entity]Repository.get(id: str) -> [Entity]`

- [ ] T030.1 在 tests/unit/test_[entity].py 中编写失败的测试
- [ ] T030.2 运行：`[测试命令] tests/unit/test_[entity].py -v` → 预期：FAIL
- [ ] T030.3 在 src/models/[entity].py 中实现 [Entity]
- [ ] T030.4 运行：`[测试命令] tests/unit/test_[entity].py -v` → 预期：PASS
- [ ] T030.5 Checkpoint: 确认测试通过，保存进度

### T031 [US3] 实现 [Service] 服务逻辑

**Files:**
- Create: `src/services/[service].py`
- Test: `tests/unit/test_[service].py`

**Interfaces:**
- Consumes: 来自 T030 的 `[Entity]Repository`
- Produces: `[Service].process(input: Input) -> Output`

- [ ] T031.1 在 tests/unit/test_[service].py 中编写失败的测试
- [ ] T031.2 运行：`[测试命令] tests/unit/test_[service].py -v` → 预期：FAIL
- [ ] T031.3 在 src/services/[service].py 中实现 [Service]
- [ ] T031.4 运行：`[测试命令] tests/unit/test_[service].py -v` → 预期：PASS
- [ ] T031.5 Checkpoint: 确认测试通过，保存进度

**Review Gate**: 所有用户故事均已独立可用。所有 Interfaces 声明一致。运行完整测试套件通过。

---

[按需添加更多用户故事阶段，遵循相同模式]

---

## 阶段 N：打磨与交叉关注点 (Polish & Cross-Cutting Concerns)

**目标**：影响多个用户故事的优化与改进

### TXXX [P] 更新文档

**Files:**
- Modify: 修改 `docs/[相关文档].md`

**Interfaces:**
- Consumes: 所有已实现的故事接口 (Interfaces)
- Produces: 更新后的 API 文档、README 等

- [ ] TXXX.1 更新文档以反映已实现的功能
- [ ] TXXX.2 验证文档中的所有代码示例能正常运行
- [ ] TXXX.3 Checkpoint: 确认测试通过，保存进度

### TXXX 性能优化

**Files:**
- Modify: 修改通过性能剖析 (profiling) 定位到的文件

**Interfaces:**
- Consumes: 现有的接口 (Interfaces)（不改变函数签名）
- Produces: 相同接口，但提升了性能

- [ ] TXXX.1 剖析并识别性能瓶获
- [ ] TXXX.2 编写基准测试 (benchmark)
- [ ] TXXX.3 运行基准测试 → 记录基准线 (baseline)
- [ ] TXXX.4 实现性能优化
- [ ] TXXX.5 运行基准测试 → 确认性能提升
- [ ] TXXX.6 运行完整测试套件 → 预期：全部 PASS（无回归）
- [ ] TXXX.7 Checkpoint: 确认测试通过，保存进度

**Review Gate**: 所有优化打磨任务完成，完整测试套件通过，文档准确无误。

---

## 依赖关系与执行顺序 (Dependencies & Execution Order)

### 阶段依赖关系

- **准备阶段 (Phase 1)**：无依赖 —— 可立即开始
- **基础架构 (Phase 2)**：依赖准备阶段的完成 —— 阻塞所有用户故事的开发
- **用户故事 (Phase 3+)**：均依赖基础架构阶段的完成
  - 之后各用户故事可并行推进（若人力充足）
  - 或按优先级顺序（P1 → P2 → P3）串行推进
- **打磨阶段 (Final Phase)**：依赖所有选定用户故事的完成

### 用户故事依赖关系

- **用户故事 1 (P1)**：可在基础架构（阶段 2）完成后开始 —— 不依赖其他故事
- **用户故事 2 (P2)**：可在基础架构（阶段 2）完成后开始 —— 可与 US1 整合，但必须能独立测试
- **用户故事 3 (P3)**：可在基础架构（阶段 2）完成后开始 —— 可与 US1/US2 整合，但必须能独立测试

### 任务内部的执行顺序

- 先编写测试，并验证其运行失败 (FAIL)
- 编写最少量的实现代码使测试通过 (PASS)
- 验证测试通过
- 每个任务测试通过后，原子化地保存进度（Checkpoint）
- 在当前任务的测试未通过前，切勿进入下一个任务

### 并行开发机会

- 准备阶段所有标记为 `[P]` 的任务可并行运行
- 基础架构阶段所有标记为 `[P]` 的任务可并行运行（在阶段 2 内）
- 一旦基础架构阶段完成，所有用户故事可并行开始（若团队资源允许）
- 故事内标记为 `[P]` 的模型定义可并行运行
- 不同的用户故事可由不同的团队成员并行开发

---

## 实施策略 (Implementation Strategy)

### MVP 优先（仅用户故事 1）

1. 完成阶段 1：准备工作 (Setup)
2. 完成阶段 2：基础架构 (Foundational)（关键 —— 阻塞所有用户故事）
3. 完成阶段 3：用户故事 1
4. **Review Gate**：独立测试用户故事 1，验证所有 Interfaces
5. 若就绪，即可进行部署/演示

### 渐进式交付

1. 完成 Setup + Foundational → 基础就绪
2. 加入用户故事 1 → Review Gate → 部署/演示（MVP!）
3. 加入用户故事 2 → Review Gate → 部署/演示
4. 加入用户故事 3 → Review Gate → 部署/演示
5. 每个故事都在不破坏先前故事的前提下增加价值

### 团队并行策略

多名开发人员协作时：

1. 团队共同完成 Setup + Foundational
2. Foundational 完成后：
   - 开发人员 A：用户故事 1
   - 开发人员 B：用户故事 2
   - 开发人员 C：用户故事 3
3. 故事各自独立完成和整合
4. 每位开发人员在合并前运行 Review Gate 验证

---

## 备注

- `[P]` 任务 = 涉及不同文件，无依赖关系
- `[Story]` 标签将任务映射到具体用户故事，便于追溯
- 每个用户故事应可独立完成并测试
- TDD 微步骤是强制性的：每个任务均需经历 Red → Green → Checkpoint
- Interfaces 声明必须精确（函数签名 + 类型）
- 每个阶段末尾的 Review Gate 用于校验接口一致性与测试覆盖率
- 可以在任何 Checkpoint 暂停，以独立验证用户故事
- 避免：模糊的任务描述、占位符、相同文件冲突、破坏独立性的跨故事依赖
