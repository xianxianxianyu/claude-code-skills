---
name: easy-repo-writer
description: Generate readable + deep documentation for this repository using a 3-agent pipeline (erw-planner → erw-writer → erw-publisher).
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Bash, Write, Edit
---

# easy-repo-writer

你是 **ERW（Easy Repo Writer）入口编排器**。你的工作是把本次请求编排成三段子任务，分别交给三个自定义 subagent 执行：

1) `erw-planner`：扫描仓库并产出 doc plan（doc map + 任务清单）
2) `erw-writer`：根据 plan 生成文档草稿（旅程轴 + 系统视图轴 + 产品/行业轴）
3) `erw-publisher`：质量检查 + 产出发布包（默认 patch，不默认改 repo 根目录）

> 重要：即使你开启了 Claude 的 plan mode，本技能也必须**显式点名**调用 `erw-planner / erw-writer / erw-publisher`，不要被内置 Plan subagent 替代执行 ERW 流程。

---

## 0. 解析参数（来自 $ARGUMENTS）

支持参数（都可选）：

- `--lang=zh|en|bilingual`（默认：zh）
- `--depth=quick|standard|deep`（默认：standard）
- `--stage=plan|write|publish|all`（默认：all）
- `--publish=preview|patch|sync`（默认：patch）
  - preview：只生成到 `.claude/moyu/docs/**`，不生成对外发布包
  - patch：生成一个“发布包/变更清单”，不直接修改 repo 根目录文件
  - sync：在用户明确指定时才允许同步到 repo 根 README/docs（高风险操作）

如果用户没有提供参数，使用默认值。

---

## 1. 设定本次 run 目录（必须）

生成 `RUN_ID`：`ERW-YYYYMMDD-HHMMSS`（以本地时间为准）

创建 run root：

`.claude/moyu/docs/easy-repo-writer/runs/<RUN_ID>/`

并写入 `run.json`（包含 lang/depth/stage/publish/RUN_ID）。

---

## 2. 调用 subagents（主线程串行链式执行）

> 约束：subagent 不能再 spawn subagent；所以你必须在主线程按顺序分别调用它们，并把上一步产物路径传下去。

### 2.1 规划（erw-planner）

如果 `--stage=plan|all`：
- 让 `erw-planner` 读取仓库并产出：
  - `00-context/repo-profile.md`
  - `01-plan/doc-map.md`
  - `01-plan/tasks.md`

委派消息必须包含：
- RUN_ID
- run root 路径
- lang/depth/publish

### 2.2 写作（erw-writer）

如果 `--stage=write|all`：
- 让 `erw-writer` 基于 `01-plan/*` 生成文档到：
  - `02-drafts/`（所有 markdown）
  - `02-drafts/index.md`（导航入口）

### 2.3 发布与质检（erw-publisher）

如果 `--stage=publish|all`：
- 让 `erw-publisher` 对 `02-drafts/` 做 QA，并产出：
  - `03-publish/report.md`
  - `03-publish/patch/`（当 publish=patch 或 sync 时）

---

## 3. 最终输出（你必须返回给用户）

最终向用户输出：
- 本次 RUN_ID
- 生成目录（run root）
- 关键文件路径（doc-map / index / report）
- 如果是 patch/sync：明确告诉用户“下一步怎么应用/验证”
