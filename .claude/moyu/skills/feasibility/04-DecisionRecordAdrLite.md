---
id: F04
name: DecisionRecordAdrLite
version: 1.0
applies_to:
  agents: [sdd-feasibility-analyst]
  modes: [speckit, openspec]
inputs: [MODE, ARTIFACT_ROOT, decision]
outputs: [decisions_md_updated]
---
# DecisionRecordAdrLite

## Purpose
把决策写进 `decisions.md`（D-xxx），方便回溯。

## Paths
- speckit：`.claude/moyu/specs/<WI>/decisions.md`
- openspec：`.claude/moyu/openspec/changes/<WI>/decisions.md`

## Required fields
- Context
- Options considered
- Decision
- Why
- Consequences
- Rollback
