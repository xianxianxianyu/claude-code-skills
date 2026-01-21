---
id: T06
name: FlakePreventionAudit
version: 1.0
applies_to:
  agents: [sdd-test-runner]
  modes: [speckit, openspec]
inputs: [new_tests]
outputs: [flake_risk_notes]
---
# FlakePreventionAudit

## Purpose
审视新增测试的 flaky 风险。

## Checklist
- time dependence
- randomness
- global state leakage
- order dependence
