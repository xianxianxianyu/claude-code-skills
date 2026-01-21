---
id: C03
name: ArtifactWriteDiscipline
version: 1.0
applies_to:
  agents: [all]
  modes: [speckit, openspec]
inputs: [MODE, ARTIFACT_ROOT]
outputs: [consistent_artifacts]
---
# ArtifactWriteDiscipline

## Purpose
用模板生成/维护工件，保证结构一致、可审阅、可追踪。

## Templates (fixed)
- context/evidence：`.claude/templates/common/{context.md,evidence.md}`
- speckit：`.claude/templates/speckit/{spec.md,plan.md,tasks.md,decisions.md,slice.md}`
- openspec：`.claude/templates/openspec/{proposal.md,tasks.md,decisions.md,delta-spec.md,slice.md}`

## Procedure
1) 新建 WI 工件时：先复制对应模板到 ARTIFACT_ROOT
2) 工件内使用 ID：
   - AC-001…（验收）
   - D-001…（决策）
   - T-001…（任务）
3) 每写完一个核心工件：立刻调用 C02 更新 context.md（指向最新工件）

## Postconditions
- spec/proposal/plan/tasks/decisions/slices/evidence 结构统一

## Quality Bar
- 不要把“聊天内容”当工件；工件必须落盘且可 review。
