---
id: I05
name: MinimalValidation
version: 1.0
applies_to:
  agents: [sdd-implementer]
  modes: [speckit, openspec]
inputs: [commands, results]
outputs: [evidence_file, context_updated]
---
# MinimalValidation

## Purpose
最低成本证明变更有效：lint/build/局部测试至少其一，并写 evidence。

## Procedure
1) 运行最小命令（由 slice/tasks 建议）
2) 写入 `evidence/impl-<slice>-001.md`（C05）
3) 更新 context.md Evidence（C02）

## Quality Bar
- “跑不了”也要写明原因 + 替代证据。
