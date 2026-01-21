---
id: D04
name: OpenSpecTruthUpdate
version: 1.0
applies_to:
  agents: [sdd-doc-sync]
  modes: [openspec]
inputs: [change_delta_specs, final_behavior]
outputs: [truth_update_plan]
---
# OpenSpecTruthUpdate

## Purpose
确保最终行为反映到真相库：`.claude/moyu/openspec/specs/**`

## Output
- which truth specs to update
- how delta maps to truth
- archive suggestion (optional)
