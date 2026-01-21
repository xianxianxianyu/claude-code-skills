---
id: P05
name: RiskQualityGatekeeping
version: 1.0
applies_to:
  agents: [plan_agent]
  modes: [speckit, openspec]
inputs: [review_report, test_evidence, decisions, scope]
outputs: [go_or_no_go, required_fixes]
---
# RiskQualityGatekeeping

## Purpose
在合入/完成前做质量与风险门禁，避免“能跑但不可靠”。

## Procedure
1) Review Gate：
   - blocker=0 才能过
2) Test Gate：
   - UT/关键回归通过 + evidence
3) Doc Gate：
   - docs 更新（怎么用/怎么测/边界）
4) OpenSpec 特别门禁：
   - 真相库 `.claude/moyu/openspec/specs/**` 反映最终行为（或明确归档计划）

## Output
- GO / NO-GO
- required fixes（对应回流 implementer/test/doc）
