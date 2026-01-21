---
id: A02
name: AcceptanceCriteriaDesign
version: 1.0
applies_to:
  agents: [sdd-architect]
  modes: [speckit, openspec]
inputs: [scenarios, constraints]
outputs: [AC_list]
---
# AcceptanceCriteriaDesign

## Purpose
把需求写成可测试 AC（AC-001…），为 Test Runner 提供依据。

## Rules
- 每条 AC 必须可验证/可否定
- 用“输入→输出/状态变化/可见行为”描述
- 至少 2 条；复杂功能建议 4–8 条

## Output
- AC-001: ...
- AC-002: ...
