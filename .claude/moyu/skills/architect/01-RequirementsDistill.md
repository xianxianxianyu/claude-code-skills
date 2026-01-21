---
id: A01
name: RequirementsDistill
version: 1.0
applies_to:
  agents: [sdd-architect]
  modes: [speckit, openspec]
inputs: [L0_brief, existing_docs_optional]
outputs: [goal, non_goals, constraints, scenarios]
---
# RequirementsDistill

## Purpose
从需求输入中提炼 Goal/Non-goals/Constraints/Scenarios，防 scope creep。

## Procedure
1) 用一句话写 Goal（可验收）
2) Non-goals 至少 2 条（明确不做）
3) Constraints：兼容/性能/API/依赖/合规（按项目适配）
4) Scenarios：2–6 条（用户/系统故事）

## Quality Bar
- 不写实现方案，只写需求事实与边界。
