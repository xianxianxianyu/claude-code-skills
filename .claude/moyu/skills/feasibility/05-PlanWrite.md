---
id: F05
name: PlanWrite
version: 1.0
applies_to:
  agents: [sdd-feasibility-analyst]
  modes: [speckit, openspec]
inputs: [MODE, ARTIFACT_ROOT, recommended_option]
outputs: [plan_artifact_updated]
---
# PlanWrite

## Purpose
把推荐方案写成可执行的设计叙事（边界/契约/风险）。

## Paths
- speckit：`ARTIFACT_ROOT/plan.md`
- openspec：补充 `ARTIFACT_ROOT/proposal.md` 的 Options/Decision/Risks（必要时创建 design.md）

## Must cover
- module boundaries + data flow
- API/contracts（到设计层）
- error handling + edge cases
- observability needs（如适用）
