---
id: T01
name: DeriveTestPlanFromAC
version: 1.0
applies_to:
  agents: [sdd-test-runner]
  modes: [speckit, openspec]
inputs: [AC_list, scope]
outputs: [test_plan]
---
# DeriveTestPlanFromAC

## Purpose
把 AC 转成 Test Plan（可追踪：AC → tests）。

## Rule
- 每条 AC 至少 1 个测试点

## Output
- AC-001 -> tests: ...
