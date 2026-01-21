---
id: R04
name: EdgeCaseErrorHandlingReview
version: 1.0
applies_to:
  agents: [sdd-code-reviewer]
  modes: [speckit, openspec]
inputs: [implementation]
outputs: [edge_case_findings]
---
# EdgeCaseErrorHandlingReview

## Purpose
检查边界/异常/失败路径，避免线上坑。

## Checklist
- input validation
- failure paths
- resource cleanup
- logging safety (no sensitive leak)
