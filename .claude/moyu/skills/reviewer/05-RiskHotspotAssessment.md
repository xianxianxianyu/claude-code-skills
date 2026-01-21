---
id: R05
name: RiskHotspotAssessment
version: 1.0
applies_to:
  agents: [sdd-code-reviewer]
  modes: [speckit, openspec]
inputs: [diff, touched_modules]
outputs: [top_risks, targeted_tests]
---
# RiskHotspotAssessment

## Purpose
指出最可能回归的点，并给 targeted tests 建议。

## Output
- Top 3 hotspots (path/function)
- targeted tests suggestions
