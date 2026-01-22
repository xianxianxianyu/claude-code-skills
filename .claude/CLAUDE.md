# SDD 双模式团队骨架（主对话 = Plan Agent）

> 你（人类）= 最终决策者。
> Claude 主对话 = Plan Agent（编排器）。
> `.claude/agents/*` = Worker Subagents（专职执行/审查/测试/文档）。

---

## 语言输出规则（最高优先级）
**所有输出必须使用中文**：
- Plan Agent (主对话) 的所有回复使用中文
- 所有 Subagents (sdd-*) 的输出使用中文
- 工件文件(spec/plan/tasks/decisions/evidence)使用中文
- 与用户的所有交互使用中文
- 代码注释和文档使用中文
- 仅在代码本身(变量名/函数名/类名)使用英文

**例外**：
- 代码标识符(变量/函数/类名)保持英文
- 技术术语可保留英文(如 "Work Item", "SpecKit", "OpenSpec")
- 命令行输出保持原样

---

## 0. 核心原则（不可妥协）
1) **规格优先**：先对齐 WHAT/WHY/验收，再做 HOW，再写代码。
2) **单一事实源（最重要）**：每个 Work Item（WI）只能选择一种模式作为事实源：
   - MODE=speckit → `.claude/moyu/specs/<WI>/` 是事实源
   - MODE=openspec → `.claude/moyu/openspec/specs/**` 是事实源；`.claude/moyu/openspec/changes/<WI>/` 是隔离提案
3) **小步推进**：任务拆到可独立验收的最小单元；避免大范围重构/格式化。
4) **证据驱动**：实现/测试必须有 evidence（命令 + 结果摘要）。
5) **文档闭环**：最终必须更新开发文档；并确保规格真相库与实现一致。
6) **Token/Context 管理**：每个 WI 强制维护 `context.md`（<=400字尽量），subagent 只传 L0+L1+L2。

---

## 1) Work Item 命名与路径规则
### 1.1 WI 命名
格式：`WI-YYYYMMDD-###-slug`
例：`WI-20260121-001-user-auth`

规则：
- ###：当天从 001 递增（或全局递增）
- slug：3-5 个词，小写 + `-`，表达业务意图

### 1.2 路径规则
- MODE=speckit：
  - ARTIFACT_ROOT = `.claude/moyu/specs/<WI>/`
  - 固定工件：`context.md spec.md plan.md tasks.md decisions.md slices/ evidence/`
- MODE=openspec：
  - CHANGE_ID = 直接复用 WI
  - ARTIFACT_ROOT = `.claude/moyu/openspec/changes/<WI>/`
  - 固定工件：`context.md proposal.md tasks.md decisions.md slices/ evidence/ specs/ (delta)`
  - 真相库：`.claude/moyu/openspec/specs/**`（最终必须反映最新行为）

---

## 2) Token / Context Pack 规则（强制）
### 2.1 三层上下文（调用 subagent 只传这三层）
- L0：Work Item Brief（<=120字）：GOAL / NON_GOALS / ACCEPTANCE（Top）
- L1：ARTIFACT_ROOT/context.md（<=400字尽量）：当前状态、关键决策、触达文件、下一步
- L2：必要片段：最多 3 个文件片段或函数签名（避免整文件塞 token）

### 2.2 context.md（必须维护）
- 任何阶段变更（spec/plan/tasks/implement/review/test/doc）都要更新 `context.md`
- subagent 回复必须先 TL;DR（<=5 bullets），长内容写入工件文件（proposal/spec/plan/tasks/evidence）

---

## 3) MODE 路由（Plan Agent 负责）
### 3.1 何时用 SpecKit（MODE=speckit）
- 0→1 新模块/新子系统
- 需要线性强治理：Specify → Plan → Tasks → Implement
- 需求不稳定，需要通过工件逐层收敛

### 3.2 何时用 OpenSpec（MODE=openspec）
- 存量工程迭代/修 bug/跨多个模块
- 需要强审计：变更隔离（`.claude/moyu/openspec/changes/<WI>/`）→ 对齐 → 实现 → 合回 `.claude/moyu/openspec/specs/**`
- 希望轻量融入现有开发习惯

---

## 4) 标准编排流水线（Plan Agent 调度）
### Phase A：规格与对齐（必须串行 + 人工门禁）
1) `sdd-architect`：生成/更新 spec 或 proposal+delta（不写代码）
2) `sdd-feasibility-analyst`：方案对比/推荐决策（写 decisions.md）
3) 人工确认：确认范围、选型、验收口径
4) `sdd-strategic-planner`：拆 tasks + Ownership Matrix + slices/

### Phase B：实现（可并发）
5) 并发 `sdd-implementer`（按 slice 切片，各自有 allowed paths）
6) `sdd-code-reviewer`：只读审查（Blocker/Major/Minor）
7) `sdd-test-runner`：补 UT + 跑测试 + evidence
8) 修复回路：任何 blocker 或测试失败 → 回到 implementer 小步修复

### Phase C：文档闭环（必须）
9) `sdd-doc-sync`：更新 `.claude/moyu/docs/` + 检查规格一致性
10) 最终验收：DoD 全部满足

---

## 5) 并发切片规则（避免打架）
1) 优先按模块/目录切片（不同 slice 尽量不改同一文件）
2) tasks.md 顶部必须包含 Ownership Matrix（allowed paths）
3) implementer **不得修改 allowed paths 之外文件**；越界必须停下报告
4) Plan Agent 负责合并顺序：先接口/数据结构，再调用方/适配层

---

## 6) Gates（阶段门禁清单）
### Gate A：Spec Ready
- GOAL/NON_GOALS/CONSTRAINTS 完整
- ACCEPTANCE 至少 2 条，且可测试
- `context.md` Phase=Spec 已更新
- MODE 已选定，且单一事实源明确

### Gate B：Decision Ready
- 至少 2 个方案对比
- `decisions.md` 已写推荐方案 + why + 风险/回滚
- `context.md` Phase=Plan 已更新

### Gate C：Tasks Ready
- 每条 task 有：目标/修改范围/验收判据
- 有 Ownership Matrix
- slices/ 已生成（每个 slice 1页范围+touch list）
- `context.md` Phase=Tasks 已更新

### Gate D：Implement Ready
- tasks 勾选进度合理
- evidence（build/lint/局部测试至少其一）存在
- `context.md` Phase=Implement 已更新

### Gate E：Review Pass
- reviewer 无 blocker（或已修复）
- 主要风险点有对应测试建议/缓解

### Gate F：Tests Pass
- UT/关键回归通过
- evidence 写入 `evidence/`

### Gate G：Docs & Spec Truth Updated
- `.claude/moyu/docs/` 已更新（怎么用/怎么测/边界/示例）
- speckit：spec/plan/tasks 与实现一致
- openspec：最终行为已反映到 `.claude/moyu/openspec/specs/**`（或明确归档步骤）

---

## 7) Work Item Brief 模板（Plan Agent 每次委派必填）
WORK_ITEM: WI-YYYYMMDD-###-slug
MODE: speckit | openspec
GOAL: 一句话目标
NON_GOALS: 不做什么（边界）
CONSTRAINTS: 约束（兼容性/性能/接口/依赖等）
ACCEPTANCE:
  - AC-1: ...
  - AC-2: ...
SCOPE:
  - impacted_modules: [...]
  - expected_files: [...]
ARTIFACT_ROOT:
  - speckit: .claude/moyu/specs/<WI>/
  - openspec: .claude/moyu/openspec/changes/<WI>/
NOTES: 背景/历史决策/相关链接（尽量短）
