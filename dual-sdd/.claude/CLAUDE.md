# SDD 双模式团队骨架 - 项目配置

> 本文件是项目级配置，补充全局 CLAUDE.md 中的 SDD 框架定义。

---

## Skills 加载规则

### 目录结构
```
.claude/
├── agents/                    # Agent 定义（含 skills 引用）
│   ├── sdd-architect.md
│   ├── sdd-feasibility-analyst.md
│   ├── sdd-strategic-planner.md
│   ├── sdd-implementer.md
│   ├── sdd-code-reviewer.md
│   ├── sdd-test-runner.md
│   └── sdd-doc-sync.md
├── skills/                    # Skill 定义
│   ├── sdd-common/SKILL.md    # 通用技能（路径解析、上下文维护等）
│   ├── sdd-architect/SKILL.md
│   ├── sdd-feasibility/SKILL.md
│   ├── sdd-planner/SKILL.md
│   ├── sdd-implementer/SKILL.md
│   ├── sdd-reviewer/SKILL.md
│   ├── sdd-tester/SKILL.md
│   ├── sdd-docsync/SKILL.md
│   └── sdd-plan/SKILL.md
└── moyu/                      # 工件存储
    ├── specs/                 # SpecKit 工件
    ├── openspec/              # OpenSpec 工件
    │   ├── specs/             # 真相库
    │   └── changes/           # 变更隔离
    ├── templates/             # 模板
    ├── docs/                  # 开发文档
    ├── trace/                 # 追踪日志
    └── .specify/              # Specify 框架
```

### Agent 与 Skill 关联
每个 Agent 通过 frontmatter 中的 `skills` 字段声明依赖的技能：

```yaml
---
name: sdd-architect
skills:
  - sdd-common      # 通用技能
  - sdd-architect   # 专属技能
---
```

### 关键路径（相对路径）
| 用途 | 路径 |
|------|------|
| 模板读取 | `.claude/moyu/templates/**` |
| SpecKit 工件 | `.claude/moyu/specs/<WI>/` |
| OpenSpec 变更 | `.claude/moyu/openspec/changes/<WI>/` |
| OpenSpec 真相库 | `.claude/moyu/openspec/specs/**` |
| 开发文档 | `.claude/moyu/docs/**` |
| 追踪日志 | `.claude/moyu/trace/runs.jsonl` |

---

## Agent 列表

| Agent | 职责 | 工具权限 |
|-------|------|----------|
| sdd-architect | 规格设计（spec/proposal） | Read, Glob, Grep, Write, Edit |
| sdd-feasibility-analyst | 方案对比/决策 | Read, Glob, Grep, Write, Edit |
| sdd-strategic-planner | 任务拆解/切片 | Read, Glob, Grep, Write, Edit |
| sdd-implementer | 代码实现 | Read, Glob, Grep, Write, Edit, Bash |
| sdd-code-reviewer | 代码审查（只读） | Read, Glob, Grep |
| sdd-test-runner | 测试执行 | Read, Glob, Grep, Write, Edit, Bash |
| sdd-doc-sync | 文档同步 | Read, Glob, Grep, Write, Edit |

---

## 快速开始

### 启动新 Work Item
1. 确定 MODE（speckit 或 openspec）
2. 生成 WI ID：`WI-YYYYMMDD-###-slug`
3. 创建 ARTIFACT_ROOT 目录
4. 按流水线执行：Architect → Feasibility → Planner → Implementer → Reviewer → Tester → DocSync
