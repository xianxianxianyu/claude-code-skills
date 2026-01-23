# 33-PublishPackager（发布包/变更清单）

## 目标
把 `02-drafts/` 打包成“可应用”的发布包。

## 输出
- `03-publish/patch/FILES.md`：文件清单（新增/修改/删除）
- `03-publish/patch/PATCH.md`：逐文件变更摘要（每个文件 3–8 行）
- （可选）把 `02-drafts/` 复制为 `03-publish/patch/content/` 方便对外同步

## 默认策略
- patch 模式不直接覆盖 repo 根 README/docs
