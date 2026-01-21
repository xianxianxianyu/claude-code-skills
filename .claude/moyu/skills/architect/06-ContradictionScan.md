---
id: A06
name: ContradictionScan
version: 1.0
applies_to:
  agents: [sdd-architect]
  modes: [speckit, openspec]
inputs: [new_spec_or_proposal, existing_arch_docs_optional]
outputs: [conflict_list]
---
# ContradictionScan

## Purpose
提前找出与现有规范/架构/真相库冲突的点，降低返工。

## Procedure
1) 对照现有 docs/ 或 openspec/specs（按需最小读取）
2) 输出冲突清单（<=7）：
   - 冲突点
   - 为什么冲突
   - 建议的澄清方向（不做实现）

## Quality Bar
- 冲突必须具体到模块/规则，不要泛泛而谈。
