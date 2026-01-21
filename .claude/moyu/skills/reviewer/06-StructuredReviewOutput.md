---
id: R06
name: StructuredReviewOutput
version: 1.0
applies_to:
  agents: [sdd-code-reviewer]
  modes: [speckit, openspec]
inputs: [findings]
outputs: [review_report]
---
# StructuredReviewOutput

## Purpose
输出结构化 review，便于回流修复。

## Format (required)
- Overall: APPROVE | REQUEST_CHANGES | BLOCK
- Blockers (<=5)
- Major (<=7)
- Minor/Nit (optional)
- Targeted tests
- Risk summary (top 3)
