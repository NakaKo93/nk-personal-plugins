---
name: ts-wfsk-build-orchestrate
description: Builds skills and subagents from an approved workflow design document produced by ts-wfsk-plan-orchestrate. Use when the user has reviewed a design and is ready to implement — trigger phrases include "設計で実装して", "ビルドして", "build from design", "この設計で作って", "plan-orchestrateの続き", "承認したのでビルドして", "skill実装して", "skillを実装して", "subagent実装して", "subagentを実装して", "implement the skill", "implement the subagent".
disable-model-invocation: false
allowed-tools: Read
---

# ts-wfsk-build-orchestrate

Implements an approved workflow design: creates subagent files, skill files, and validates the result.
Always requires a design document and reuse report from `ts-wfsk-plan-orchestrate` as input.

## Example Usage

- "この設計で実装して"
- "設計を承認したので作って"
- "Build the workflow from the approved design"
- "ts-wfsk-plan-orchestrate の続き"
- "skill実装して"
- "subagentを実装して"

## Input Required

Before starting, verify that the following are present in the conversation context:

- **Design document** — output from `wfsk-design` (component list, responsibilities, flow)
- **Reuse report** — output from `wfsk-research` (gap analysis, which items to create vs. reuse)

If either is missing, stop immediately and ask the user to run `ts-wfsk-plan-orchestrate` first.

## Steps

1. **Verify inputs** — Confirm the design document and reuse report are present in context.
   If not, do not proceed. Prompt the user to run `ts-wfsk-plan-orchestrate` first.

2. **Execute build pipeline** — Read `references/orchestration-phases.md` for the phase sequence,
   then execute each phase in order:
   - Phase 4: `ts-wfsk-build-subagent` — create subagent files (only if gap analysis shows new ones needed)
   - Phase 5: `ts-wfsk-build-skill` — create SKILL.md and references/ files
   - Phase 6: `ts-wfsk-review` — validate all artifacts
   - Phase 7: Re-invoke the failing child skill if the reviewer reports ❌ issues, then re-run Phase 6
   See `references/orchestration-phases.md` for inputs/outputs per phase.

3. **Present results** — Use `references/output-schema.md` for the output format. Present:
   - Created subagent file paths
   - Created skill file paths
   - Review findings and any remaining known issues

## Error Handling

- **Design document or reuse report missing**: Do not proceed. Ask the user to run `ts-wfsk-plan-orchestrate` first.
- **Reviewer returns critical issues**: Surface the reviewer's findings to the user and ask whether to fix them now or proceed with known issues.
- **Name conflict with existing files**: Report the conflict (names, paths) and ask the user how to proceed before creating any files.

## Limitations

- Does not modify existing skills or subagents — only creates new ones.
- Does not evaluate whether the resulting workflow works end-to-end (runtime testing is the user's responsibility).
- Does not handle project-specific tool configuration (MCP servers, hooks) beyond what the design specifies.
