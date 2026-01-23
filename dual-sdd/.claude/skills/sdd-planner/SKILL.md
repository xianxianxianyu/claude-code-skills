---
description: SDD Strategic Planner 技能集 - 任务拆解、切片规划、所有权矩阵
user-invocable: false
disable-model-invocation: true
---

# SDD Strategic Planner Skills

## P01: TaskDecomposition
### Purpose
将规格拆解为可执行的任务列表

### Rules
1. 每个任务必须可独立验收
2. 任务粒度：1-4 小时工作量
3. 任务之间依赖关系清晰
4. 避免循环依赖

### Output Format
```markdown
## Task: T-<number>
### Objective
<what_to_achieve>

### Scope
- Files: <file_list>
- Functions: <function_list>

### Acceptance
<how_to_verify>

### Dependencies
- Blocked by: <task_ids>
- Blocks: <task_ids>
```

---

## P02: OwnershipMatrix
### Purpose
定义文件/模块的所有权，避免并发冲突

### Rules
1. 每个文件只能属于一个 slice
2. 公共文件需要特殊标记和协调
3. 接口文件优先处理
4. 矩阵必须放在 tasks.md 顶部

### Output Format
```markdown
## Ownership Matrix

| File/Module | Owner (Slice) | Priority | Notes |
|-------------|---------------|----------|-------|
| src/api/auth.ts | slice-1 | P0 | Interface |
| src/services/user.ts | slice-2 | P1 | |
| src/utils/common.ts | SHARED | P0 | Coordinate |
```

---

## P03: SliceDefinition
### Purpose
定义实现切片，支持并发开发

### Rules
1. 每个 slice 有独立的 allowed paths
2. slice 之间不应有文件重叠
3. 先接口后实现的顺序
4. slice 文件位置：ARTIFACT_ROOT/slices/

### Output Format
```markdown
# Slice: <slice_id>

## Scope
<brief_description>

## Allowed Paths
- src/module-a/**
- src/module-b/specific.ts

## Tasks
- T-1: <task_summary>
- T-2: <task_summary>

## Dependencies
- Requires: <other_slices>
- Enables: <other_slices>

## Touch List
<files_to_modify>
```

---

## P04: DependencyGraph
### Purpose
构建任务/切片依赖图

### Rules
1. 识别关键路径
2. 标记可并行的任务
3. 检测循环依赖
4. 优化执行顺序

### Output Format
```markdown
## Dependency Graph

```
T-1 (Interface) ─┬─> T-2 (Impl A)
                 └─> T-3 (Impl B) ─> T-4 (Integration)
```

### Critical Path
T-1 -> T-3 -> T-4

### Parallelizable
- T-2 and T-3 can run in parallel
```

---

## P05: TasksDocWriting
### Purpose
编写 tasks.md 文档

### Rules
1. 位置：ARTIFACT_ROOT/tasks.md
2. 顶部必须有 Ownership Matrix
3. 每个任务有完整定义
4. 包含进度追踪标记

### Template
```markdown
# Tasks: <WI>

## Ownership Matrix
<matrix>

## Task List

### T-1: <title>
- [ ] Status: pending
- Objective: <objective>
- Scope: <scope>
- Acceptance: <criteria>
- Assigned: <slice_id>

### T-2: <title>
...
```

---

## P06: PlanValidation
### Purpose
验证计划完整性

### Checklist
- [ ] 所有规格需求都有对应任务
- [ ] 任务粒度合理
- [ ] 依赖关系无循环
- [ ] Ownership Matrix 完整
- [ ] 切片边界清晰
- [ ] 关键路径已识别
