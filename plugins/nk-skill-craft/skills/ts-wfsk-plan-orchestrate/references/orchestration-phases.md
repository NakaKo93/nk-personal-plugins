# Orchestration Phases — Plan

Phases executed by `ts-wfsk-plan-orchestrate` (design phase only).
For the build phases, see `ts-wfsk-build-orchestrate/references/orchestration-phases.md`.

---

## Phase 1 — Requirement Structuring (inline — no child skill)

Organize the clarified user inputs into a requirement memo:

| Field | Description |
|-------|-------------|
| `goal` | One-sentence statement of what the workflow accomplishes |
| `triggers` | Trigger phrases and conditions |
| `scope` | `user` (global) or `project` (local) |
| `output_dir` | Relative path where `skills/` and `agents/` will be created (e.g., `plugins/nk-skill-craft`; use `~/.claude` for user-level only) |
| `constraints` | Tools to avoid, preferred models, known existing assets |
| `output_expectations` | What the finished workflow should produce |

---

## Phase 2 — Design

**Invoke**: `ts-wfsk-design` (via Skill tool)
**Input**: Requirement memo
**Output**: Design document (components, responsibility split, flow, review criteria)

---

## Phase 3 — Reuse Research

**Invoke**: `ts-wfsk-research` (via Skill tool)
**Input**: Requirement memo + design document
**Output**: Reuse report (existing assets, gap analysis, new items needed)

---

## Constraints

- Pass only the minimum necessary context to each child skill.
- Track intermediate outputs as short summaries, not full file dumps.
- Do NOT build any files — implementation is ts-wfsk-build-orchestrate's responsibility.
- Stop after Phase 3 and present results to the user for approval.
