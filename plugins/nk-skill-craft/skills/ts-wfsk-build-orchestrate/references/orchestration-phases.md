# Orchestration Phases — Build

Phases executed by `ts-wfsk-build-orchestrate` (build phase only).
For the design phases, see `ts-wfsk-plan-orchestrate/references/orchestration-phases.md`.

---

## Phase 4 — Subagent Creation (only if new subagents are needed)

**Invoke**: `ts-wfsk-build-subagent` (via Skill tool)
**Condition**: Only if the reuse report's gap analysis identifies subagents to create
**Input**: Design document + reuse report + list of subagents to build
**Output**: Created file paths and frontmatter decisions

---

## Phase 5 — Skill Creation

**Invoke**: `ts-wfsk-build-skill` (via Skill tool)
**Input**: Design document + reuse report + subagent definitions from Phase 4
**Output**: Created SKILL.md and references/ paths

---

## Phase 6 — Review

**Invoke**: `ts-wfsk-review` (via Skill tool)
**Input**: Design document + all artifacts from Phases 4–5
**Output**: Review report (pass/fail per criterion, issues, recommended fixes)

---

## Phase 7 — Rework (if needed)

**Condition**: Reviewer reports ❌ Critical issues
**Action**:
1. Identify the responsible child skill (`ts-wfsk-build-subagent` or `ts-wfsk-build-skill`)
2. Re-invoke that child skill with the reviewer's specific feedback
3. Re-run Phase 6

---

## Constraints

- Pass only the minimum necessary context to each child skill.
- Track intermediate outputs as short summaries, not full file dumps.
- Do NOT re-do design decisions — design is fixed at this point.
- If a child skill returns with `issues` containing only ✅, proceed to the next phase.
