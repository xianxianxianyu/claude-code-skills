# SpecKit 模式工件目录（事实源）

每个 Work Item（WI）一个子目录：

- .claude/moyu/specs/<WI>/
  - context.md        # Context Pack（<=400字尽量）
  - spec.md           # WHAT/WHY/AC
  - plan.md           # HOW（技术方案）
  - tasks.md          # 可执行任务清单（含 Ownership Matrix）
  - decisions.md      # ADR-lite（关键决策记录）
  - slices/           # 并发切片（每个 implementer 一份 1页说明）
  - evidence/         # 测试/命令证据

规则：
- 同一个 WI 不要同时使用 OpenSpec 的 `.claude/moyu/openspec/changes/`。
