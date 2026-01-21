---
id: C05
name: EvidenceCapture
version: 1.0
applies_to:
  agents: [all]
  modes: [speckit, openspec]
inputs: [ARTIFACT_ROOT, commands, results_summary]
outputs: [evidence_file, context_updated]
---
# EvidenceCapture

## Purpose
把“我验证过了”变成可复盘证据（命令 + 结果摘要），并写入 `evidence/`。

## Procedure
1) 若 evidence 文件不存在：从 `.claude/templates/common/evidence.md` 创建
2) 写入：
   - Commands Run
   - Results Summary
   - 若失败：Repro + Suspected cause + Suggested fix
3) 更新 `context.md` 的 Evidence 字段（调用 C02）

## Naming
- 实现：`evidence/impl-<slice>-001.md`
- 测试：`evidence/test-001.md`
- 评审：`evidence/review-001.md`（可选）

## Quality Bar
- 回复里只写摘要；长日志落盘到 evidence 文件。
