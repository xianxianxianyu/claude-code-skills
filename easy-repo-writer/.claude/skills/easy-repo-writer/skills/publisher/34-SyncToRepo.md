# 34-SyncToRepo（可选同步到 repo 根目录）

## 前置条件
仅当主线程明确 `publish=sync` 才执行。

## 同步建议（默认最小侵入）
- 只同步 README（或 docs/）的“对外可见版本”
- 保留 `.claude/moyu/docs/**` 作为生成源与审计源

## 输出
- 在 `03-publish/report.md` 写清楚：
  - 同步了哪些文件
  - 覆盖策略（覆盖/合并/新增）
  - 回滚建议（如何恢复）
