# SDD 双模式 Quickstart（给团队看的）

## 1) 创建一个 Work Item
- WI 命名：WI-YYYYMMDD-###-slug
- 选择 MODE：
  - speckit：新模块/0→1/需要线性强治理
  - openspec：存量迭代/跨模块/强审计

---

## 2) SpecKit（MODE=speckit）启动步骤
1) 创建目录：
   - .claude/moyu/specs/<WI>/{slices,evidence}
2) 拷贝模板：
   - context.md ← .claude/templates/common/context.md
   - spec.md    ← .claude/templates/speckit/spec.md
   - plan.md    ← .claude/templates/speckit/plan.md
   - tasks.md   ← .claude/templates/speckit/tasks.md
   - decisions.md ← .claude/templates/speckit/decisions.md
3) 顺序调用 subagents：
   - sdd-architect → sdd-feasibility-analyst →（人工确认）→ sdd-strategic-planner
4) 并发实现：
   - 按 slices/ 切片并发 sdd-implementer
5) Review/Test/Doc：
   - sdd-code-reviewer → sdd-test-runner → sdd-doc-sync

---

## 3) OpenSpec（MODE=openspec）启动步骤
1) 创建目录：
   - .claude/moyu/openspec/changes/<WI>/{slices,evidence,specs}
2) 拷贝模板：
   - context.md  ← .claude/templates/common/context.md
   - proposal.md ← .claude/templates/openspec/proposal.md
   - tasks.md    ← .claude/templates/openspec/tasks.md
   - decisions.md ← .claude/templates/openspec/decisions.md
   - delta spec  ← .claude/templates/openspec/delta-spec.md （按需创建多个）
3) 对齐后实现：
   - sdd-architect → sdd-feasibility-analyst →（人工确认）→ sdd-strategic-planner → 并发 implementers
4) 收尾（关键）：
   - sdd-doc-sync 检查：最终行为必须合回 .claude/moyu/openspec/specs/**（真相库）

---

## 4) Token/Context 约束（强制）
- context.md 保持“一页真相”，尽量 <= 400 字
- subagent 调用只给：L0 Brief + context.md + 最多 3 个代码片段
- subagent 回复先 TL;DR（<=5 bullets），细节落到工件/evidence 文件
