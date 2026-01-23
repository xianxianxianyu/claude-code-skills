# Moyu 双 SDD 骨架（SpecKit / OpenSpec）

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

英文版：[`README.md`](README.md)

这个仓库是一套「双 SDD」工作流骨架（SpecKit / OpenSpec），用于在 Claude Code 中把"规格 → 计划 → 任务 → 实现 → 验证 → 文档"落到可审计、可复用、路径稳定的工件上。

设计目标：所有 SDD 工件都落在 `.claude/moyu/` 下，repo 根目录保持干净。

## 特性

- 双模式 SDD：按 Work Item（WI）选择 SpecKit 或 OpenSpec
- 单一事实源：每个 WI 只能选一种模式作为事实源
- 标准 Claude Code 结构：agents 在 `.claude/agents/`，skills 在 `.claude/skills/`
- 工件路径确定：`context/spec/tasks/evidence` 位置固定
- Agent-Skill 映射：通过 frontmatter `skills:` 字段声明
- 可选可观测性：TRACE Envelope

## 目录结构

```text
.
├── CLAUDE.md                               # 全局 Plan Agent 手册（用户 ~/.claude/）
├── README.md                               # 英文 README
├── README.zh-CN.md                         # 中文 README
├── LICENSE                                 # MIT
└── .claude/                                # Claude Code 集成根目录
    ├── CLAUDE.md                           # 项目级配置 + skills 加载规则
    ├── agents/                             # Agent 定义（完整定义，非 shim）
    │   ├── sdd-architect.md                # 规格设计
    │   ├── sdd-feasibility-analyst.md      # 方案对比/决策
    │   ├── sdd-strategic-planner.md        # 任务拆解/切片
    │   ├── sdd-implementer.md              # 代码实现
    │   ├── sdd-code-reviewer.md            # 代码审查（只读）
    │   ├── sdd-test-runner.md              # 测试执行
    │   └── sdd-doc-sync.md                 # 文档同步
    ├── skills/                             # Skill 定义
    │   ├── sdd-common/SKILL.md             # 通用技能（路径、上下文、工件）
    │   ├── sdd-architect/SKILL.md          # Architect 专属技能
    │   ├── sdd-feasibility/SKILL.md        # 可行性分析技能
    │   ├── sdd-planner/SKILL.md            # 规划/切片技能
    │   ├── sdd-implementer/SKILL.md        # 实现技能
    │   ├── sdd-reviewer/SKILL.md           # 代码审查技能
    │   ├── sdd-tester/SKILL.md             # 测试技能
    │   ├── sdd-docsync/SKILL.md            # 文档同步技能
    │   └── sdd-plan/SKILL.md               # Plan Agent 编排技能
    └── moyu/                               # 工件存储（干净分离）
        ├── specs/                          # SpecKit 工件：.claude/moyu/specs/<WI>/
        ├── openspec/                       # OpenSpec 系统
        │   ├── changes/                    # 变更隔离：.claude/moyu/openspec/changes/<WI>/
        │   └── specs/                      # 真相库（必须反映最终行为）
        ├── templates/                      # 模板
        ├── docs/                           # 开发文档
        ├── trace/                          # 追踪日志：runs.jsonl
        └── .specify/                       # Specify 框架
```

## 安装

### 方式一：全局安装（推荐）

```bash
# 克隆本仓库
git clone https://github.com/your-username/claude-code-skills.git
cd claude-code-skills

# 复制到全局 .claude 目录
# Windows
xcopy /E /I .claude "%USERPROFILE%\.claude"
copy CLAUDE.md "%USERPROFILE%\.claude\CLAUDE.md"

# macOS/Linux
cp -r .claude ~/.claude/
cp CLAUDE.md ~/.claude/CLAUDE.md
```

### 方式二：项目级安装

```bash
cd /path/to/your/project

git clone https://github.com/your-username/claude-code-skills.git temp-skills
cp -r temp-skills/.claude .
cp temp-skills/CLAUDE.md .claude/CLAUDE.md
rm -rf temp-skills
```

### 验证安装

检查 Claude Code 中是否可用以下 agent：
- `sdd-architect`
- `sdd-feasibility-analyst`
- `sdd-strategic-planner`
- `sdd-implementer`
- `sdd-code-reviewer`
- `sdd-test-runner`
- `sdd-doc-sync`

## 使用指南

### 1. 创建 Work Item（WI）

格式：`WI-YYYYMMDD-###-slug`
示例：`WI-20260121-001-user-auth`

### 2. 选择 MODE

| MODE | 事实源 | 适用场景 |
|------|--------|----------|
| SpecKit | `.claude/moyu/specs/<WI>/` | 新模块、线性治理 |
| OpenSpec | `.claude/moyu/openspec/specs/**` | 增量变更、跨模块 |

### 3. 执行流水线

```
Phase A：规格阶段（串行 + 人工门禁）
  1. sdd-architect → spec.md / proposal.md
  2. sdd-feasibility-analyst → decisions.md
  3. 人工确认
  4. sdd-strategic-planner → tasks.md + slices/

Phase B：实现阶段（可并发）
  5. sdd-implementer（按 slice）
  6. sdd-code-reviewer
  7. sdd-test-runner → evidence/
  8. 修复回路（如需要）

Phase C：文档阶段（必须）
  9. sdd-doc-sync → .claude/moyu/docs/
  10. 最终验收
```

### 4. 收尾

- **SpecKit**：确保 `spec.md/plan.md/tasks.md` 与实现一致
- **OpenSpec**：将最终行为合并到 `.claude/moyu/openspec/specs/**`
- 按需更新 `.claude/moyu/docs/**`

## Agent-Skill 映射

每个 Agent 通过 frontmatter 声明其技能：

```yaml
---
name: sdd-architect
skills:
  - sdd-common      # 通用技能
  - sdd-architect   # 专属技能
---
```

| Agent | Skills |
|-------|--------|
| sdd-architect | sdd-common, sdd-architect |
| sdd-feasibility-analyst | sdd-common, sdd-feasibility |
| sdd-strategic-planner | sdd-common, sdd-planner |
| sdd-implementer | sdd-common, sdd-implementer |
| sdd-code-reviewer | sdd-common, sdd-reviewer |
| sdd-test-runner | sdd-common, sdd-tester |
| sdd-doc-sync | sdd-common, sdd-docsync |

## Contributing

欢迎提 Issue/PR：

- 尽量小步、可 review
- 所有 SDD 工件必须在 `.claude/moyu/` 下
- 路径变更需同步更新 `CLAUDE.md` 及相关文件

## License

MIT，见 `LICENSE`。
