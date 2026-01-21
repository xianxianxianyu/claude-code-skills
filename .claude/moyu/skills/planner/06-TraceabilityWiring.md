---
id: L06
name: TraceabilityWiring
version: 1.0
applies_to:
  agents: [sdd-strategic-planner]
  modes: [speckit, openspec]
inputs: [AC_list, decisions, tasks]
outputs: [traceable_links]
---
# TraceabilityWiring

## Purpose
把 AC / Decision / Tasks 串起来，便于 review 与测试。

## Rules
- 每个 task 必须引用至少一个 AC（AC-xxx）
- 关键任务可引用决策（D-xxx）
- 保证每条 AC 至少对应 1 个 task（供 tester 使用）

## Output
- 更新 tasks.md（补充 references）
