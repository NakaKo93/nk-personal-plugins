---
name: ts-dmc-draft
description: Delegates to the dmc-drafter subagent to generate a full 12-section design.md draft from concept-hearing answers. Used by ts-dmc-create in Step 2.
context: fork
agent: dmc-drafter
---

# ts-dmc-draft

Invoke the `dmc-drafter` subagent to convert concept-hearing answers into a complete 12-section design.md draft.

## Task Purpose

Produce the full `design.md` draft (all 12 sections, in-conversation only — no disk write) by passing the user's hearing answers to the `dmc-drafter` subagent. Return the draft verbatim to the orchestrator for display and revision.

## Input

The user's concept-hearing answers passed by the orchestrator, covering all or some of:
- プロダクト概要
- ターゲットユーザー
- ブランドムード
- カラー好み
- フォント／タイポトーン
- 主要インタラクションパターン
- アクセシビリティ優先度
- 日本語UI固有の考慮事項

Answers may be partial — unspecified fields will be filled with `[best-effort]` defaults by the subagent.

## Task-Specific Conditions

- Pass the hearing answers to `dmc-drafter` **verbatim** — do not interpret or rephrase them.
- Reference guide used by the subagent: `docs/tmp/design-md/design-md.md`
- The subagent must NOT write any file to disk. Output is in-conversation only.
- If the subagent returns fewer than 12 sections, report the discrepancy in the output block.
- The subagent will prepend a warning block if `docs/design.md` already exists — preserve this warning in the returned output.

## Output Format

Return the subagent's output unchanged to the orchestrator. The output must contain:

1. Warning block (only if `docs/design.md` exists — omit if not present in subagent output)
2. Full 12-section Markdown draft with `[best-effort]` labels on any unspecified fields

Followed by the standard output block:

```
## summary
[1 sentence: whether the draft is complete and how many [best-effort] fields are present]

## decisions
[Any decisions made when mapping hearing answers to sections]

## issues
[Missing sections, ambiguous answers that could not be resolved, or subagent errors]

## next_actions
[Pass draft to orchestrator for reviser loop]
```
