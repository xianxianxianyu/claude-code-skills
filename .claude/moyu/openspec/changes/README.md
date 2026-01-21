# OpenSpec 变更提案目录（Change Proposals）

每个 Work Item（WI）一个 change folder：

- .claude/moyu/openspec/changes/<WI>/
  - context.md
  - proposal.md
  - tasks.md
  - decisions.md
  - slices/
  - evidence/
  - specs/            # delta specs（对 `.claude/moyu/openspec/specs/**` 的增量描述）

规则：
- 不要把 change folder 当真相库；真相库是 `.claude/moyu/openspec/specs/**`。
- 完成后需要归档/同步：让 `.claude/moyu/openspec/specs/**` 反映最终行为。
