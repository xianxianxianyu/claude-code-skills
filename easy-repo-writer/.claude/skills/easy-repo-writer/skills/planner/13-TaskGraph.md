# 13-TaskGraph（任务拆分与分配）

## 目标
把 doc map 变成 writer/publisher 可执行任务。

## 规则
- 每个任务 = 1 个输出文件（或一组强相关文件）
- 每个任务必须写清楚：
  - 输入依赖（repo-profile/doc-map）
  - 输出路径（run root 下）
  - 负责人（erw-writer / erw-publisher）
  - 完成定义（DoD）

## 输出
写入：`01-plan/tasks.md`

格式建议（可用 markdown 列表或表格）：
- [W] README quickstart -> 02-drafts/README.md
- [W] Journey adopt -> 02-drafts/journey/adopt.md
- ...
- [P] QA + report -> 03-publish/report.md
