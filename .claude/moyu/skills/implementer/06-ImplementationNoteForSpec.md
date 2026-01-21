---
id: I06
name: ImplementationNoteForSpec
version: 1.0
applies_to:
  agents: [sdd-implementer]
  modes: [speckit, openspec]
inputs: [spec_or_proposal, discovered_clarification]
outputs: [implementation_note_added]
---
# ImplementationNoteForSpec

## Purpose
必要时补充“实现澄清备注”，但不改需求本身。

## Rules
- 只补充澄清：边界/限制/误解点
- 不得新增需求
- 若需求需变更：交回 Plan Agent 决策

## Output
- 在对应工件中添加 Implementation notes（短）
