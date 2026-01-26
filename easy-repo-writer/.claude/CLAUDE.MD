# Easy Repo Writer

## Goal
- 为任意仓库生成可验证、可维护的文档
- 3-axis 视角：Journey / System / Product

## 入口
- 调用 `/easy-repo-writer` 或直接使用 agents

## 默认输出位置
- 草稿写入 `.claude/moyu/docs/easy-repo-writer/runs/<RUN_ID>/`
- 默认 patch 模式，不修改 repo root

## Subagents 路由索引

| Agent | 触发场景 |
|-------|----------|
| erw-planner | 扫描仓库、生成文档计划、repo profile |
| erw-writer | 根据计划生成文档、README、quickstart、journey、views |
| erw-publisher | QA 检查、生成发布包、link check、patch |

## 关键路径索引

| 用途 | 路径 |
|------|------|
| 运行输出 | `.claude/moyu/docs/easy-repo-writer/runs/<RUN_ID>/` |
| 模板 | `.claude/moyu/templates/easy-repo-writer/` |

## Rules 索引
- `.claude/rules/easy-repo-writer/docs.md`
- `.claude/rules/easy-repo-writer/testing.md`
- `.claude/rules/easy-repo-writer/style.md`
- `.claude/rules/easy-repo-writer/security.md`

## 3-Agent Pipeline

```
erw-planner → erw-writer → erw-publisher
```

1. **erw-planner**: 扫描仓库 → 形成文档计划
2. **erw-writer**: 按计划写文档（多视角）
3. **erw-publisher**: 质量检查 → 输出发布包
