# ts-wfsk-design

**何をするか**: 要件メモをワークフロー設計ドキュメントに変換する。`ts-wfsk-plan-orchestrate` の Phase 2 で使用。

**起動**: `ts-wfsk-plan-orchestrate` 経由のみ（直接呼び出し不可）

---

## 入力（orchestrate から渡される）

- `goal`: ワークフローが達成することの 1 文
- `triggers`: 起動フレーズと条件
- `scope`: `user`（グローバル）or `project`（ローカル）
- `constraints`: 避けるべきツール、推奨モデル、既知の既存アセット
- `output_expectations`: 完成したワークフローが生成すべきもの

## 設計時の評価観点

設計ドキュメント生成時に以下を必ず評価する：

| 観点 | 評価内容 | 出力先 |
|---|---|---|
| Python自動化 | 構造的・反復的タスクを AI ではなく Python スクリプトで自動化できるか | Section 9 |
| 共通化 | 導入するルール・ガイドラインが他スキルでも使えるか（docs/ に分離すべきか） | Section 10 |
| テンプレート配置 | 出力フォーマット・JSON スキーマ・テンプレートを references/ または docs/ に配置する計画 | Section 10 |

## 制約

- ファイルシステムの探索は行わない（再利用調査は Phase 3 の担当）
- subagent は最大 5 つまで
- 各コンポーネントは単一の責務を持つ
- 出力フォーマット・JSON スキーマ・テンプレートは SKILL.md にインライン定義しない

## 出力フォーマット（セクション一覧）

| # | セクション | 内容 |
|---|---|---|
| 1 | Purpose | 解決する問題と対象者 |
| 2 | Scope | スコープ内・外の明示 |
| 3 | Trigger Conditions | 起動フレーズと条件 |
| 4 | Inputs and Outputs | 入力・出力の定義 |
| 5 | Overall Flow | エンドツーエンドの実行フロー |
| 6 | Component List | コンポーネント表（Component / Type / Responsibility / Single sentence） |
| 7 | Responsibility Split | 境界が曖昧なペアの責務分担 |
| 8 | Reuse Candidates | 既存アセットの再利用候補 |
| 9 | Automation Opportunities | Python自動化の評価表（Component / Step / Automatable? / Reason） |
| 10 | Shared Resource Candidates | 共通化評価表（Content / Proposed Location / Reusable Across Skills? / Reason） |
| 11 | Review Criteria | レビュー時の確認チェックリスト |

## 関連スキル

- [ts-wfsk-plan-orchestrate](ts-wfsk-plan-orchestrate.md) — 呼び出し元オーケストレーター
- [ts-wfsk-research](ts-wfsk-research.md) — 次ステップ（既存アセット調査）
