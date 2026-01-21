# Moyu SDD Skills Library

这个目录是 **“一个 skill 一个文件”** 的技能库，供：
- Plan Agent（主对话/编排器）
- 7 个 Worker Subagents（architect/feasibility/planner/implementer/reviewer/tester/docsync）

## 关键路径（硬规则）
- Speckit 事实源：`.claude/moyu/specs/<WI>/`
- OpenSpec 变更隔离：`.claude/moyu/openspec/changes/<WI>/`
- OpenSpec 真相库：`.claude/moyu/openspec/specs/**`
- Dev docs：`.claude/moyu/docs/**`
- Templates（不在 moyu 内）：`.claude/templates/**`
- Specify scaffolding（在 moyu 内）：`.claude/moyu/.specify/**`

## 如何用（建议）
- 每个 subagent 在开始时先读：
  1) `skills/common/*`
  2) 自己角色目录（如 `skills/architect/*`）
- Plan Agent（主对话）读：
  1) `skills/common/*`
  2) `skills/plan/*`

## Manifest
见 `skills/manifest.yaml`：Agent → Skills 的映射（可用于自动加载/路由）。
