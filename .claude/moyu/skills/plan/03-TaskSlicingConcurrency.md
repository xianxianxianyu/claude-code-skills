---
id: P03
name: TaskSlicingConcurrency
version: 1.0
applies_to:
  agents: [plan_agent]
  modes: [speckit, openspec]
inputs: [tasks_md, repo_structure, risk_hotspots]
outputs: [ownership_matrix, slice_assignments, merge_order]
---
# TaskSlicingConcurrency

## Purpose
把任务切成可并发 slice，降低冲突成本，并定义合并顺序。

## Procedure
1) 切片优先级：
   - 按模块/目录切（最佳）
   - 按调用方向切（接口/类型先行）
   - 共享文件 → 标注 “Plan Agent only”
2) 要求 planner 在 tasks.md 写 Ownership Matrix
3) 对每个 slice 分配：
   - allowed paths
   - 任务编号范围（T-xxx）
4) 定义 merge order：
   - 先接口/类型/数据结构
   - 再调用方/适配层
   - 最后文档/清理

## Quality Bar
- 任何 implementer 不得越界写文件；越界触发 C06。
