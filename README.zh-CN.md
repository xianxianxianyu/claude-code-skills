# Moyu 双 SDD Skills（SpecKit / OpenSpec）

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

英文版：[`README.md`](README.md)

这个仓库的核心是一套「双 SDD」工作流骨架（SpecKit / OpenSpec），用于在 Claude Code/LLM 团队协作中把“规格 → 计划 → 任务 → 实现 → 验证 → 文档”落到可审计、可复用、路径稳定的工件上。

设计目标很简单：所有 SDD 工件都落在 `.claude/moyu/` 下，repo 根目录保持干净，审查/回溯更确定。

## Features

- 双模式 SDD：按 Work Item（WI）选择 SpecKit 或 OpenSpec
- 单一事实源（Single Source of Truth）：每个 WI 只能选一种模式作为事实源
- 工件路径确定：`context/spec/tasks/evidence` 位置固定，便于 review
- subagent 两层结构：`.claude/agents/` 放 shim（兼容 Claude Code 发现），真实定义在 `.claude/moyu/agents/`
- 统一模板：`.claude/moyu/templates/` 生成一致的工件结构
- skills 库与映射：`.claude/moyu/skills/**` + `.claude/moyu/skills/manifest.yaml`
- 可选可观测性：TRACE Envelope（见 `.claude/moyu/skills/common/07-TraceEnvelope.md`）

## 目录结构（tree）

```text
.
├── CLAUDE.md                               # Plan Agent 手册 + MODE/路径/gates 规则
├── README.md                               # 英文 README
├── README.zh-CN.md                         # 中文 README
├── LICENSE                                 # MIT
└── .claude/                                # Claude Code 集成根目录
    ├── agents/                             # 入口层：shim，保证 Claude Code 能发现 subagent
    │   ├── sdd-architect.md                # shim -> .claude/moyu/agents/sdd-architect.md
    │   ├── sdd-feasibility-analyst.md      # shim -> .claude/moyu/agents/sdd-feasibility-analyst.md
    │   ├── sdd-strategic-planner.md        # shim -> .claude/moyu/agents/sdd-strategic-planner.md
    │   ├── sdd-implementer.md              # shim -> .claude/moyu/agents/sdd-implementer.md
    │   ├── sdd-code-reviewer.md            # shim -> .claude/moyu/agents/sdd-code-reviewer.md
    │   ├── sdd-test-runner.md              # shim -> .claude/moyu/agents/sdd-test-runner.md
    │   └── sdd-doc-sync.md                 # shim -> .claude/moyu/agents/sdd-doc-sync.md
    └── moyu/                               # 真实命名空间：所有 SDD 工件 + prompts 都在这里
        ├── agents/                         # 真实 subagent prompts（权威来源）
        ├── templates/                      # 模板（common/speckit/openspec）
        ├── skills/                         # skills 库（含 manifest.yaml：agent -> skills）
        ├── specs/                          # SpecKit 工件：.claude/moyu/specs/<WI>/...
        ├── openspec/                       # OpenSpec 系统
        │   ├── changes/                    # 变更隔离：.claude/moyu/openspec/changes/<WI>/...
        │   ├── specs/                      # 真相库：.claude/moyu/openspec/specs/**（必须反映最终行为）
        │   └── archive/                    # 归档（可选）
        ├── docs/                           # 开发文档：.claude/moyu/docs/**
        ├── .specify/                       # Specify scaffolding（memory + templates）
        └── trace/                          # 可观测性（可选）：runs.jsonl + 协议说明
```

## 使用指南

1) 先读 `CLAUDE.md`：它定义 MODE 路由、ARTIFACT_ROOT 规则、阶段门禁（gates）。

2) 创建一个 Work Item（WI）：
   - 格式：`WI-YYYYMMDD-###-slug`
   - 示例：`WI-20260121-001-user-auth`

3) 每个 WI 必须且只能选一个 MODE：
   - SpecKit：事实源是 `.claude/moyu/specs/<WI>/`
   - OpenSpec：事实源是 `.claude/moyu/openspec/specs/**`，隔离变更在 `.claude/moyu/openspec/changes/<WI>/`

4) 调用 subagents（从 `.claude/agents/*.md` 入口层开始）：
   - shim 会指向 `.claude/moyu/agents/*.md` 的真实定义
   - 按角色读取并执行 `.claude/moyu/skills/**` 的约束与流程

5) 复制模板并产出工件：
   - 模板在 `.claude/moyu/templates/**`
   - 证据（命令 + 结果摘要）写入 `ARTIFACT_ROOT/evidence/`

6) 收尾（很关键）：
   - SpecKit：确保 `spec.md/plan.md/tasks.md` 与实际实现一致
   - OpenSpec：确保最终行为已同步到 `.claude/moyu/openspec/specs/**`（不要只停留在 changes）
   - 按需更新 `.claude/moyu/docs/**`

## Contributing

欢迎提 Issue/PR：

- 尽量小步、可 review。
- 不要在 repo 根目录生成 `specs/`、`openspec/`、`docs/`、`.specify/`；所有 SDD 工件必须在 `.claude/moyu/` 下。
- 任何路径变更都需要同步更新：`CLAUDE.md`、`.claude/agents` shim、以及相关 skills/templates/docs。

## License

MIT，见 `LICENSE`。

