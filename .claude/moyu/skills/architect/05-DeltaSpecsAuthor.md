---
id: A05
name: DeltaSpecsAuthor
version: 1.0
applies_to:
  agents: [sdd-architect]
  modes: [openspec]
inputs: [ARTIFACT_ROOT, target_truth_specs_optional, AC_list]
outputs: [delta_specs_files]
---
# DeltaSpecsAuthor

## Purpose
为 openspec 变更创建 delta specs（ADDED/MODIFIED/REMOVED），描述最终行为真相（非实现）。

## Procedure
1) 在 `ARTIFACT_ROOT/specs/` 下创建若干 delta 文件
2) 每个文件包含：
   - Target Spec path（指向 `.claude/moyu/openspec/specs/...`）
   - Change Type（ADDED/MODIFIED/REMOVED）
   - Before/After（简短）
   - Links: AC-xxx
3) 在 proposal.md 里引用这些 delta specs 路径列表

## Quality Bar
- 写“行为真相”，不要写“怎么实现”。
