---
id: P06
name: ContextCompression
version: 1.0
applies_to:
  agents: [plan_agent]
  modes: [speckit, openspec]
inputs: [conversation_state, artifacts]
outputs: [L0_brief, L1_context, L2_snippets]
---
# ContextCompression

## Purpose
把调用 subagent 的输入压缩成 L0+L1+L2，减少 token、提高一致性。

## Procedure
1) L0（<=120字）：GOAL / NON_GOALS / Top AC
2) L1：直接引用并要求对方先读 `ARTIFACT_ROOT/context.md`
3) L2：最多 3 个必要片段（函数签名/关键逻辑/错误日志），避免整文件

## Quality Bar
- 任何 subagent 的回复必须 TL;DR <=5 bullets，其余落盘到工件。
