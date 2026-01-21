---
id: C01
name: ResolvePaths
version: 1.0
applies_to:
  agents: [all]
  modes: [speckit, openspec]
inputs: [WORK_ITEM, MODE, ARTIFACT_ROOT]
outputs: [verified_paths, created_dirs_or_errors]
---
# ResolvePaths

## Purpose
在写任何工件/代码前，确认 WI/MODE/ARTIFACT_ROOT **一致且位于 `.claude/moyu/`**，并创建必要目录。

## Preconditions
- 已获得：WORK_ITEM、MODE、ARTIFACT_ROOT（来自 Plan Agent）
- repo 存在 `.claude/moyu/`

## Procedure
1) 校验 ARTIFACT_ROOT 必须以 `.claude/moyu/` 开头。
2) MODE 对应规则：
   - speckit → `.claude/moyu/specs/<WI>/`
   - openspec → `.claude/moyu/openspec/changes/<WI>/`
3) 创建基础目录（若缺失）：
   - `slices/`
   - `evidence/`
4) 若发现同一 WI 在两套事实源中都被写入：停止并上报（见 C06）。

## Postconditions
- 返回：verified_paths（artifacts root + slices + evidence）
- 或返回：errors（明确指出错误路径/混用情况）

## Quality Bar
- 任何写入都不得发生在 `.claude/moyu/` 之外。
