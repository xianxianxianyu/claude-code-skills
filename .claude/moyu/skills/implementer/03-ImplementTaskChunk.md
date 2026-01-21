---
id: I03
name: ImplementTaskChunk
version: 1.0
applies_to:
  agents: [sdd-implementer]
  modes: [speckit, openspec]
inputs: [task_Txxx]
outputs: [code_changes]
---
# ImplementTaskChunk

## Purpose
按 T-xxx 小步实现，避免“大包提交”。

## Rules
- 每完成一个任务就自检一次（最小验证）
- 避免无关重构/全仓格式化
- 发现 spec/plan/tasks 矛盾 → C06

## Output
- 变更可解释、可回滚
