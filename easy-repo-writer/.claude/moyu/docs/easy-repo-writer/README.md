# Easy Repo Writer（ERW）使用说明

ERW 是一个独立流程：用 3-agent 流水线为“开源/代码库”生成**易读 + 有深度**的文档草稿，并默认以 patch 的形式交付，不直接污染 repo 根目录。

## 入口（Claude Code）
在 Claude Code 里运行：

- `/easy-repo-writer`
- `/easy-repo-writer --lang=zh --depth=standard --publish=patch`
- `/easy-repo-writer --stage=plan`（只做规划）
- `/easy-repo-writer --stage=write`（只做写作，前提是已有 plan）
- `/easy-repo-writer --publish=preview`（只生成草稿，不打包）
- `/easy-repo-writer --publish=sync`（⚠️ 高风险：允许同步到 repo 根目录）

## 产物位置
所有产物都会写到（每次一个 run）：

`.claude/moyu/docs/easy-repo-writer/runs/<RUN_ID>/`

建议目录结构：

- `00-context/`：仓库画像（入口点/模块/示例/测试/构建）
- `01-plan/`：doc map 与 tasks
- `02-drafts/`：文档草稿
- `03-publish/`：QA report 与 patch（如启用）

## 默认发布策略（强烈建议）
- 默认 `--publish=patch`：只产出 patch 包/变更清单，不直接改 repo 根目录
- 只有你明确 `--publish=sync` 时才允许同步（并在 report 里记录同步清单）
