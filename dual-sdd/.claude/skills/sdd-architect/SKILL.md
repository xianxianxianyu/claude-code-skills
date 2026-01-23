---
description: SDD Architect 技能集 - 规格设计、需求分析、架构定义
user-invocable: false
disable-model-invocation: true
---

# SDD Architect Skills

## A01: RequirementAnalysis
### Purpose
分析用户需求，提取 GOAL/NON_GOALS/CONSTRAINTS/ACCEPTANCE

### Rules
1. GOAL 必须是一句话，清晰表达业务目标
2. NON_GOALS 明确边界，避免范围蔓延
3. CONSTRAINTS 列出技术/业务约束
4. ACCEPTANCE 至少 2 条，必须可测试

### Output Format
```markdown
## GOAL
<one_sentence_goal>

## NON_GOALS
- <boundary_1>
- <boundary_2>

## CONSTRAINTS
- <constraint_1>
- <constraint_2>

## ACCEPTANCE
- AC-1: <testable_criteria_1>
- AC-2: <testable_criteria_2>
```

---

## A02: SpecWriting
### Purpose
编写规格文档 (spec.md)

### Rules
1. MODE=speckit 时写 spec.md
2. 必须包含：GOAL, NON_GOALS, CONSTRAINTS, ACCEPTANCE, SCOPE
3. SCOPE 包含 impacted_modules 和 expected_files
4. 不写实现代码，只定义 WHAT/WHY

### Template
```markdown
# Spec: <WI>

## GOAL
<goal>

## NON_GOALS
<non_goals>

## CONSTRAINTS
<constraints>

## ACCEPTANCE
<acceptance_criteria>

## SCOPE
### Impacted Modules
<modules>

### Expected Files
<files>

## NOTES
<background_info>
```

---

## A03: ProposalWriting
### Purpose
编写变更提案 (proposal.md)

### Rules
1. MODE=openspec 时写 proposal.md
2. 必须包含：变更目标、影响范围、delta 描述
3. delta 描述现有行为 vs 期望行为
4. 关联到真相库 `.claude/moyu/openspec/specs/**`

### Template
```markdown
# Proposal: <WI>

## Change Goal
<goal>

## Current Behavior
<current_state>

## Expected Behavior
<expected_state>

## Delta
<what_changes>

## Impact Analysis
### Affected Specs
<spec_files>

### Affected Code
<code_files>

## Risks
<risk_assessment>
```

---

## A04: DeltaTracking
### Purpose
追踪规格变更 delta

### Rules
1. delta 文件位置：ARTIFACT_ROOT/specs/
2. 命名格式：`<original_spec_name>.delta.md`
3. 最终必须合回真相库

---

## A05: ScopeValidation
### Purpose
验证规格范围合理性

### Rules
1. 检查 impacted_modules 是否存在
2. 检查 expected_files 路径是否合理
3. 验证 ACCEPTANCE 是否可测试
4. 范围过大时建议拆分

---

## A06: SpecReview
### Purpose
审查规格完整性

### Checklist
- [ ] GOAL 清晰且单一
- [ ] NON_GOALS 明确边界
- [ ] CONSTRAINTS 完整
- [ ] ACCEPTANCE 可测试
- [ ] SCOPE 合理
- [ ] 无实现细节泄露
