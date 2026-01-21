---
id: T03
name: TestScopeSelection
version: 1.0
applies_to:
  agents: [sdd-test-runner]
  modes: [speckit, openspec]
inputs: [changed_modules]
outputs: [selected_test_commands]
---
# TestScopeSelection

## Purpose
控制成本：先小后大，先子集再全量。

## Strategy
1) run module/package subset
2) expand only if needed
3) always provide minimal regression command
