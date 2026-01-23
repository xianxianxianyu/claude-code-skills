# 30-PublishingPolicy（发布策略）

## 三种 publish 模式
- preview：仅生成 run 工件，不产出 patch
- patch（默认）：产出 patch 包（不改 repo 根目录）
- sync：同步到 repo 根目录（仅在主线程明确要求时）

## 输出位置
- report：`03-publish/report.md`
- patch：`03-publish/patch/`

## 安全规则
- 不允许在未明确 sync 的情况下修改 repo 根 README/docs
- sync 时必须在 report 记录修改清单
