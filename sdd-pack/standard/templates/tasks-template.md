---

description: "Task list template for feature implementation"
---

# Tasks: [FEATURE NAME]

**Input**: Design documents from `/specs/[###-feature-name]/`

**Prerequisites**: plan.md (required), requirement.md (required for user stories, requirements, and acceptance criteria), research.md, data-model.md, contracts/

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format

Each task is a block with header, Files/Interfaces declaration, and TDD micro-steps:

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

**Format Components**:

- **Task ID**: Sequential number (T001, T002, T003...) in execution order
- **[P] marker**: Include ONLY if task is parallelizable (different files, no dependencies)
- **[Story] label**: REQUIRED for user story phase tasks (e.g., [US1], [US2])
  - Setup / Foundational / Polish phases: NO story label
  - User Story phases: MUST have story label
- **Files block**: List every file this task creates, modifies, or tests (exact paths)
- **Interfaces block**: Consumes = what this task uses from earlier tasks (exact signatures). Produces = what later tasks rely on (exact function names, parameter and return types)
- **Sub-steps**: TDD micro-cycle steps (`TN.1` through `TN.5`), each a single 2-5 minute action

## Path Conventions

- **Single project**: `src/`, `tests/` at repository root
- **Web app**: `backend/src/`, `frontend/src/`
- **Mobile**: `api/src/`, `ios/src/` or `android/src/`
- Paths shown below assume single project - adjust based on plan.md structure

## Prohibited Patterns

The following MUST NOT appear in tasks.md:

- "TBD", "TODO", "implement later", "fill in details"
- "Add appropriate error handling" / "add validation" (without specific content)
- "Similar to Task N" (repeat the full specification — the implementer may read tasks out of order)
- Descriptions without file paths
- Code steps without code blocks
- References to types, functions, or methods not defined in any task's Interfaces block

<!--
  ============================================================================
  IMPORTANT: The tasks below are SAMPLE TASKS for illustration purposes only.

  During the Standard SDD Tasks stage, replace these with actual tasks based on:
  - User stories from requirement.md (with their priorities P1, P2, P3...)
  - Feature requirements and acceptance criteria from requirement.md
  - File Structure Mapping from plan.md (drives Files declarations)
  - Entities from data-model.md
  - Endpoints from contracts/

  Tasks MUST be organized by user story so each story can be:
  - Implemented independently
  - Tested independently
  - Delivered as an MVP increment

  DO NOT keep these sample tasks in the generated tasks.md file.
  ============================================================================
-->

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure

### T001 Create project structure per implementation plan

**Files:**
- Create: `src/`, `tests/`, config files per plan.md Project Structure

**Interfaces:**
- Consumes: N/A
- Produces: Project directory layout

- [ ] T001.1 Create directory structure per plan.md
- [ ] T001.2 Verify structure matches plan
- [ ] T001.3 Checkpoint: 确认测试通过，保存进度

### T002 Initialize [language] project with [framework] dependencies

**Files:**
- Create: `pyproject.toml` (or equivalent)
- Create: `src/__init__.py`

**Interfaces:**
- Consumes: Project structure from T001
- Produces: Importable package, runnable test suite

- [ ] T002.1 Initialize project and add dependencies
- [ ] T002.2 Run: `[test command]` → Expected: 0 tests collected, no errors
- [ ] T002.3 Checkpoint: 确认测试通过，保存进度

### T003 [P] Configure linting and formatting tools

**Files:**
- Create: `.ruff.toml` / `.eslintrc` (or equivalent)

**Interfaces:**
- Consumes: Project structure from T001
- Produces: `lint` and `format` commands available

- [ ] T003.1 Add linting/formatting config
- [ ] T003.2 Run: `[lint command]` → Expected: PASS, no warnings
- [ ] T003.3 Checkpoint: 确认测试通过，保存进度

**Review Gate**: Confirm project initializes, all tools run, no errors.

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

Examples of foundational tasks (adjust based on your project):

### T004 Setup database schema and migrations framework

**Files:**
- Create: `src/db/schema.py`
- Create: `src/db/migrations/`
- Test: `tests/integration/test_db.py`

**Interfaces:**
- Consumes: Project from T002
- Produces: `Database.connect() -> Connection`, `migrate() -> None`

- [ ] T004.1 Write failing test for DB connection in tests/integration/test_db.py
- [ ] T004.2 Run: `[test command] tests/integration/test_db.py -v` → Expected: FAIL
- [ ] T004.3 Implement schema and connection in src/db/schema.py
- [ ] T004.4 Run: `[test command] tests/integration/test_db.py -v` → Expected: PASS
- [ ] T004.5 Checkpoint: 确认测试通过，保存进度

