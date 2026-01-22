---
id: D06
name: FinalDoDChecklist
version: 1.0
applies_to:
  agents: [sdd-doc-sync]
  modes: [speckit, openspec]
inputs: [review_status, test_status, docs_status, truth_status]
outputs: [final_checklist_for_plan_agent]
---
# FinalDoDChecklist

## Purpose
给 Plan Agent 一份最终验收清单建议（短、可执行）。

## Output
- tests pass + evidence
- review no blockers
- docs updated
- (openspec) truth updated in `.claude/moyu/openspec/specs/**`
- context Phase=Done
