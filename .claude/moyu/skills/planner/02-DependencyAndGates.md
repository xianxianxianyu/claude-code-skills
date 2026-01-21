---
id: L02
name: DependencyAndGates
version: 1.0
applies_to:
  agents: [sdd-strategic-planner]
  modes: [speckit, openspec]
inputs: [task_list]
outputs: [serial_gates]
---
# DependencyAndGates

## Purpose
识别必须串行的门禁点，避免并发踩踏。

## Output
- Gate 1: interface/types ready
- Gate 2: callers migrated
- Gate 3: cleanup/docs

## Quality Bar
- 每个 gate 都要有完成判据（可验证）。
