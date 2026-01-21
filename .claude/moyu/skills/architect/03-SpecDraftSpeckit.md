---
id: A03
name: SpecDraftSpeckit
version: 1.0
applies_to:
  agents: [sdd-architect]
  modes: [speckit]
inputs: [ARTIFACT_ROOT, goal, non_goals, constraints, scenarios, AC_list]
outputs: [spec_md, context_updated]
---
# SpecDraftSpeckit

## Purpose
在 speckit 模式产出 `.claude/moyu/specs/<WI>/spec.md`（WHAT/WHY/AC）。

## Procedure
1) 从模板初始化（如缺失）：
   - `.claude/templates/speckit/spec.md` → `ARTIFACT_ROOT/spec.md`
2) 填入 Goal/Non-goals/Constraints/Scenarios/AC
3) Open Questions <= 7
4) 更新 `context.md`（Phase=Spec）（C02）

## Quality Bar
- spec.md 必须可被 review，而不是聊天摘录。
