---
id: C04
name: SingleSourceGuard
version: 1.0
applies_to:
  agents: [all]
  modes: [speckit, openspec]
inputs: [MODE, WORK_ITEM, intended_write_paths]
outputs: [allow_or_block_with_reason]
---
# SingleSourceGuard

## Purpose
防止“同一 WI 混用 speckit/openspec 工件系统”与“写错目录”。

## Rules
- 所有写入必须在 `.claude/moyu/` 下
- speckit（同一 WI）禁止写：
  - `.claude/moyu/openspec/changes/<WI>/`
- openspec（同一 WI）禁止写：
  - `.claude/moyu/specs/<WI>/`
- openspec 最终真相必须落到：
  - `.claude/moyu/openspec/specs/**`

## Procedure
1) 对 intended_write_paths 做前缀匹配校验
2) 如触发禁区：阻断并要求 Escalate（C06）

## Quality Bar
- 宁可阻断，也不要“悄悄写错地方”造成后续打架。
