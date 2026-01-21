---
id: D05
name: DocQualityChecklist
version: 1.0
applies_to:
  agents: [sdd-doc-sync]
  modes: [speckit, openspec]
inputs: [docs_changes]
outputs: [quality_notes]
---
# DocQualityChecklist

## Purpose
保证文档可复制粘贴、可执行、可维护。

## Checklist
- commands runnable
- examples minimal
- boundaries clear
- no new requirements introduced
