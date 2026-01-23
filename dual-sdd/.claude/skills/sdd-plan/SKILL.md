---
description: SDD Plan Agent 技能集 - 编排调度、门禁检查、流程控制
user-invocable: false
disable-model-invocation: true
---

# SDD Plan Agent Skills

## PL01: WorkItemInit
### Purpose
初始化 Work Item

### Rules
1. 生成 WI ID：`WI-YYYYMMDD-###-slug`
2. 确定 MODE：speckit 或 openspec
3. 创建 ARTIFACT_ROOT 目录
4. 初始化 context.md

### Process
```
1. 解析用户需求
2. 生成 WI ID
3. 选择 MODE
4. 创建目录结构
5. 写入初始 context.md
6. 返回 Work Item Brief
```

---

## PL02: ModeRouting
### Purpose
决定使用 SpecKit 还是 OpenSpec 模式

### Decision Tree
```
新模块/子系统？
  └─ Yes → SpecKit
  └─ No → 存量迭代/修 bug？
            └─ Yes → OpenSpec
            └─ No → 需要强治理？
                      └─ Yes → SpecKit
                      └─ No → OpenSpec
```

### Factors
- SpecKit: 0→1、线性治理、需求不稳定
- OpenSpec: 存量迭代、跨模块、轻量融入

---

## PL03: PhaseOrchestration
### Purpose
编排执行阶段

### Standard Pipeline
```
Phase A: 规格与对齐（串行 + 人工门禁）
  1. sdd-architect → spec/proposal
  2. sdd-feasibility-analyst → decisions
  3. 人工确认
  4. sdd-strategic-planner → tasks + slices

Phase B: 实现（可并发）
  5. sdd-implementer (并发 by slice)
  6. sdd-code-reviewer
  7. sdd-test-runner
  8. 修复回路

Phase C: 文档闭环
  9. sdd-doc-sync
  10. 最终验收
```

---

## PL04: GateEnforcement
### Purpose
执行阶段门禁检查

### Gates
- Gate A: Spec Ready
- Gate B: Decision Ready
- Gate C: Tasks Ready
- Gate D: Implement Ready
- Gate E: Review Pass
- Gate F: Tests Pass
- Gate G: Docs & Spec Truth Updated

### Enforcement
```
1. 阶段结束时检查对应 Gate
2. 未通过则阻止进入下一阶段
3. 记录 Gate 检查结果
4. 人工门禁需要明确确认
```

---

## PL05: SubagentDispatch
### Purpose
调度 subagent 执行任务

### Rules
1. 只传 L0+L1+L2 上下文
2. 明确任务目标和边界
3. 等待结果并验证
4. 处理失败和重试

### Dispatch Format
```markdown
## Dispatch to: <agent_name>

### Work Item Brief
<L0>

### Context
<L1 - context.md>

### Specific Task
<task_description>

### Expected Output
<what_to_produce>
```

---

## PL06: ConflictResolution
### Purpose
解决并发冲突

### Rules
1. 检测文件冲突
2. 协调 slice 边界
3. 决定合并顺序
4. 处理阻塞报告

### Resolution Order
```
1. 接口/数据结构优先
2. 核心逻辑次之
3. 调用方/适配层最后
4. 测试/文档最后
```
