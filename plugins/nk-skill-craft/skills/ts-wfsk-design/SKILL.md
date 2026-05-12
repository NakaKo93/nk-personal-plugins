---
name: ts-wfsk-design
description: Produces a workflow design document from user requirements. Used by ts-wfsk-orchestrate in Phase 2.
context: fork
agent: wfsk-design
---

# wfsk-design

Translate the structured requirement memo into a clear, actionable workflow design document.

## Task Purpose

Produce a design document that defines all components (skills and subagents), their responsibilities, the overall execution flow, and review criteria for the workflow being built.

## Input

The requirement memo passed by the orchestrator, containing:
- `goal`: one-sentence statement of what the workflow accomplishes
- `triggers`: trigger phrases and conditions
- `scope`: `user` (global) or `project` (local)
- `constraints`: tools to avoid, preferred models, known existing assets
- `output_expectations`: what the finished workflow should produce

## Task-Specific Conditions

- Do NOT explore the filesystem — reuse research is Phase 3's job
- Limit component count to ≤5 subagents unless strictly necessary
- Each component must have a single, expressible responsibility
- Prefer linear chains over orchestrators when the flow is sequential
- For each component, evaluate whether any steps are structural/deterministic enough to automate with a Python script (e.g., validation, file generation, naming checks). Document findings in Section 9.
- For each rule, guideline, or reference document introduced in this design, evaluate whether other skills could also use it. If yes, it belongs in `docs/` not in skill-specific files. Document findings in Section 10.
- For any output format, JSON schema, or file template defined in this design, plan to place it in `references/` (skill-specific) or `docs/` (cross-skill shared). Never leave templates inline in SKILL.md.

## Output Format

A Markdown design document with sections:
1. Purpose
2. Scope
3. Trigger Conditions
4. Inputs and Outputs
5. Overall Flow
6. Component List (table: Component | Type | Responsibility | Single sentence)
7. Responsibility Split
8. Reuse Candidates
9. Automation Opportunities (table: Component | Step | Automatable? | Reason)
10. Shared Resource Candidates (table: Content | Proposed Location | Reusable Across Skills? | Reason)
11. Review Criteria

Followed by the standard output block:
```
## summary
## decisions
## issues
## next_actions
```