### T005 [P] Implement authentication/authorization framework

**Files:**
- Create: `src/auth/middleware.py`
- Test: `tests/unit/test_auth.py`

**Interfaces:**
- Consumes: Project from T002
- Produces: `AuthMiddleware.authenticate(request: Request) -> User`, `@require_auth` decorator

- [ ] T005.1 Write failing test for auth middleware in tests/unit/test_auth.py
- [ ] T005.2 Run: `[test command] tests/unit/test_auth.py -v` → Expected: FAIL
- [ ] T005.3 Implement auth middleware in src/auth/middleware.py
- [ ] T005.4 Run: `[test command] tests/unit/test_auth.py -v` → Expected: PASS
- [ ] T005.5 Checkpoint: 确认测试通过，保存进度

### T006 [P] Setup API routing and middleware structure

**Files:**
- Create: `src/api/router.py`
- Test: `tests/unit/test_router.py`

**Interfaces:**
- Consumes: Auth from T005
- Produces: `Router.register(path: str, handler: Callable) -> None`, `app` ASGI/WSGI application

- [ ] T006.1 Write failing test for router in tests/unit/test_router.py
- [ ] T006.2 Run: `[test command] tests/unit/test_router.py -v` → Expected: FAIL
- [ ] T006.3 Implement router in src/api/router.py
- [ ] T006.4 Run: `[test command] tests/unit/test_router.py -v` → Expected: PASS
- [ ] T006.5 Checkpoint: 确认测试通过，保存进度

**Review Gate**: Foundation ready — all Foundational tasks pass, Interfaces match declarations. User story implementation can now begin in parallel.

---

## Phase 3: User Story 1 - [Title] (Priority: P1) 🎯 MVP

**Goal**: [Brief description of what this story delivers]

**Independent Test**: [How to verify this story works on its own]

### T010 [P] [US1] Create [Entity1] model

**Files:**
- Create: `src/models/[entity1].py`
- Test: `tests/unit/test_[entity1].py`

**Interfaces:**
- Consumes: Database from T004 — `Database.connect() -> Connection`
- Produces: `[Entity1](id: str, field1: type, field2: type)`, `[Entity1]Repository.get(id: str) -> [Entity1]`, `[Entity1]Repository.save(entity: [Entity1]) -> None`

- [ ] T010.1 Write failing test for [Entity1] in tests/unit/test_[entity1].py

```python
def test_create_entity1():
    entity = Entity1(id="1", field1="value1", field2="value2")
    assert entity.id == "1"
    assert entity.field1 == "value1"
```

- [ ] T010.2 Run: `[test command] tests/unit/test_[entity1].py -v` → Expected: FAIL with "Entity1 not defined"
- [ ] T010.3 Implement [Entity1] model in src/models/[entity1].py
- [ ] T010.4 Run: `[test command] tests/unit/test_[entity1].py -v` → Expected: PASS
- [ ] T010.5 Checkpoint: 确认测试通过，保存进度

### T011 [P] [US1] Create [Entity2] model

**Files:**
- Create: `src/models/[entity2].py`
- Test: `tests/unit/test_[entity2].py`

**Interfaces:**
- Consumes: Database from T004 — `Database.connect() -> Connection`
- Produces: `[Entity2](id: str, ...)`, `[Entity2]Repository.get(id: str) -> [Entity2]`

- [ ] T011.1 Write failing test in tests/unit/test_[entity2].py
- [ ] T011.2 Run: `[test command] tests/unit/test_[entity2].py -v` → Expected: FAIL
- [ ] T011.3 Implement [Entity2] in src/models/[entity2].py
- [ ] T011.4 Run: `[test command] tests/unit/test_[entity2].py -v` → Expected: PASS
- [ ] T011.5 Checkpoint: 确认测试通过，保存进度

### T012 [US1] Implement [Service]

**Files:**
- Create: `src/services/[service].py`
- Test: `tests/unit/test_[service].py`

**Interfaces:**
- Consumes: `[Entity1]Repository.get(id: str) -> [Entity1]` from T010, `[Entity2]Repository.get(id: str) -> [Entity2]` from T011
- Produces: `[Service].create(params: CreateParams) -> [Entity1]`, `[Service].get(id: str) -> [Entity1]`

