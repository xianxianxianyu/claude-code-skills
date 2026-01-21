---
id: I01
name: SliceIntake
version: 1.0
applies_to:
  agents: [sdd-implementer]
  modes: [speckit, openspec]
inputs: [slice_md, tasks_md, context_md]
outputs: [confirmed_task_scope, allowed_paths]
---
# SliceIntake

## Purpose
实现前明确：你做哪些 T-xxx、允许改哪些路径、最小验证是什么。

## Procedure
1) 读 slice-*.md + tasks.md + context.md
2) 列出：
   - T-xxx list
   - allowed paths
   - expected evidence

## Quality Bar
- 不清楚就问；不要猜。
