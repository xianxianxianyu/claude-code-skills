# Claude Code 技能包合集

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

[English](README.md)

一套 Claude Code 技能包合集，提升你的开发工作流效率。

## 包含内容

| 技能包 | 描述 | 适用场景 |
|--------|------|----------|
| [**Dual SDD**](dual-sdd/) | 双模式规格驱动开发骨架（SpecKit / OpenSpec） | 需要结构化 规格→计划→实现→审查 工作流的团队 |
| [**Easy Repo Writer**](easy-repo-writer/) | 自动为任意仓库生成全面文档 | 为现有项目快速生成文档 |

---

## Dual SDD

完整的规格驱动开发框架：

- **SpecKit 模式**：适用于新项目、新模块、线性治理
- **OpenSpec 模式**：适用于增量变更、跨模块、可审计性
- **7 个专职 Agent**：Architect、Feasibility Analyst、Strategic Planner、Implementer、Code Reviewer、Test Runner、Doc Sync
- **9 套技能集**：通用工具 + 角色专属技能
- **门禁系统**：阶段间强制检查点

**快速开始：**
```bash
# 复制到你的项目
cp -r dual-sdd/.claude /path/to/your/project/
```

[详细文档 →](dual-sdd/README.zh-CN.md)

---

## Easy Repo Writer

使用 3-Agent 流水线自动生成文档：

- **erw-planner**：扫描仓库，创建文档计划
- **erw-writer**：生成多视角文档（旅程、系统视图、产品定位）
- **erw-publisher**：质量检查，创建发布包

**快速开始：**
```bash
# 在 Claude Code 中
/easy-repo-writer
```

[详细文档 →](easy-repo-writer/README.zh-CN.md)

---

## 安装方式

### 方式一：全部安装（全局）

```bash
git clone https://github.com/your-username/claude-code-skills.git
cd claude-code-skills

# Windows
xcopy /E /I dual-sdd\.claude "%USERPROFILE%\.claude"
xcopy /E /I easy-repo-writer\.claude "%USERPROFILE%\.claude"

# macOS/Linux
cp -r dual-sdd/.claude ~/.claude/
cp -r easy-repo-writer/.claude ~/.claude/
```

### 方式二：安装特定技能包

```bash
# 只安装 Dual SDD
cp -r dual-sdd/.claude /path/to/your/project/

# 只安装 Easy Repo Writer
cp -r easy-repo-writer/.claude /path/to/your/project/
```

### 方式三：按需选取组件

每个技能包都是模块化的，你可以单独复制 agent 或 skill：

```bash
# 只要 architect agent
cp dual-sdd/.claude/agents/sdd-architect.md /path/to/your/project/.claude/agents/

# 只要 easy-repo-writer skill
cp -r easy-repo-writer/.claude/skills/easy-repo-writer /path/to/your/project/.claude/skills/
```

---

## 快速对比

| 特性 | Dual SDD | Easy Repo Writer |
|------|----------|------------------|
| **用途** | 结构化开发工作流 | 文档生成 |
| **Agent 数量** | 7 个（规格、计划、实现、审查、测试、文档） | 3 个（计划、写作、发布） |
| **工作流** | 多阶段 + 门禁 | 单流水线 |
| **产出** | 规格、计划、任务、代码、测试、文档 | 仅文档 |
| **最适合** | 新功能、重构、团队项目 | 需要文档的现有仓库 |

---

## 目录结构

```
claude-code-skills/
├── README.md                    # 英文版
├── README.zh-CN.md              # 本文件
├── LICENSE                      # MIT
├── dual-sdd/                    # Dual SDD 技能包
│   ├── README.md
│   ├── README.zh-CN.md
│   └── .claude/
│       ├── agents/              # 7 个 SDD agent
│       ├── skills/              # 9 套技能集
│       └── moyu/                # 工件存储
└── easy-repo-writer/            # Easy Repo Writer 技能包
    ├── README.md
    ├── README.zh-CN.md
    └── .claude/
        ├── agents/              # 3 个 ERW agent
        ├── skills/              # ERW 技能
        └── moyu/                # 模板与输出
```

---

## 贡献

欢迎提 Issue 和 PR！

- 尽量小步、可 review
- 每个技能包应该自包含
- 修改时更新相关 README

## License

MIT，见 [LICENSE](LICENSE)。
