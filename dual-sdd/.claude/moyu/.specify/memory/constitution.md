# Project Constitution（不可妥协规则）

1) 单一事实源：每个 WI 只能在 speckit 或 openspec 二选一，不混用工件系统。
2) 规格优先：没有可测试的验收标准（AC）不开始写代码。
3) 小步提交：避免大范围格式化/重构；每次变更必须可解释、可回滚。
4) 证据驱动：实现与测试必须有 evidence（命令+结果摘要）。
5) 文档闭环：完成后更新开发文档与规格真相库。
6) Token 管理：每个 WI 必须维护 context.md（<=400字尽量），subagent 只传 L0+L1+L2。
7) 发现规格矛盾：停止实现，回报 Plan Agent 触发回退（Spec/Plan/Tasks）。
