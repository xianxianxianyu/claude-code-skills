---
description: SDD Test Runner 技能集 - 测试编写、执行、证据生成
user-invocable: false
disable-model-invocation: true
---

# SDD Test Runner Skills

## T01: TestPlanning
### Purpose
根据 spec 和 review 建议规划测试

### Rules
1. 覆盖所有 ACCEPTANCE 条件
2. 包含正常路径和异常路径
3. 优先级排序
4. 估算测试范围

### Output Format
```markdown
## Test Plan: <WI>

### Coverage Goals
- AC-1: <test_cases>
- AC-2: <test_cases>

### Test Cases
| ID | Description | Type | Priority |
|----|-------------|------|----------|
| TC-1 | <desc> | Unit | P0 |
| TC-2 | <desc> | Integration | P1 |
```

---

## T02: UnitTestWriting
### Purpose
编写单元测试

### Rules
1. 遵循项目测试框架约定
2. 测试命名清晰表达意图
3. AAA 模式：Arrange-Act-Assert
4. 每个测试聚焦单一行为

### Guidelines
```
- 测试文件位置遵循项目约定
- Mock 外部依赖
- 避免测试实现细节
- 保持测试独立性
```

---

## T03: TestExecution
### Purpose
执行测试并收集结果

### Rules
1. 运行相关测试套件
2. 捕获完整输出
3. 记录通过/失败状态
4. 失败时记录详细信息

### Process
```
1. 确定测试命令
2. 执行测试
3. 解析结果
4. 生成 evidence
```

---

## T04: EvidenceGeneration
### Purpose
生成测试证据文档

### Rules
1. 位置：ARTIFACT_ROOT/evidence/
2. 命名：`test-<scope>-<timestamp>.md`
3. 包含命令、输出、结论
4. 失败测试需要详细分析

### Template
```markdown
# Test Evidence: <scope>

## Execution Info
- Command: `<command>`
- Timestamp: <ISO8601>
- Duration: <seconds>

## Results
- Total: <count>
- Passed: <count>
- Failed: <count>
- Skipped: <count>

## Failed Tests
### <test_name>
- Error: <error_message>
- Stack: <stack_trace>
- Analysis: <root_cause>

## Conclusion
<PASS / FAIL>
```

---

## T05: CoverageAnalysis
### Purpose
分析测试覆盖率

### Rules
1. 运行覆盖率工具
2. 识别未覆盖的关键路径
3. 不追求 100%，关注关键逻辑
4. 记录覆盖率数据

---

## T06: RegressionCheck
### Purpose
确保没有引入回归

### Rules
1. 运行完整测试套件
2. 对比基线结果
3. 新增失败需要分析
4. 记录回归检查结果

### Output Format
```markdown
## Regression Check

### Baseline
- Total tests: <count>
- Passing: <count>

### Current
- Total tests: <count>
- Passing: <count>

### New Failures
<list_or_none>

### Verdict
<NO_REGRESSION / REGRESSION_FOUND>
```
