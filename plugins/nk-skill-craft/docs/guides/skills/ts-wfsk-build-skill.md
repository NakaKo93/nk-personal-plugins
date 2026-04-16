# ts-wfsk-build-skill

**何をするか**: オーケストレータースキル・チャイルドスキル・`references/` ファイルを作成する。ts-wfsk-orchestrate の Phase 5 で使用。

**起動**: ts-wfsk-orchestrate 経由のみ（直接呼び出し不可）

**入力**: 設計ドキュメント + 再利用レポート + Phase 4 の subagent 定義

**制約**:
- オーケストレータースキル: `allowed-tools: Read`、`context:` / `agent:` フィールドなし、Skill ツールでチャイルドを呼び出す
- チャイルドスキル: フロントマターに `context: fork` + `agent: <subagent-name>` が必須
- docs の内容を `references/` にコピーしない（リンクで参照）
- subagent ファイルは作成・変更しない

**出力**: 作成した全スキルファイルのパス一覧 + フロントマター決定の根拠
