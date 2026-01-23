---
description: SDD Implementer 技能集 - 代码实现、边界检查、增量开发
user-invocable: false
disable-model-invocation: true
---

# SDD Implementer Skills

## I01: BoundaryCheck
### Purpose
实现前检查文件是否在 allowed paths 内

### Rules
1. 读取当前 slice 的 allowed paths
2. 任何修改必须在 allowed paths 内
3. 越界必须立即停止并报告
4. 不得擅自扩展 allowed paths

### Check Process
```
1. 获取目标文件路径
2. 对比 allowed paths 列表
3. 如果匹配 -> 继续
4. 如果不匹配 -> 停止 + 报告
```

---

## I02: IncrementalDev
### Purpose
小步增量开发，避免大范围修改

### Rules
1. 每次修改聚焦单一目标
2. 修改后立即验证（lint/build/test）
3. 保持代码可编译状态
4. 避免大范围重构/格式化

### Process
```
1. 读取目标文件
2. 理解现有代码结构
3. 最小化修改实现目标
4. 验证修改正确性
5. 记录 evidence
```

---

## I03: CodeWriting
### Purpose
编写符合规范的代码

### Rules
1. 遵循项目现有代码风格
2. 不添加不必要的注释
3. 不过度工程化
4. 保持简单直接

### Guidelines
- 变量/函数命名清晰
- 避免深层嵌套
- 单一职责原则
- 错误处理适度

---

## I04: InterfaceFirst
### Purpose
优先实现接口和数据结构

### Rules
1. 先定义接口/类型
2. 再实现具体逻辑
3. 接口变更需要协调
4. 保持向后兼容（如需要）

### Order
```
1. Types/Interfaces
2. Data structures
3. Core logic
4. Integration points
5. Edge cases
```

---

## I05: EvidenceCapture
### Purpose
捕获实现证据

### Rules
1. 每个任务完成后记录 evidence
2. 包含：命令、结果、摘要
3. 保存到 ARTIFACT_ROOT/evidence/
4. 失败也要记录

### Evidence Types
- Build: 编译结果
- Lint: 代码检查结果
- Test: 测试结果
- Manual: 手动验证结果

---

## I06: BlockerReport
### Purpose
报告阻塞问题

### Rules
1. 遇到阻塞立即报告
2. 不要尝试绕过边界
3. 清晰描述阻塞原因
4. 提供可能的解决方案

### Report Format
```markdown
## Blocker Report

### Issue
<description>

### Blocked Task
<task_id>

### Reason
<why_blocked>

### Suggested Resolution
<possible_solutions>

### Files Involved
<file_list>
```
