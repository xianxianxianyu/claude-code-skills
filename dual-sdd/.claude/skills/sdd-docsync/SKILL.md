---
description: SDD Doc Sync 技能集 - 文档更新、规格一致性检查
user-invocable: false
disable-model-invocation: true
---

# SDD Doc Sync Skills

## D01: DocInventory
### Purpose
盘点需要更新的文档

### Rules
1. 检查 `.claude/moyu/docs/` 下的文档
2. 识别与本次变更相关的文档
3. 标记需要新建的文档
4. 标记需要更新的文档

### Output Format
```markdown
## Doc Inventory: <WI>

### Existing Docs to Update
| Doc | Reason | Priority |
|-----|--------|----------|
| <path> | <reason> | P0/P1/P2 |

### New Docs Needed
| Doc | Purpose | Priority |
|-----|---------|----------|
| <path> | <purpose> | P0/P1/P2 |
```

---

## D02: DocWriting
### Purpose
编写/更新开发文档

### Rules
1. 位置：`.claude/moyu/docs/`
2. 包含：怎么用、怎么测、边界、示例
3. 保持简洁，避免冗余
4. 代码示例要可运行

### Template
```markdown
# <Feature/Module Name>

## Overview
<brief_description>

## Usage
<how_to_use>

### Example
```<language>
<code_example>
```

## API Reference
<if_applicable>

## Testing
<how_to_test>

## Boundaries & Limitations
<edge_cases_and_limits>

## Related
<links_to_related_docs>
```

---

## D03: SpecConsistencyCheck
### Purpose
检查规格与实现的一致性

### Rules
1. 对比 spec/proposal 与实际实现
2. 标记不一致的地方
3. 确定是更新规格还是修改实现
4. 记录差异

### Checklist
- [ ] GOAL 已实现
- [ ] ACCEPTANCE 全部满足
- [ ] CONSTRAINTS 未违反
- [ ] SCOPE 内文件已修改
- [ ] 无超出 SCOPE 的修改

---

## D04: SpecTruthUpdate
### Purpose
更新规格真相库

### Rules
1. MODE=speckit: 确保 spec/plan/tasks 与实现一致
2. MODE=openspec: 将 delta 合回 `.claude/moyu/openspec/specs/**`
3. 归档变更记录
4. 更新版本标记（如有）

### Process (OpenSpec)
```
1. 读取 proposal.md 中的 delta
2. 定位真相库中的目标 spec
3. 应用变更
4. 验证一致性
5. 归档 change 目录（可选）
```

---

## D05: ChangelogUpdate
### Purpose
更新变更日志

### Rules
1. 位置：`.claude/moyu/docs/CHANGELOG.md`
2. 格式：Keep a Changelog
3. 包含：变更类型、描述、WI 引用
4. 按时间倒序

### Template
```markdown
## [Unreleased]

### Added
- <feature> (<WI>)

### Changed
- <change> (<WI>)

### Fixed
- <fix> (<WI>)

### Removed
- <removal> (<WI>)
```

---

## D06: DocValidation
### Purpose
验证文档完整性

### Checklist
- [ ] 所有公开 API 有文档
- [ ] 使用示例可运行
- [ ] 边界条件已说明
- [ ] 测试方法已说明
- [ ] 规格真相库已更新
- [ ] CHANGELOG 已更新
