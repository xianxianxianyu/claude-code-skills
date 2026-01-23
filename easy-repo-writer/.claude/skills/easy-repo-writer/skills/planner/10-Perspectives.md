# 10-Perspectives（Doc Map 的三视角编排）

## 目标
把“三视角”落成一份 doc map（页面列表 + 入口导航 + next links）。

## Doc Map 最小集合（standard 深度）
- index（总导航）
- README（quickstart）
- journey：adopt / integrate / operate / extend / contribute
- views：context / component / code-tour / runtime
- positioning：problem / alternatives / differentiators / adoption-paths
- glossary

## 链接规则
- `index.md` 必须作为唯一总入口（按三视角分区）
- README 必须链接到：
  - journey/adopt
  - views/context
  - positioning/problem

## 输出
写入：`01-plan/doc-map.md`
内容必须包含：
- 页面清单（按目录）
- 每页 1 行“读者问题”描述
- next/see-also 链接建议
