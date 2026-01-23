---
description: SDD Feasibility Analyst 技能集 - 方案对比、风险评估、决策推荐
user-invocable: false
disable-model-invocation: true
---

# SDD Feasibility Analyst Skills

## F01: OptionGeneration
### Purpose
生成多个可行方案供对比

### Rules
1. 至少生成 2 个方案
2. 每个方案必须包含：名称、描述、优点、缺点
3. 方案应有明显差异，避免雷同
4. 考虑技术可行性和业务适配性

### Output Format
```markdown
## Option A: <name>
### Description
<description>

### Pros
- <pro_1>
- <pro_2>

### Cons
- <con_1>
- <con_2>

### Effort
<low/medium/high>
```

---

## F02: RiskAssessment
### Purpose
评估每个方案的风险

### Rules
1. 识别技术风险、业务风险、时间风险
2. 评估风险等级：High/Medium/Low
3. 提供风险缓解措施
4. 考虑回滚方案

### Output Format
```markdown
## Risk Assessment: <option_name>

### Technical Risks
| Risk | Level | Mitigation |
|------|-------|------------|
| <risk> | <level> | <mitigation> |

### Business Risks
| Risk | Level | Mitigation |
|------|-------|------------|
| <risk> | <level> | <mitigation> |

### Rollback Plan
<rollback_description>
```

---

## F03: ComparisonMatrix
### Purpose
生成方案对比矩阵

### Rules
1. 定义对比维度（至少 4 个）
2. 每个维度打分或定性评价
3. 突出关键差异
4. 便于决策者快速理解

### Output Format
```markdown
## Comparison Matrix

| Dimension | Option A | Option B | Option C |
|-----------|----------|----------|----------|
| Complexity | Low | Medium | High |
| Performance | Good | Better | Best |
| Maintainability | High | Medium | Low |
| Risk | Low | Medium | High |
```

---

## F04: RecommendationWriting
### Purpose
撰写推荐决策

### Rules
1. 明确推荐哪个方案
2. 说明推荐理由（Why）
3. 列出关键假设
4. 提供备选方案

### Output Format
```markdown
## Recommendation

### Recommended Option
<option_name>

### Rationale
<why_this_option>

### Key Assumptions
- <assumption_1>
- <assumption_2>

### Fallback
<fallback_option_if_fails>
```

---

## F05: DecisionDocWriting
### Purpose
编写 decisions.md 文档

### Rules
1. 位置：ARTIFACT_ROOT/decisions.md
2. 包含所有方案对比和最终决策
3. 记录决策时间和决策者
4. 便于后续追溯

### Template
```markdown
# Decisions: <WI>

## Decision Date
<date>

## Context
<background>

## Options Considered
<options_summary>

## Decision
<final_decision>

## Rationale
<reasoning>

## Consequences
<expected_outcomes>

## Review Date
<when_to_revisit>
```

---

## F06: FeasibilityReport
### Purpose
生成可行性分析报告

### Checklist
- [ ] 至少 2 个方案对比
- [ ] 风险评估完整
- [ ] 推荐方案明确
- [ ] 回滚方案存在
- [ ] decisions.md 已更新
