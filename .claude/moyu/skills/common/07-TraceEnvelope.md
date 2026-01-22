---
id: C07
name: TraceEnvelope
version: 1.0
applies_to:
  agents: [all]
  modes: [speckit, openspec]
inputs: [WORK_ITEM, MODE, ARTIFACT_ROOT, skills_used, artifacts_written, gate_results_optional]
outputs: [trace_envelope_in_response, trace_event_jsonl_optional]
---
# TraceEnvelope

## Purpose
Provide observability: clearly record "who ran (agent/subagent) -> why (parent_id) -> which skills -> which artifacts -> which gate results".

## Required Output (in every response)
Your response MUST start with:

[TRACE]
run_id: <YYYYMMDD-HHMMSS-rand>
parent_id: <optional, if triggered by another agent>
agent: <plan_agent|sdd-architect|...>
subagent: <same as agent for worker, or omit>
mode: <speckit|openspec>
work_item: <WI-...>
skills:
  - C01 ResolvePaths
  - ...
artifacts_written:
  - <paths written in this run>
gates:
  - <Gate Name>: PASS|FAIL|N/A
[/TRACE]

## Procedure
1) Generate run_id (time + short random).
2) Set parent_id from caller run_id (if provided).
3) List skills actually used (IDs must exist in `.claude/moyu/skills/**`).
4) If you wrote files, list them under artifacts_written.
5) If you evaluated gates, list PASS/FAIL; otherwise N/A.

## Optional Logging (if file write is allowed)
Append one JSON line to `.claude/moyu/trace/runs.jsonl` (append-only):
{"run_id":"...","parent_id":"...","agent":"...","mode":"...","work_item":"...","skills":["C01","C02"],"artifacts":["..."],"gates":[...],"ts":"..."}

## Quality Bar
- The TRACE block must be truthful, concise, and parseable.
- Skills must use IDs (e.g., C01, A03, L05, I05, R06, T04, D02).

