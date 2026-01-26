# SDD 双模式框架

## Goal
- 规格驱动开发：先有可测试的验收标准，再写代码
- 双模式支持：SpecKit（新模块）/ OpenSpec（存量改造）

## 入口
- 启动 WI：`WI-YYYYMMDD-###-slug`
- 选择模式后按流水线执行

## 默认输出位置
- 所有工件先写入 `.claude/moyu/`
- 需用户同意才能修改 repo 根目录

## Subagents 路由索引

| Agent | 触发场景 |
|-------|----------|
| sdd-architect | 需求分析、spec、proposal、需求定义 |
| sdd-feasibility-analyst | feasibility、方案对比、技术选型、风险评估 |
| sdd-strategic-planner | 任务分解、slice、ownership、拆解 |
| sdd-implementer | 实现、编码、slice 执行 |
| sdd-code-reviewer | review、代码审查、QA |
| sdd-test-runner | 测试、UT、验证 |
| sdd-doc-sync | 文档更新、sync docs、CHANGELOG |

## 关键路径索引

| 用途 | 路径 |
|------|------|
| 模板 | `.claude/moyu/templates/**` |
| SpecKit 工件 | `.claude/moyu/specs/<WI>/` |
| OpenSpec 变更 | `.claude/moyu/openspec/changes/<WI>/` |
| OpenSpec 真相库 | `.claude/moyu/openspec/specs/**` |
| 开发文档 | `.claude/moyu/docs/**` |
| 追踪日志 | `.claude/moyu/trace/runs.jsonl` |

## Rules 索引
- `.claude/rules/dual-sdd/docs.md`
- `.claude/rules/dual-sdd/testing.md`
- `.claude/rules/dual-sdd/style.md`
- `.claude/rules/dual-sdd/security.md`
- `.claude/rules/dual-sdd/docs/prd.md`
- `.claude/rules/dual-sdd/docs/feasibility.md`

## 快速开始

### 启动新 Work Item
1. 确定 MODE（speckit 或 openspec）
2. 生成 WI ID：`WI-YYYYMMDD-###-slug`
3. 创建 ARTIFACT_ROOT 目录
4. 按流水线执行：Architect → Feasibility → Planner → Implementer → Reviewer → Tester → DocSync
