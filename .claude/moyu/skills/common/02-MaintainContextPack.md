---
id: C02
name: MaintainContextPack
version: 1.0
applies_to:
  agents: [all]
  modes: [speckit, openspec]
inputs: [ARTIFACT_ROOT, latest_artifacts, latest_evidence]
outputs: [updated_context_md]
---
# MaintainContextPack

## Purpose
把长对话/复杂状态压缩到 `context.md`（一页真相），降低 token 并让协作可见。

## Preconditions
- ARTIFACT_ROOT 已通过 C01 校验
- `context.md` 存在（若不存在先从 `.claude/templates/common/context.md` 初始化）

## Procedure
1) 读取现有 `ARTIFACT_ROOT/context.md`
2) 更新以下字段（保持短）：
   - Phase：Spec | Plan | Tasks | Implement | Review | Test | Doc | Done
   - Key Decisions：引用 D-xxx
   - Touch List：预计/已改文件（路径即可）
   - Evidence：最新 evidence 文件名
   - Next：下一步应调用的 agent
3) 控制长度：尽量 <= 400 中文字（删冗余保关键）

## Postconditions
- `context.md` 更新，能作为 L1 上下文被复用

## Quality Bar
- context 必须可独立理解，不依赖聊天历史。
