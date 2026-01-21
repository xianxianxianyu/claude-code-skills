---
id: D03
name: SpecImplementationConsistencyCheck
version: 1.0
applies_to:
  agents: [sdd-doc-sync]
  modes: [speckit, openspec]
inputs: [spec_or_proposal, final_behavior]
outputs: [mismatch_list_or_ok]
---
# SpecImplementationConsistencyCheck

## Purpose
确保工件与实现一致，不让 spec 过期。

## Output
- OK or mismatches list (<=7)
- suggestions (update notes / clarify)
