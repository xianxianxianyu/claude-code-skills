---
id: L04
name: SliceFileGenerate
version: 1.0
applies_to:
  agents: [sdd-strategic-planner]
  modes: [speckit, openspec]
inputs: [ARTIFACT_ROOT, ownership_matrix, task_list]
outputs: [slice_md_files]
---
# SliceFileGenerate

## Purpose
为每个 slice 生成 `slices/slice-*.md`（1页实现合同）。

## Must include
- Slice ID
- Covered tasks（T-xxx）
- Allowed paths（touch list）
- Minimal validation suggestion
- Evidence naming suggestion

## Templates
- speckit slice：`.claude/templates/speckit/slice.md`
- openspec slice：`.claude/templates/openspec/slice.md`
