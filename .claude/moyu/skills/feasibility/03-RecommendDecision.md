---
id: F03
name: RecommendDecision
version: 1.0
applies_to:
  agents: [sdd-feasibility-analyst]
  modes: [speckit, openspec]
inputs: [options, tradeoff_matrix]
outputs: [recommended_option, rationale, non_selected_reasons]
---
# RecommendDecision

## Purpose
明确推荐方案，并说明为什么不选其它方案。

## Output
- Recommended: Option X
- Why (<=5 bullets)
- Not chosen: Option Y/Z (each <=2 bullets)
