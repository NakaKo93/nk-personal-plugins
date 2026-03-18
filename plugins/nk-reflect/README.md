# nk-reflect

セッション反省プラグイン。
Claude Code の JSONL セッションログを解析し、エージェント・スキル・フック・プロセスの問題を特定して、修正タスクリストを生成する。

## スキル

| スキル | 役割 |
|---|---|
| `ts-rfl-orchestrate` | オーケストレーター — 反省パイプライン全体を制御 |
| `ts-rfl-extract` | フェーズ1 — JSONL ログを探して extract_events.py を実行 |
| `ts-rfl-analyze` | フェーズ2 — 抽出結果を読んで fixes.json を生成 |
| `ts-rfl-apply` | フェーズ3 — fixes.json を読んで各修正を適用 |

## エージェント

| エージェント | 使用スキル |
|---|---|
| `rfl-extract` | ts-rfl-extract |
| `rfl-analyze` | ts-rfl-analyze |
| `rfl-apply` | ts-rfl-apply |

## 使い方

トリガーフレーズ: `反省して`、`reflect`、`review session`、`analyze what went wrong`

```
/ts-rfl-orchestrate
```

## 注意事項

- 自動トリガーなし — 必ずユーザーの明示的な指示でのみ実行する。
- ローカルファイルシステムの `~/.claude/projects/<current-project>/` へのアクセスが必要。
- 通知音フックはこのプラグイン外で個人管理。
