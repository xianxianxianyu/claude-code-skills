# 11-RepoTaxonomy（仓库类型与文档重点）

## 目标
判断仓库形态（library / CLI / service / monorepo），并决定文档重点。

## 判断信号（按优先级）
- 是否有 cli 入口：cmd/、bin、main、click/argparse、cobra
- 是否有对外 API：public exports、sdk、client、lib/
- 是否有运行形态：docker、deploy、helm、k8s、server 启动脚本
- 是否 monorepo：packages/、pnpm-workspace、turbo、bazel、workspace

## 输出到 repo-profile
在 `00-context/repo-profile.md` 里明确写：
- repo 类型 + 依据
- 文档优先级（例如 CLI：Adopt/Operate 优先；库：Integrate/Extend 优先）
