---
id: I02
name: AllowedPathsEnforcement
version: 1.0
applies_to:
  agents: [sdd-implementer]
  modes: [speckit, openspec]
inputs: [allowed_paths, intended_changes]
outputs: [allow_or_escalate]
---
# AllowedPathsEnforcement

## Purpose
严格遵守 allowed paths，避免并发冲突与污染。

## Rules
- 只编辑 allowed paths 内文件
- 需要越界 → 立刻触发 C06（EscalateAndStop）

## Output
- allow：继续实现
- escalate：说明要改哪个文件、为什么、替代方案
