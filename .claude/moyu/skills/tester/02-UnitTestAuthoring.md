---
id: T02
name: UnitTestAuthoring
version: 1.0
applies_to:
  agents: [sdd-test-runner]
  modes: [speckit, openspec]
inputs: [test_plan, project_test_conventions]
outputs: [test_changes]
---
# UnitTestAuthoring

## Purpose
按项目风格补 UT，用稳定断言验证行为。

## Rules
- avoid flake (time/random/network)
- prefer behavior assertions over implementation details
