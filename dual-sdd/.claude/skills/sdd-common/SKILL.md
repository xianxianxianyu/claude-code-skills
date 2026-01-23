---
description: SDD 通用技能集 - 路径解析、上下文维护、工件写入规范
user-invocable: false
disable-model-invocation: true
---

# SDD Common Skills

## C01: ResolvePaths
### Purpose
在写任何工件/代码前，确认 WI/MODE/ARTIFACT_ROOT 一致且位于 `.claude/moyu/`

### Rules
1. 解析 Work Item Brief 中的 MODE 字段
2. 根据 MODE 确定 ARTIFACT_ROOT：
   - MODE=speckit → `.claude/moyu/specs/<WI>/`
   - MODE=openspec → `.claude/moyu/openspec/changes/<WI>/`
3. 验证路径存在，不存在则创建
4. 返回解析后的路径供后续使用

---

## C02: ContextMaintenance
### Purpose
维护 context.md 文件，确保上下文信息准确且精简

### Rules
1. context.md 必须 <= 400 字（尽量）
2. 每次阶段变更必须更新 context.md
3. 必须包含：当前状态、关键决策、触达文件、下一步
4. 格式：
```markdown
# Context: <WI>
## Phase: <current_phase>
## Status: <status_summary>
## Key Decisions: <bullet_list>
## Touched Files: <file_list>
## Next Steps: <action_items>
```

---

## C03: ArtifactWriting
### Purpose
规范工件文件的写入格式和位置

### Rules
1. 所有 SDD 工件必须落在 `.claude/moyu/` 下
2. 工件类型及位置：
   - spec.md / proposal.md → ARTIFACT_ROOT/
   - plan.md → ARTIFACT_ROOT/
   - tasks.md → ARTIFACT_ROOT/
   - decisions.md → ARTIFACT_ROOT/
   - evidence/* → ARTIFACT_ROOT/evidence/
   - slices/* → ARTIFACT_ROOT/slices/
3. 写入前检查文件是否存在，存在则更新而非覆盖

---

## C04: TokenBudget
### Purpose
控制 token 使用，避免上下文溢出

### Rules
1. 三层上下文规则：
   - L0: Work Item Brief (<=120字)
   - L1: context.md (<=400字尽量)
   - L2: 必要片段 (最多3个文件片段)
2. subagent 回复必须先 TL;DR (<=5 bullets)
3. 长内容写入工件文件，不在回复中展开

---

## C05: EvidenceRecording
### Purpose
记录执行证据，确保可追溯

### Rules
1. evidence 必须包含：命令 + 结果摘要
2. 格式：
```markdown
## Evidence: <action_name>
- Command: `<command>`
- Result: <pass/fail>
- Summary: <brief_description>
- Timestamp: <ISO8601>
```
3. 保存位置：ARTIFACT_ROOT/evidence/<action_name>.md

---

## C06: TraceLogging
### Purpose
记录执行追踪日志

### Rules
1. 追踪日志位置：`.claude/moyu/trace/runs.jsonl`
2. 每条记录格式：
```json
{"wi": "<WI>", "phase": "<phase>", "agent": "<agent>", "action": "<action>", "ts": "<ISO8601>"}
```
3. 关键节点必须记录：阶段开始、阶段结束、关键决策

---

## C07: GateChecklist
### Purpose
阶段门禁检查

### Rules
1. 每个阶段结束前必须检查对应 Gate
2. Gate 检查失败必须报告，不得跳过
3. Gate 定义参见 CLAUDE.md 中的 Gates 章节
