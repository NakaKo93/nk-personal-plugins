# Output Schema — ts-wfsk-build-orchestrate

Defines the final output presented to the user after Phase 6 (or 7) completes.

---

## Final Output

```markdown
## Workflow Build Complete

### Components Created

**Subagents**
- `~/.claude/agents/<name>.md`

**Skills**
- `~/.claude/skills/<name>/SKILL.md`
- `~/.claude/skills/<name>/references/<file>.md`

### Review Result
[Pass/fail summary from wfsk-review]
[Any open ❌ Critical or ⚠️ Warning issues]
```

---

## Standard Output Block (per child subagent)

Each child subagent (`wfsk-build-subagent`, `wfsk-build-skill`, `wfsk-review`) returns:

```markdown
## summary
## decisions
## issues
## next_actions
```
