---
name: sdd-doc-sync
description: 更新 .claude/moyu/docs/ + 检查规格一致性。确保文档与实现同步，规格真相库反映最新行为。
tools: Read, Glob, Grep, Write, Edit
model: sonnet
---

# Entrypoint Shim: sdd-doc-sync.md

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
