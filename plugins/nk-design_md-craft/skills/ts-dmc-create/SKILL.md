---
name: ts-dmc-create
description: >
  Interactively creates docs/design.md through concept hearing, draft generation, and revision cycles.
  Trigger phrases: "design.mdを作って", "デザインドキュメントを作成して", "design document を生成して".
allowed-tools: Read, Write
---

# ts-dmc-create

Interactive workflow for creating `docs/design.md` through a concept-hearing → draft generation → feedback revision cycle.

## Example Usage

- "design.mdを作って"
- "デザインドキュメントを作成して"
- "design document を生成して"
- "プロダクトのデザイン仕様書を作りたい"

---

## Steps

### Step 1: Concept Hearing (hearer — inline)

Ask the user all concept questions in a **single message**. Do not split into multiple rounds.

Cover all of the following dimensions:

1. **プロダクト概要** — このプロダクトは何ですか？どんな問題を解決しますか？
2. **ターゲットユーザー** — 誰が使いますか？年齢層・リテラシー・利用文脈は？
3. **ブランドムード** — 雰囲気・トーンをどう表現したいですか？（例: ミニマル、温かみ、プロフェッショナル）
4. **カラー好み** — 希望するカラーパレットや避けたい色はありますか？
5. **フォント／タイポトーン** — 書体の方向性は？（例: セリフ、サンセリフ、日本語フォントの好み）
6. **主要インタラクションパターン** — ページ遷移・ホバー・アニメーション等、重視するUXパターンはありますか？
7. **アクセシビリティ優先度** — WCAG準拠レベル、コントラスト比、キーボード操作のサポート度合いは？
8. **日本語UI固有の考慮事項** — 縦書き・ルビ・句読点の扱い等、特別な要件はありますか？

Collect the user's answers. **Do not interpret, generate, or draft anything at this stage.** Just record responses.

---

### Step 2: Draft Generation (drafter — subagent)

Invoke the child skill using the `Skill` tool:

```
Skill: ts-dmc-draft
Args: <user's hearing answers verbatim>
```

The child skill will delegate to the `dmc-drafter` subagent, which:
- Reads `docs/tmp/design-md/design-md.md` as reference
- Generates the full 12-section draft (in conversation only — no disk write)
- Marks unspecified values with `[best-effort]`
- Warns if `docs/design.md` already exists

Display the returned draft to the user in full.

---

### Step 3: Revision Loop (reviser — inline)

After displaying the draft, tell the user:

> 修正したいセクションがあれば「〇〇セクションを〜に変更して」と伝えてください。完了したら「完了」「書き出して」「finish」「done」のいずれかを入力してください。

**Per revision request:**
- Identify the target section from the user's instruction.
- If the section is ambiguous, ask: "どのセクションを修正しますか？（1〜12の番号または見出し名で指定してください）"
- Apply the change to that section only. Keep all other sections unchanged.
- Re-display the updated draft in full after each revision.

**Completion conditions** (any of):
- User says: 「完了」「書き出して」「finish」「done」
- User confirms no further revisions are needed

**Before exiting the loop, verify:**
- No `[best-effort]` markers remain that the user has not resolved or accepted.
- If any remain, prompt: "以下のセクションに `[best-effort]` マーカーが残っています。内容を確認して修正しますか、そのまま書き出しますか？" — list the affected sections.
- If the user chooses "そのまま書き出す": reply "了解しました。`[best-effort]` マーカーが残ったまま書き出します。これらは後から手動で修正してください。" and record that the user explicitly accepted the remaining markers before proceeding to Step 4.

---

### Step 4: Write to Disk (writer — inline)

1. **Overwrite check** — Read `docs/design.md`. If it exists, ask the user:
   > `docs/design.md` がすでに存在します。上書きしますか？（yes / no）
   - If "no": stop and inform the user that the file was not written.
   - If "yes": proceed to write.

2. **Write** — Use the `Write` tool to write the finalized draft to `docs/design.md`.

3. **Verify** — Read `docs/design.md` to confirm the write succeeded. Count the number of `##` section headings. If the file cannot be read or the count is less than 12, report the error and stop.

4. **Report** — Confirm completion:
   > `docs/design.md` を書き出しました。セクション数: 12

---

## Error Handling

- **Hearing answers are empty or too vague**: Prompt for clarification on the most critical dimensions (プロダクト概要, ターゲットユーザー) before invoking the drafter.
- **Drafter returns fewer than 12 sections**: Report the gap to the user and re-invoke the drafter.
- **User specifies a section that does not exist**: Respond with the valid section list (1–12) and ask again.

## Limitations

- Does not validate the semantic correctness of the generated design.
- Does not push or commit `docs/design.md` to version control.
- The revision loop applies changes inline without subagent delegation — complex rewrites may require re-invoking the drafter.
