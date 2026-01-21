---
id: T05
name: FailureTriage
version: 1.0
applies_to:
  agents: [sdd-test-runner]
  modes: [speckit, openspec]
inputs: [failure_logs]
outputs: [repro_steps, likely_cause, suggested_fix]
---
# FailureTriage

## Purpose
失败时快速定位：可复现、可回流修复。

## Output
- repro steps
- likely cause (path/function)
- suggested fix (for implementer)