- [ ] T012.1 Write failing test in tests/unit/test_[service].py
- [ ] T012.2 Run: `[test command] tests/unit/test_[service].py -v` → Expected: FAIL
- [ ] T012.3 Implement [Service] in src/services/[service].py (depends on T010, T011)
- [ ] T012.4 Run: `[test command] tests/unit/test_[service].py -v` → Expected: PASS
- [ ] T012.5 Checkpoint: 确认测试通过，保存进度

### T013 [US1] Implement [endpoint/feature]

**Files:**
- Create: `src/api/[endpoint].py`
- Test: `tests/integration/test_[endpoint].py`

**Interfaces:**
- Consumes: `[Service].create(params) -> [Entity1]` from T012, `Router.register()` from T006
- Produces: `POST /api/[resource]` endpoint, `GET /api/[resource]/:id` endpoint

- [ ] T013.1 Write failing integration test in tests/integration/test_[endpoint].py
- [ ] T013.2 Run: `[test command] tests/integration/test_[endpoint].py -v` → Expected: FAIL
- [ ] T013.3 Implement endpoint in src/api/[endpoint].py
- [ ] T013.4 Run: `[test command] tests/integration/test_[endpoint].py -v` → Expected: PASS
- [ ] T013.5 Checkpoint: 确认测试通过，保存进度

**Review Gate**: User Story 1 fully functional and independently testable. All Interfaces match declarations. Run full test suite.

---

## Phase 4: User Story 2 - [Title] (Priority: P2)

**Goal**: [Brief description of what this story delivers]

**Independent Test**: [How to verify this story works on its own]

### T020 [P] [US2] Create [Entity] model

**Files:**
- Create: `src/models/[entity].py`
- Test: `tests/unit/test_[entity].py`

**Interfaces:**
- Consumes: Database from T004 — `Database.connect() -> Connection`
- Produces: `[Entity](id: str, ...)`, `[Entity]Repository.get(id: str) -> [Entity]`

- [ ] T020.1 Write failing test in tests/unit/test_[entity].py
- [ ] T020.2 Run: `[test command] tests/unit/test_[entity].py -v` → Expected: FAIL
- [ ] T020.3 Implement [Entity] in src/models/[entity].py
- [ ] T020.4 Run: `[test command] tests/unit/test_[entity].py -v` → Expected: PASS
- [ ] T020.5 Checkpoint: 确认测试通过，保存进度

### T021 [US2] Implement [Service]

**Files:**
- Create: `src/services/[service].py`
- Test: `tests/unit/test_[service].py`

**Interfaces:**
- Consumes: `[Entity]Repository` from T020
- Produces: `[Service].execute(params: Params) -> Result`

- [ ] T021.1 Write failing test in tests/unit/test_[service].py
- [ ] T021.2 Run: `[test command] tests/unit/test_[service].py -v` → Expected: FAIL
- [ ] T021.3 Implement [Service] in src/services/[service].py
- [ ] T021.4 Run: `[test command] tests/unit/test_[service].py -v` → Expected: PASS
- [ ] T021.5 Checkpoint: 确认测试通过，保存进度

### T022 [US2] Implement [endpoint/feature]

**Files:**
- Create: `src/api/[endpoint].py`
- Test: `tests/integration/test_[endpoint].py`

**Interfaces:**
- Consumes: `[Service].execute()` from T021, `Router.register()` from T006
- Produces: `POST /api/[resource]` endpoint

- [ ] T022.1 Write failing integration test in tests/integration/test_[endpoint].py
- [ ] T022.2 Run: `[test command] tests/integration/test_[endpoint].py -v` → Expected: FAIL
- [ ] T022.3 Implement endpoint in src/api/[endpoint].py
- [ ] T022.4 Run: `[test command] tests/integration/test_[endpoint].py -v` → Expected: PASS
- [ ] T022.5 Checkpoint: 确认测试通过，保存进度

**Review Gate**: User Stories 1 AND 2 both work independently. All Interfaces match. Full test suite passes.

---

## Phase 5: User Story 3 - [Title] (Priority: P3)

**Goal**: [Brief description of what this story delivers]

**Independent Test**: [How to verify this story works on its own]

### T030 [P] [US3] Create [Entity] model

**Files:**
- Create: `src/models/[entity].py`
- Test: `tests/unit/test_[entity].py`

**Interfaces:**
- Consumes: Database from T004
- Produces: `[Entity](id: str, ...)`, `[Entity]Repository.get(id: str) -> [Entity]`

