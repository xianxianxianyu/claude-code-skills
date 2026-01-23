# 00-ERW-Protocol（ERW 流程协议）

## 目的
统一 ERW 的 run 目录结构、命名、默认策略，避免与其他流程（如 SDD）混淆。

## Run Root（必须）
`.claude/moyu/docs/easy-repo-writer/runs/<RUN_ID>/`

推荐子目录（按需创建）：
- `00-context/`：repo-profile、入口点、公共 API 索引
- `01-plan/`：doc-map、tasks
- `02-drafts/`：writer 输出（所有文档草稿）
- `03-publish/`：publisher 输出（report、patch）

## 默认发布策略
- 默认 `publish=patch`：产出 patch 包，不默认修改 repo 根目录
- 只有 `publish=sync` 才允许改 repo 根目录 README/docs（且必须在 report 记录文件清单）

## 三条视角（写作与规划都必须覆盖）
1) 旅程轴：Adopt / Integrate / Operate / Extend / Contribute
2) 系统视图：Context / Component / Code / Runtime
3) 产品轴：Problem / Alternatives / Differentiators / Adoption paths

## “不要做”的清单（硬约束）
- 不创建 repo 根目录的 `docs/` 作为“流程工件”；一切先落 `.claude/moyu/docs/**`
- 本流程独立：不引入 WI / SpecKit / OpenSpec 等概念
