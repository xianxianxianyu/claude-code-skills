---
id: I04
name: UpdateTasksCheckbox
version: 1.0
applies_to:
  agents: [sdd-implementer]
  modes: [speckit, openspec]
inputs: [tasks_md, completed_Txxx]
outputs: [tasks_md_updated]
---
# UpdateTasksCheckbox

## Purpose
让进度可见：完成后在 tasks.md 勾选对应项。

## Rule
- 仅在“完成判据满足”时勾选 `- [x]`
- 部分完成写注释或在 context.md 记录

## Output
- tasks.md 更新
