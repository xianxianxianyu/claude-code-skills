---
description: SDD Code Reviewer 技能集 - 代码审查、问题分级、改进建议
user-invocable: false
disable-model-invocation: true
---

# SDD Code Reviewer Skills

## R01: ReviewScope
### Purpose
确定审查范围

### Rules
1. 只审查本次变更的代码
2. 对比 spec/tasks 确认范围
3. 不审查无关代码
4. 标记超出范围的修改

---

## R02: IssueClassification
### Purpose
对发现的问题进行分级

### Levels
```markdown
## Blocker (必须修复)
- 安全漏洞
- 数据丢失风险
- 功能完全不工作
- 违反核心约束

## Major (应该修复)
- 性能问题
- 边界条件未处理
- 代码逻辑错误
- 不符合规格要求

## Minor (建议修复)
- 代码风格问题
- 命名不清晰
- 可读性改进
- 文档缺失
```

---

## R03: SecurityReview
### Purpose
检查安全问题

### Checklist
- [ ] 无 SQL 注入风险
- [ ] 无 XSS 风险
- [ ] 无命令注入风险
- [ ] 敏感数据已加密/脱敏
- [ ] 权限检查到位
- [ ] 输入验证完整

---

## R04: LogicReview
### Purpose
检查业务逻辑正确性

### Checklist
- [ ] 符合 spec 定义的行为
- [ ] 边界条件已处理
- [ ] 错误处理合理
- [ ] 状态转换正确
- [ ] 并发安全（如适用）

---

## R05: ReviewReport
### Purpose
生成审查报告

### Template
```markdown
# Code Review Report: <WI>

## Summary
- Files reviewed: <count>
- Blockers: <count>
- Majors: <count>
- Minors: <count>

## Blockers
### B-1: <title>
- File: <file_path>
- Line: <line_number>
- Issue: <description>
- Suggestion: <fix>

## Majors
### M-1: <title>
...

## Minors
### m-1: <title>
...

## Positive Notes
<good_practices_observed>

## Verdict
<PASS / PASS_WITH_COMMENTS / FAIL>
```

---

## R06: TestSuggestion
### Purpose
建议需要的测试覆盖

### Rules
1. 识别未测试的关键路径
2. 建议边界条件测试
3. 建议错误场景测试
4. 优先级排序

### Output Format
```markdown
## Test Suggestions

### High Priority
- [ ] Test case: <description>
  - Input: <input>
  - Expected: <output>

### Medium Priority
- [ ] Test case: <description>
...
```
