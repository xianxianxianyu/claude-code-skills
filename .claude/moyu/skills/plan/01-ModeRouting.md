---
id: P01
name: ModeRouting
version: 1.0
applies_to:
  agents: [plan_agent]
  modes: [speckit, openspec]
inputs: [goal, scope, existing_code_context, audit_need]
outputs: [MODE, ARTIFACT_ROOT, rationale]
---
# ModeRouting

## Purpose
为每个 WI 选择 speckit 或 openspec，确保“单一事实源”。

## Heuristics
- speckit 优先：0→1 新模块/新子系统/需要线性治理
- openspec 优先：存量迭代/跨模块/强审计/需隔离提案与归档

## Procedure
1) 判断 greenfield vs brownfield
2) 判断是否需要变更隔离与强审计（是→openspec）
3) 输出：
   - MODE
   - ARTIFACT_ROOT（必须在 `.claude/moyu/`）
   - 选择理由（3 条内）

## Postconditions
- Plan Agent 在 WI Brief 中固定 MODE 与 ARTIFACT_ROOT（后续不可随意改）
