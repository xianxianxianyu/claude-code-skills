---
id: T04
name: RunTestsAndCaptureEvidence
version: 1.0
applies_to:
  agents: [sdd-test-runner]
  modes: [speckit, openspec]
inputs: [commands, results]
outputs: [evidence_file, context_updated]
---
# RunTestsAndCaptureEvidence

## Purpose
跑测试并写 evidence（C05），保证可复盘。

## Output
- evidence/test-001.md
- context.md Evidence updated
