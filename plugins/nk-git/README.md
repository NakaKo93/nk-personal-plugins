# nk-git

git 操作プラグイン。
コミット・ブランチ・PR 作成の一貫したフローを提供する。

## スキル

| スキル | 役割 |
|---|---|
| `ts-commit-orchestrate` | オーケストレーター — 安全なコミットフロー（解析→ブランチ→コミット→同期）|
| `ts-analyze-changes` | git の変更を検査してコミット計画を生成 |
| `ts-git-commit` | 単一のコンベンショナルコミットを作成 |
| `ts-git-branch-commit` | 計画に基づきブランチ作成とコミットを実行 |
| `ts-git-branch` | ブランチの作成・削除 |
| `ts-sync-branch` | 作業ブランチを最新の main に同期 |
| `ts-gh-pr` | gh CLI を使って GitHub Pull Request を作成 |

## エージェント

| エージェント | 使用スキル |
|---|---|
| `analyze-changes` | ts-analyze-changes |
| `git-commit` | ts-git-commit |
| `git-branch-commit` | ts-git-branch-commit |

## 使い方

| 目的 | トリガー |
|---|---|
| 変更をコミット | `コミットして`、`commit these changes` |
| ブランチを作る | `ブランチを作って`、`create a branch` |
| PR を作る | `PRを作って`、`create a PR` |
| main を取り込む | `ブランチを最新化して`、`sync branch` |

## 同梱ドキュメント

```
docs/reference/git/
├── branch-naming.md
├── branch-lifecycle.md
├── commit-format.md
└── pr-guidelines.md
```
