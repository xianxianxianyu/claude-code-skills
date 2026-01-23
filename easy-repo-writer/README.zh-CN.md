# Easy Repo Writer

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](../LICENSE)

英文版：[`README.md`](README.md)

一个 Claude Code 技能包，使用 3-Agent 流水线自动为任意仓库生成全面、易读的文档。

## 特性

- **3-Agent 流水线**：Planner → Writer → Publisher
- **多视角文档**：旅程轴 + 系统视图 + 产品定位
- **双语支持**：生成中文、英文或双语文档
- **安全发布**：默认 patch 模式 - 生成变更包而不直接修改仓库
- **可调深度**：快速概览、标准文档或深度分析

## 目录结构

```text
easy-repo-writer/
└── .claude/
    ├── agents/                              # Agent 定义
    │   ├── erw-planner.md                   # 扫描仓库，创建文档计划
    │   ├── erw-writer.md                    # 生成文档
    │   └── erw-publisher.md                 # 质量检查，创建发布包
    ├── skills/
    │   └── easy-repo-writer/
    │       ├── SKILL.md                     # 入口技能
    │       └── skills/                      # 内部技能
    │           ├── 00-ERW-Protocol.md
    │           ├── planner/                 # 规划技能
    │           ├── writer/                  # 写作技能
    │           └── publisher/               # 发布技能
    └── moyu/
        ├── templates/easy-repo-writer/      # 文档模板
        └── docs/easy-repo-writer/runs/      # 输出目录
```

## 安装

将 `.claude` 目录复制到你的项目根目录：

```bash
# 从本仓库
cp -r easy-repo-writer/.claude /path/to/your/project/
```

或全局安装：

```bash
# Windows
xcopy /E /I easy-repo-writer\.claude "%USERPROFILE%\.claude"

# macOS/Linux
cp -r easy-repo-writer/.claude ~/.claude/
```

## 使用方法

在 Claude Code 中调用技能：

```bash
# 默认：中文、标准深度、patch 模式
/easy-repo-writer

# 带参数
/easy-repo-writer --lang=en --depth=deep --publish=preview
```

### 参数说明

| 参数 | 选项 | 默认值 | 说明 |
|------|------|--------|------|
| `--lang` | `zh`, `en`, `bilingual` | `zh` | 输出语言 |
| `--depth` | `quick`, `standard`, `deep` | `standard` | 文档深度 |
| `--stage` | `plan`, `write`, `publish`, `all` | `all` | 执行阶段 |
| `--publish` | `preview`, `patch`, `sync` | `patch` | 发布模式 |

### 发布模式

- **preview**：仅生成到 `.claude/moyu/docs/`，不生成发布包
- **patch**：生成发布包和变更清单（安全，推荐）
- **sync**：直接修改仓库根目录文件（需要用户明确同意）

## 输出结构

所有输出位于：

```
.claude/moyu/docs/easy-repo-writer/runs/<RUN_ID>/
├── 00-context/
│   └── repo-profile.md          # 仓库分析
├── 01-plan/
│   ├── doc-map.md               # 文档结构
│   └── tasks.md                 # 写作任务
├── 02-drafts/
│   ├── index.md                 # 导航入口
│   └── *.md                     # 生成的文档
└── 03-publish/
    ├── report.md                # 质量报告
    └── patch/                   # 待发布文件
```

## 流水线概览

```
erw-planner          erw-writer           erw-publisher
    │                    │                     │
    ▼                    ▼                     ▼
扫描仓库 ──────► 生成文档 ──────► 质检 + 打包
    │                    │                     │
repo-profile.md     02-drafts/*.md        patch/
doc-map.md          index.md              report.md
tasks.md
```

## License

MIT，见 [`LICENSE`](../LICENSE)。
