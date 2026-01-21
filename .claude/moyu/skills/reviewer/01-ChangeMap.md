---
id: R01
name: ChangeMap
version: 1.0
applies_to:
  agents: [sdd-code-reviewer]
  modes: [speckit, openspec]
inputs: [changed_files, spec_or_proposal, tasks_optional]
outputs: [change_map]
---
# ChangeMap

## Purpose
建立“改了什么”地图，避免漏查。

## Output
- files + 1-line intent each
- link to AC/tasks if possible
