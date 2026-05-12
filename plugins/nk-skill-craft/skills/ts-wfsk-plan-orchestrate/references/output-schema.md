# Output Schema — ts-wfsk-plan-orchestrate

Defines the output presented to the user after Phase 3 completes.

---

## Design Review Output

```markdown
## Workflow Design — Review Required

### Goal
[One-sentence goal from requirement memo]

### Scope
[user / project]

### Output Directory
[Path where skills/ and agents/ will be created]

### Component Plan

| Component | Type | Responsibility | Status |
|-----------|------|----------------|--------|
| name | skill / subagent | one sentence | Reuse / Create |

### Execution Flow
[Summary of phase sequence from design document]

### Reuse Summary
- Reusable: [count] existing assets
- New: [count] components to create

---
Design approved? Run `ts-wfsk-build-orchestrate` with this design document and reuse report.
```

---

## Standard Output Block (per child subagent)

Each child subagent (`wfsk-design`, `wfsk-research`) returns:

```markdown
## summary
## decisions
## issues
## next_actions
```
