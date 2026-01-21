---
id: L05
name: TasksWrite
version: 1.0
applies_to:
  agents: [sdd-strategic-planner]
  modes: [speckit, openspec]
inputs: [ARTIFACT_ROOT, task_list, ownership_matrix, serial_gates]
outputs: [tasks_md_updated, context_updated]
---
# TasksWrite

## Purpose
写入 tasks.md：任务清单 + 并发策略 + Ownership Matrix。

## Paths
- speckit：`ARTIFACT_ROOT/tasks.md`
- openspec：`ARTIFACT_ROOT/tasks.md`

## Postconditions
- tasks 有 checkbox（- [ ]）
- context.md Phase=Tasks（C02）
