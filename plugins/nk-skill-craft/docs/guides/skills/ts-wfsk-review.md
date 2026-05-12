# ts-wfsk-review

**何をするか**: 作成した全スキル・subagent を設計ドキュメントとアーキテクチャポリシーに照らして検証する。`ts-wfsk-build-orchestrate` の Phase 3 で使用。

**起動**: `ts-wfsk-build-orchestrate` 経由のみ（直接呼び出し不可）

---

## 入力

- 設計ドキュメント（wfsk-design の出力）
- 再利用レポート（wfsk-research の出力）
- 作成した subagent ファイルのパス一覧
- 作成した skill ファイルのパス一覧

## 制約

読み取りのみ（ファイルの作成・変更は行わない）

## 検証観点

チェックリストは `skill-subagent-review-checklist.md` と `file-placement-checklist.md` を参照。

| カテゴリ | 主な確認内容 |
|---|---|
| アーキテクチャ準拠 | orchestrator が Skill ツールを使用 / child skill に `context: fork` + `agent:` がある / `<prefix>-*` 命名規則 |
| 命名一貫性 | family プレフィックスが全コンポーネントで揃っている |
| child skill 品質 | 本文に task purpose / input / output format が含まれている |
| subagent 品質 | 単一責務 / 読み取り専用に Write・Edit がない / PJ 固有コンテンツの混入なし |
| 責務重複 | 複数 subagent で同じ責務を持っていない |
| **共通化の実装** | 複数スキルで共通するルールが docs/ に集約されている / 設計 Section 10 の結果が反映されている |
| **Python自動化の実装** | 設計 Section 9 で「Automatable: Yes」とされたステップが scripts/ に実装されている |
| **テンプレート配置** | 出力フォーマット・JSON スキーマ・テンプレートが SKILL.md にインラインでなく references/ または docs/ にある |
| ファイル配置 | docs/ と references/ の分離が正しい（file-placement-checklist.md 参照） |

## 出力

レビューレポート（❌ Critical / ⚠️ Warning / ✅ Pass のテーブル）

## 関連スキル

- [ts-wfsk-build-orchestrate](ts-wfsk-build-orchestrate.md) — 呼び出し元オーケストレーター
- [ts-wfsk-build-skill](ts-wfsk-build-skill.md) / [ts-wfsk-build-subagent](ts-wfsk-build-subagent.md) — レビュー対象の生成元
