---
id: A04
name: ProposalDraftOpenSpec
version: 1.0
applies_to:
  agents: [sdd-architect]
  modes: [openspec]
inputs: [ARTIFACT_ROOT, why, what, scope, AC_list]
outputs: [proposal_md, context_updated]
---
# ProposalDraftOpenSpec

## Purpose
在 openspec 模式产出 `.claude/moyu/openspec/changes/<WI>/proposal.md`（WHY/WHAT/AC）。

## Procedure
1) 从模板初始化（如缺失）：
   - `.claude/moyu/templates/openspec/proposal.md` → `ARTIFACT_ROOT/proposal.md`
2) 填入 Why/What/In-Scope/Out-of-Scope/AC
3) 指向 delta specs 路径：`ARTIFACT_ROOT/specs/**`
4) 更新 `context.md`（Phase=Spec）（C02）

## Quality Bar
- proposal 必须能独立说明动机与边界。
