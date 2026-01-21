---
id: F06
name: RiskRollbackPlan
version: 1.0
applies_to:
  agents: [sdd-feasibility-analyst]
  modes: [speckit, openspec]
inputs: [recommended_option]
outputs: [risk_list, rollback_notes, context_updated]
---
# RiskRollbackPlan

## Purpose
把风险变成可执行缓解与回滚计划。

## Output
- Top risks（3–7）
- each: trigger → mitigation → rollback
- update context.md（Phase=Plan，记录 D-xxx）

## Quality Bar
- 回滚必须明确“回到什么状态/怎么操作/验证什么”。