- [ ] T030.1 Write failing test in tests/unit/test_[entity].py
- [ ] T030.2 Run: `[test command] tests/unit/test_[entity].py -v` → Expected: FAIL
- [ ] T030.3 Implement [Entity] in src/models/[entity].py
- [ ] T030.4 Run: `[test command] tests/unit/test_[entity].py -v` → Expected: PASS
- [ ] T030.5 Checkpoint: 确认测试通过，保存进度

### T031 [US3] Implement [Service]

**Files:**
- Create: `src/services/[service].py`
- Test: `tests/unit/test_[service].py`

**Interfaces:**
- Consumes: `[Entity]Repository` from T030
- Produces: `[Service].process(input: Input) -> Output`

- [ ] T031.1 Write failing test in tests/unit/test_[service].py
- [ ] T031.2 Run: `[test command] tests/unit/test_[service].py -v` → Expected: FAIL
- [ ] T031.3 Implement [Service] in src/services/[service].py
- [ ] T031.4 Run: `[test command] tests/unit/test_[service].py -v` → Expected: PASS
- [ ] T031.5 Checkpoint: 确认测试通过，保存进度

**Review Gate**: All user stories independently functional. All Interfaces consistent. Full test suite passes.

---

[Add more user story phases as needed, following the same pattern]

---

## Phase N: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories

### TXXX [P] Documentation updates

**Files:**
- Modify: `docs/[relevant].md`

**Interfaces:**
- Consumes: All completed story Interfaces
- Produces: Updated API docs, README

- [ ] TXXX.1 Update documentation to reflect implemented features
- [ ] TXXX.2 Verify all code examples in docs work
- [ ] TXXX.3 Checkpoint: 确认测试通过，保存进度

### TXXX Performance optimization

**Files:**
- Modify: files identified by profiling

**Interfaces:**
- Consumes: Existing Interfaces (no signature changes)
- Produces: Same Interfaces, improved performance

- [ ] TXXX.1 Profile and identify bottlenecks
- [ ] TXXX.2 Write benchmark test
- [ ] TXXX.3 Run benchmark → Record baseline
- [ ] TXXX.4 Implement optimization
- [ ] TXXX.5 Run benchmark → Confirm improvement
- [ ] TXXX.6 Run full test suite → Expected: all PASS (no regressions)
- [ ] TXXX.7 Checkpoint: 确认测试通过，保存进度

**Review Gate**: All polish tasks complete, full test suite passes, documentation accurate.

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel (if staffed)
  - Or sequentially in priority order (P1 → P2 → P3)
- **Polish (Final Phase)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) - No dependencies on other stories
- **User Story 2 (P2)**: Can start after Foundational (Phase 2) - May integrate with US1 but should be independently testable
- **User Story 3 (P3)**: Can start after Foundational (Phase 2) - May integrate with US1/US2 but should be independently testable

### Within Each Task

- Write test FIRST, verify it FAILS
- Implement minimal code to pass the test
- Verify test PASSES
- Save progress atomically after each task passes
- Do not proceed to next task until current task's test passes

### Parallel Opportunities

- All Setup tasks marked [P] can run in parallel
- All Foundational tasks marked [P] can run in parallel (within Phase 2)
- Once Foundational phase completes, all user stories can start in parallel (if team capacity allows)
- Models within a story marked [P] can run in parallel
- Different user stories can be worked on in parallel by different team members

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL - blocks all stories)
3. Complete Phase 3: User Story 1
4. **Review Gate**: Test User Story 1 independently, verify all Interfaces
5. Deploy/demo if ready

### Incremental Delivery

1. Complete Setup + Foundational → Foundation ready
2. Add User Story 1 → Review Gate → Deploy/Demo (MVP!)
3. Add User Story 2 → Review Gate → Deploy/Demo
4. Add User Story 3 → Review Gate → Deploy/Demo
5. Each story adds value without breaking previous stories

### Parallel Team Strategy

With multiple developers:

1. Team completes Setup + Foundational together
2. Once Foundational is done:
   - Developer A: User Story 1
   - Developer B: User Story 2
   - Developer C: User Story 3
3. Stories complete and integrate independently
4. Each developer runs Review Gate before merging

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- Each user story should be independently completable and testable
- TDD micro-steps are mandatory: Red → Green → Checkpoint per task
- Interfaces declarations must be precise (function signatures + types)
- Review Gate at each Phase end validates Interface consistency and test coverage
- Stop at any checkpoint to validate story independently
- Avoid: vague tasks, placeholders, same file conflicts, cross-story dependencies that break independence
