# ts-wfsk-build-subagent

**何をするか**: 再利用レポートの Gap Analysis で「新規作成」とされた subagent ファイルを `~/.claude/agents/` に作成する。ts-wfsk-orchestrate の Phase 4 で使用。

**起動**: ts-wfsk-orchestrate 経由のみ（直接呼び出し不可）

**入力**: 設計ドキュメント + 再利用レポート（どの subagent を作成するかの情報）

**制約**:
- Gap Analysis で「新規作成」とされたもののみ作成（再利用可能なものは手を加えない）
- スキルファイルの作成・変更は行わない
- ファイル名: `<prefix>-<task>` 形式
- システムプロンプト構成: ロール定義・番号付き手順・制約・出力フォーマット

**出力**: 作成した各 subagent ファイルのパス一覧 + フロントマター決定の根拠
