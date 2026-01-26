# Easy Repo Writer (ERW) — Project Memory for Claude Code

## 目标 / Goal
- 本项目提供 “Easy Repo Writer” 文档生成能力：为任意仓库生成/补齐高质量、可发布的文档包。
- 产出必须尽量 **真实、可验证、可维护**：不要编造命令、不要猜测未确认的行为；不确定就标注 TODO 并说明需要用户确认。

## 如何使用 / How to run
- 在 Claude Code 中运行：`/easy-repo-writer`
- ERW 采用 3-agent pipeline：
  1) `erw-planner`：扫描仓库 → 形成文档计划
  2) `erw-writer`：按计划写文档（多视角）
  3) `erw-publisher`：质量检查 → 输出发布包（文件清单 + 摘要 + 建议）

## 默认输出策略（非常重要）
- 默认先把草稿/中间产物写到 `.claude/moyu/`（或本 pack 约定的输出目录）里，避免污染 repo 根目录。
- 只有在用户明确同意后，才去修改仓库对外可见的文件（如 `README.md`、`docs/`、`wiki/`、`CHANGELOG.md` 等）。
- 尽量做 **增量更新**：保留现有文档结构和语气；不要大规模重写/删除除非用户要求。

## 工作流 / Workflow Contract

### Phase 0 — 先问 3 个关键问题（如信息不足）
- 目标读者是谁？（新用户 / 贡献者 / 维护者 / 管理层）
- 文档语言？（默认跟随仓库现有 README；若不存在则询问）
- 产出位置？（仅 `.claude/moyu`、或要同步到 repo 的 `README/docs`）

> 若用户未指定：优先产出一个 “可发布的最小文档包”（Quickstart + Architecture + Contributing 基本骨架），先在 `.claude/moyu` 出草稿。

### Phase 1 — `erw-planner`（只读扫描 → 计划）
必须交付：
- 仓库概览：用途、主要模块、入口、依赖/构建体系（从代码与现有文档中提取）
- 文档差距分析：已有啥、缺啥、哪些内容最影响上手/维护
- 文档计划（Plan）：
  - 准备创建/更新哪些文件（逐条列出）
  - 每个文件的目录大纲（heading 列表）
  - 需要验证的点（命令、环境、配置项、示例等）
  - 风险/不确定项（明确标注）

约束：
- 未经确认，不要开始写大量新文档；先把 Plan 给用户看。

### Phase 2 — `erw-writer`（按计划写文档）
写作要求：
- 采用多视角结构（至少包含）：
  - **User Journey / Quickstart**：怎么跑起来、最小例子、常见坑
  - **System View**：模块划分、数据流/控制流、关键目录
  - **Positioning**：这个项目解决什么问题、适用/不适用场景、与相近方案的差异（仅在可验证信息范围内）
- 所有命令/配置：
  - 若能从仓库文件（package.json/pyproject/Makefile/justfile 等）验证，就直接写
  - 若无法验证，写成 “可能的命令（需确认）” 或 TODO，并提示如何验证

### Phase 3 — `erw-publisher`（QA & 发布包）
必须做 QA：
- 断言/事实是否可从仓库验证（避免 hallucination）
- 链接是否相对路径正确、文件名一致、标题层级合理
- 文档结构是否自洽：Quickstart → 细节 → 贡献指南
- 输出 “Publish Package”：
  - 变更文件清单（新增/修改）
  - 每个文件一句话用途
  - 建议下一步（可选：需要用户补充的信息、可再迭代的方向）

## Guardrails（边界与安全）
- 不主动运行破坏性命令（rm、重置分支、清理目录等）；需要时先解释原因并征求确认。
- 不把 secret/密钥写进文档；遇到疑似 secret 文件优先忽略并提醒用户。
- 尽量保持 diff 可审阅：分批提交、每次变更聚焦一个主题（结构/内容/修复链接）。
