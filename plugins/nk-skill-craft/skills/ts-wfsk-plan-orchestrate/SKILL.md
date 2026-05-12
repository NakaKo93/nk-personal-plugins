---
name: ts-wfsk-plan-orchestrate
description: Clarifies requirements and produces a workflow design document + gap analysis for user review. Use when the user wants to create or redesign a Claude Code skill or subagent — trigger phrases include "ワークフローを作って", "workflow化したい", "skill化したい", "skill作成したい", "create a workflow", "build a skill for this", "この作業をスキルにして", "subagentを作って", "subagentを作成したい", "subagentを設計したい", "skill修正したい", "skillを直したい". Always run before ts-wfsk-build-orchestrate.
disable-model-invocation: false
allowed-tools: Read
---

# ts-wfsk-plan-orchestrate

Transforms user requirements into a reviewed workflow design document and gap analysis,
ready to hand off to `ts-wfsk-build-orchestrate` for implementation.

## Example Usage

- "コードレビューを自動化するworkflowを作って"
- "この手順をskill化したい"
- "Build a skill that converts meeting notes into Jira tickets"
- "この作業を再利用可能なworkflowにしてほしい"
- "subagentを作成したい"
- "このskillを修正したい"

## Steps

1. **Clarify requirements** — Ask the user for:
   - What they want to accomplish (the workflow goal in 1 sentence)
   - Trigger phrases or conditions (when should this activate?)
   - Output directory (where to create skills and agents — e.g., `plugins/nk-skill-craft`; specify `~/.claude` only for user-level installation)
   - Constraints (tools to avoid, models to prefer, existing assets to integrate)
   If the user says "修正したい" or "直したい", ask which existing skill/subagent is the target and what specifically needs to change — the design document will reflect the intended state after modification.
   Verify the goal is expressible in one sentence before proceeding. Do not delegate an ambiguous requirement.

2. **Execute design pipeline** — Read `references/orchestration-phases.md` for the phase sequence, then execute each phase in order:
   - Phase 1: Structure requirements memo (inline — no child skill)
   - Phase 2: `ts-wfsk-design` — produce design document
   - Phase 3: `ts-wfsk-research` — produce reuse report and gap analysis
   See `references/orchestration-phases.md` for inputs/outputs per phase.

3. **Present design for review** — Use `references/output-schema.md` for the output format. Present:
   - Requirement memo summary
   - Component plan (what to create vs. what to reuse)
   - Execution flow summary
   Then prompt the user to review and confirm before building.

## Handoff

After the user approves the design, run `ts-wfsk-build-orchestrate` with the design document
and reuse report as input. Do NOT start building automatically.

## Error Handling

- **Requirements are ambiguous**: Ask clarifying questions in Step 1. Do not proceed until the goal is expressible in one sentence.
- **Design conflicts with existing assets**: Report the conflict (names, paths) and ask the user how to proceed before continuing.
