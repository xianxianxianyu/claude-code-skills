---
id: L01
name: TaskDecomposition
version: 1.0
applies_to:
  agents: [sdd-strategic-planner]
  modes: [speckit, openspec]
inputs: [spec_or_proposal, decisions]
outputs: [task_list_Txxx]
---
# TaskDecomposition

## Purpose
拆成可执行、可验收任务（T-xxx）。

## Each task must include
- Goal
- Scope（文件/模块）
- Acceptance（关联 AC-xxx）
- Evidence expectation（最小验证）

## Quality Bar
- 任务太大就再拆；目标是可并发与可回滚。
