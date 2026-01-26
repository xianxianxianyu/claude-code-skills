# SDD Document Types

## Overview

SDD uses two primary document types with distinct responsibilities:

| Document Type | Responsibility | Template | Output Path |
|---------------|----------------|----------|-------------|
| PRD (spec.md/proposal.md) | Why/What | speckit/spec.md, openspec/proposal.md | specs/<WI>/, openspec/changes/<WI>/ |
| Feasibility (decisions.md) | How/Tradeoffs | speckit/decisions.md, openspec/decisions.md | specs/<WI>/, openspec/changes/<WI>/ |

## PRD Documents

### Purpose
Define **WHAT** needs to be built and **WHY**.

### Files
- `spec.md` (SpecKit mode)
- `proposal.md` (OpenSpec mode)

### Required Sections
1. Work Item (WI ID, Mode, Owner)
2. Goal (single business objective)
3. Non-Goals (explicit exclusions)
4. Constraints (technical/business)
5. Background (current behavior)
6. Scenarios (user/dev stories)
7. Acceptance Criteria (min 2, testable)
8. Out of Scope
9. Open Questions (max 7)
10. **Related Documents** (cross-links)

### Cross-Link Requirements
```markdown
## Related Documents
- Feasibility Analysis: [decisions.md](./decisions.md)
- Implementation Plan: [tasks.md](./tasks.md)
- Evidence: [evidence/](./evidence/)
```

## Feasibility Documents

### Purpose
Analyze **HOW** to implement and document **TRADEOFFS**.

### Files
- `decisions.md` (both modes)

### Required Sections
1. Decision Date (ISO8601)
2. Context (background + constraints)
3. Options Considered (min 2)
4. Decision (selected option)
5. Rationale (why this option)
6. Consequences (expected outcomes)
7. Review Date
8. **Source Specification** (cross-link)

### Option Requirements
- Name, description
- Pros (min 2), Cons (min 1)
- Effort estimate (Low/Medium/High)
- Risk assessment with mitigation

### Cross-Link Requirements
```markdown
## Source Specification
- Spec: [spec.md](./spec.md)
- WI: <WI_ID>
```

## Separation of Concerns

| Aspect | PRD | Feasibility |
|--------|-----|-------------|
| Focus | Business requirements | Technical implementation |
| Owner | Product/Architect | Technical Lead |
| Changes | Requires stakeholder approval | Technical team decision |
| Scope | What to build | How to build |

## Workflow

```
1. sdd-architect creates PRD (spec.md/proposal.md)
   ↓
2. sdd-feasibility-analyst creates decisions.md
   ↓
3. Both documents cross-link to each other
   ↓
4. sdd-strategic-planner references both for tasks.md
```
