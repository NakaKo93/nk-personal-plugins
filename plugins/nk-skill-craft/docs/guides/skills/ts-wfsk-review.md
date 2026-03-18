# ts-wfsk-review

**何をするか**: 作成した全スキル・subagent を設計ドキュメントとアーキテクチャポリシーに照らして検証する。ts-wfsk-orchestrate の Phase 6 で使用。

**起動**: ts-wfsk-orchestrate 経由のみ（直接呼び出し不可）

**入力**: 設計ドキュメント + 再利用レポート + 作成した subagent/skill ファイルのパス一覧

**制約**: 読み取りのみ（ファイルの作成・変更は行わない）

**検証観点**:
- アーキテクチャ準拠: オーケストレーターが Skill ツールを使用、チャイルドに `context: fork` + `agent:` がある、`<prefix>-*` 命名規則
- チャイルドスキル本文の完全性（task purpose / input / output format が含まれているか）
- プロジェクト固有コンテンツの混入（警告）

**出力**: レビューレポート（❌ Critical / ⚠️ Warning / ✅ Pass のテーブル）
