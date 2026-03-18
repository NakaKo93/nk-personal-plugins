# ts-wfsk-research

**何をするか**: 既存スキル・subagent を調査し、設計コンポーネントの再利用可否を判定する。ts-wfsk-orchestrate の Phase 3 で使用。

**起動**: ts-wfsk-orchestrate 経由のみ（直接呼び出し不可）

**入力**: 設計ドキュメント（Phase 2 出力）+ 要件メモ

**制約**:
- 読み取りのみ（ファイルの作成・変更は行わない）
- `~/.claude/skills/*/SKILL.md` と `~/.claude/agents/*.md` を確認
- 実際にファイルを読まずに再利用可と判定しない
- 不確かな場合は「部分的に再利用可能」とメモ付きで記載

**出力**: 再利用レポート
- Reusable Assets テーブル（既存アセット / パス / 設計コンポーネント / 適用可否 / 備考）
- Gap Analysis（新規作成が必要なコンポーネント一覧）
- Warnings（命名衝突・責務重複）
