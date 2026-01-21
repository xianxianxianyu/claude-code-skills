---
id: P04
name: ArtifactGovernance
version: 1.0
applies_to:
  agents: [plan_agent]
  modes: [speckit, openspec]
inputs: [MODE, ARTIFACT_ROOT]
outputs: [artifact_check_report]
---
# ArtifactGovernance

## Purpose
保证工件齐全、结构统一、可追踪（AC/D/T IDs）。

## Checklist (minimum)
- context.md 存在且 Phase 正确
- speckit：spec.md plan.md tasks.md decisions.md slices/ evidence/
- openspec：proposal.md tasks.md decisions.md slices/ evidence/ specs(delta)/
- tasks.md 包含 Ownership Matrix
- 关键引用存在：tasks → AC；决策 D-xxx 可追

## Procedure
1) 扫描 ARTIFACT_ROOT 文件结构
2) 缺失则要求补齐（调用对应 agent）
3) 每次整合后更新 context（C02）

## Output
- missing artifacts list
- broken references list
