---
id: C06
name: EscalateAndStop
version: 1.0
applies_to:
  agents: [all]
  modes: [speckit, openspec]
inputs: [blocker_reason, needed_action, affected_paths]
outputs: [blocker_report, context_updated]
---
# EscalateAndStop

## Purpose
遇到越界/矛盾/阻塞时停止错误推进，保护流程一致性与并发安全。

## Trigger Conditions
- 需要写入 allowed paths 之外文件（Implementer）
- spec/plan/tasks 互相矛盾或不完整
- 模式/路径混用风险（触发 C04）
- 无法验证且无法提供替代 evidence

## Procedure (output contract)
1) TL;DR（<=5 bullets）
2) Blocker 列表（最多 7 条，每条明确）：
   - 阻塞点是什么
   - 需要谁做什么（Plan Agent/人/其他 agent）
   - 影响哪些文件/模块
3) 更新 `context.md`：
   - Phase 不前进
   - Next 写明“解除阻塞的动作”

## Quality Bar
- 不要硬扛继续写；一旦越界必须停。
