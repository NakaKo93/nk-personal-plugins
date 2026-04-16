# ts-wfsk-design

**何をするか**: 要件メモをワークフロー設計ドキュメントに変換する。ts-wfsk-orchestrate の Phase 2 で使用。

**起動**: ts-wfsk-orchestrate 経由のみ（直接呼び出し不可）

**入力**（orchestrate から渡される）:
- `goal`: ワークフローが達成することの 1 文
- `triggers`: 起動フレーズと条件
- `scope`: `user`（グローバル）or `project`（ローカル）
- `constraints`: 避けるべきツール、推奨モデル、既知の既存アセット
- `output_expectations`: 完成したワークフローが生成すべきもの

**制約**:
- ファイルシステムの探索は行わない（再利用調査は Phase 3 の担当）
- subagent は最大 5 つまで
- 各コンポーネントは単一の責務を持つ

**出力**: 以下のセクションを含む設計ドキュメント
1. Purpose / 2. Scope / 3. Trigger Conditions / 4. Inputs and Outputs
5. Overall Flow / 6. Component List / 7. Responsibility Split
8. Reuse Candidates / 9. Review Criteria
