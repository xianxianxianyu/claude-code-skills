---
name: sdd-strategic-planner
description: 拆 tasks + Ownership Matrix + slices。将规格拆解为可执行的任务列表，定义文件归属和切片边界。
tools: Read, Glob, Grep, Write, Edit
model: sonnet
---

# Entrypoint Shim: sdd-strategic-planner.md

This file is kept under .claude/agents/ so Claude Code can discover the subagent.
The real agent definition lives here (canonical source of truth):

- $real

## MUST: Read Skills First
Before doing any work, you MUST read:
- .claude/moyu/skills/README.md
- .claude/moyu/skills/common/*.md
- Your role skills folder (see .claude/moyu/skills/manifest.yaml)

## MUST: Use Moyu paths only
- All SDD artifacts MUST be under .claude/moyu/**
- Templates are at: .claude/moyu/templates/**

## Now do this
1) Open and follow the instructions in: $real
2) Execute the task using that file as the authoritative agent prompt.
