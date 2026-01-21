---
id: L03
name: OwnershipMatrixBuild
version: 1.0
applies_to:
  agents: [sdd-strategic-planner]
  modes: [speckit, openspec]
inputs: [repo_structure, tasks]
outputs: [ownership_matrix]
---
# OwnershipMatrixBuild

## Purpose
建立并发切片的 allowed paths（文件锁），降低冲突。

## Rules
- 优先按模块/目录切
- 避免多个 slice 改同一文件
- 共享文件标注：Shared (Plan Agent only)

## Output
写入 tasks.md 顶部：
- Slice A: allowed paths: ...
- Slice B: allowed paths: ...
