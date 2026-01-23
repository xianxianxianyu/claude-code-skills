# 12-RepoScan（扫描与画像）

## 目标
产出“写作可用的 repo 画像”，避免 writer 猜测。

## 建议扫描步骤（Read/Glob/Grep/Bash）
1) 目录拓扑：顶层目录、子包目录、examples/tests
2) 入口点：main/cli entry、public exports
3) 构建与运行：CI、构建脚本、依赖管理文件
4) 示例与测试：找 “黄金路径” 示例（quickstart 优先复用）

## 输出
写入：`00-context/repo-profile.md`，至少包含：
- 目录树（简化版）
- 入口点清单（文件路径 + 简述）
- 示例清单（如何运行）
- 测试/CI 概览（如何跑）
