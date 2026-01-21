---
id: R02
name: SpecToCodeVerification
version: 1.0
applies_to:
  agents: [sdd-code-reviewer]
  modes: [speckit, openspec]
inputs: [AC_list, implementation_diff]
outputs: [AC_coverage_review]
---
# SpecToCodeVerification

## Purpose
逐条对齐 AC：是否满足、证据是什么、缺口是什么。

## Output
- AC-001: PASS/FAIL (where/why)
- AC-002: ...

## Quality Bar
- 缺口要落到 Blocker/Major。
