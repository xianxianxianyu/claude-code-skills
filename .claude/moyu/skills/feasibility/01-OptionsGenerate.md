---
id: F01
name: OptionsGenerate
version: 1.0
applies_to:
  agents: [sdd-feasibility-analyst]
  modes: [speckit, openspec]
inputs: [spec_or_proposal, constraints]
outputs: [Option_A, Option_B, optional_C]
---
# OptionsGenerate

## Purpose
给出 >=2 套可行方案（必须含最小改动方案）。

## Each option must include
- scope impact（模块/文件）
- risk（回归点）
- testability（UT 难度）
- compatibility/perf impact（如有）

## Quality Bar
- 不给“只有一个方案”的结论。
