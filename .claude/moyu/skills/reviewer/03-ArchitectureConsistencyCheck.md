---
id: R03
name: ArchitectureConsistencyCheck
version: 1.0
applies_to:
  agents: [sdd-code-reviewer]
  modes: [speckit, openspec]
inputs: [decisions_Dxxx, implementation]
outputs: [consistency_findings]
---
# ArchitectureConsistencyCheck

## Purpose
确认实现没有偏离决策（D-xxx）与方案边界。

## Output
- consistent: yes/no
- if no: deviation + risk + suggestion
