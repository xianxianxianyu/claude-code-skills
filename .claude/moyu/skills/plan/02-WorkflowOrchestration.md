---
id: P02
name: WorkflowOrchestration
version: 1.0
applies_to:
  agents: [plan_agent]
  modes: [speckit, openspec]
inputs: [MODE, ARTIFACT_ROOT, current_phase]
outputs: [next_phase, assigned_agents, gates]
---
# WorkflowOrchestration

## Purpose
驱动状态机：Spec → Plan → Tasks → Implement → Review → Test → Doc → Done

## Gates (minimum)
- Spec Ready：spec/proposal + AC + context
- Decision Ready：decisions + plan/decision + rollback
- Tasks Ready：tasks + Ownership Matrix + slices
- Implement Ready：tasks 勾选 + evidence
- Review Pass：无 blocker
- Tests Pass：UT/关键回归 + evidence
- Doc Closed：docs 更新 + truth updated

## Procedure
1) 基于 current_phase 检查必需工件
2) 仅在 Gate 满足后推进 phase
3) 每次 phase 变化更新 context（调用 C02）

## Output
- next_phase
- 需要调用的 agent 列表（含输入：L0/L1/L2）
