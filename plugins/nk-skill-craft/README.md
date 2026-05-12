# nk-skill-craft

スキル作成・レビュープラグイン。
Knowledge Skill（kn-*）から Task Skill（ts-*）・Workflow Skill まで、Claude Code スキルとサブエージェントの作成・検証ライフサイクル全体をカバーする。

全体像と使い方は [`docs/guides/overview.md`](docs/guides/overview.md) / [`docs/guides/workflows.md`](docs/guides/workflows.md) を参照。

## スキル

### Knowledge Skill 作成（cksk）

| スキル | 役割 |
|---|---|
| `ts-cksk-orchestrate` | オーケストレーター — Knowledge Skill 作成をエンドツーエンドで制御 |
| `ts-cksk-analyze` | フェーズ2 — ソースファイルを解析してスキル構造を設計 |
| `ts-cksk-build` | フェーズ3 — SKILL.md と references/ ファイルを作成 |

### Workflow Skill 作成（wfsk）

設計フェーズと実装フェーズに分かれている。先に `ts-wfsk-plan-orchestrate` で設計・承認を得てから `ts-wfsk-build-orchestrate` で実装する。

| スキル | 役割 |
|---|---|
| `ts-wfsk-plan-orchestrate` | 設計オーケストレーター — 要件 → 設計ドキュメント + ギャップ分析（ユーザーの入口） |
| `ts-wfsk-build-orchestrate` | 実装オーケストレーター — 承認済み設計 → subagent + skill 作成 + レビュー |
| `ts-wfsk-design` | フェーズ2 — ワークフロー設計書を作成（自動化・共通化・テンプレート配置を評価） |
| `ts-wfsk-research` | フェーズ3 — 既存アセットの再利用可否を調査 |
| `ts-wfsk-build-subagent` | フェーズ4 — 新規サブエージェント Markdown ファイルを作成 |
| `ts-wfsk-build-skill` | フェーズ5 — SKILL.md と references/ を作成 |
| `ts-wfsk-review` | フェーズ6 — 作成した全成果物を検証（共通化・Python自動化・テンプレート配置を確認） |

### スキル検証（val）

| スキル | 役割 |
|---|---|
| `ts-val-orchestrate` | オーケストレーター — スキルディレクトリの品質を検証 |
| `ts-val-task-skill` | Task Skill（ts-*）ディレクトリを検証 |
| `ts-val-subagent` | Task Skill に対応するエージェントファイルを検証 |

## エージェント

| エージェント | 使用スキル |
|---|---|
| `cksk-analyze` | ts-cksk-analyze |
| `cksk-build` | ts-cksk-build |
| `wfsk-design` | ts-wfsk-design |
| `wfsk-research` | ts-wfsk-research |
| `wfsk-build-subagent` | ts-wfsk-build-subagent |
| `wfsk-build-skill` | ts-wfsk-build-skill |
| `wfsk-review` | ts-wfsk-review |
| `validate-subagent` | ts-val-subagent |

## 使い方

| 目的 | 使うスキル | トリガーフレーズ例 |
|---|---|---|
| Workflow Skill を設計する | `ts-wfsk-plan-orchestrate` | 「ワークフローを作って」「skill化したい」 |
| 設計を承認して実装する | `ts-wfsk-build-orchestrate` | 「ビルドして」「承認したので実装して」 |
| Knowledge Skill を作る | `ts-cksk-orchestrate` | 「ナレッジスキルを作って」「社内規約をスキルにして」 |
| スキルをレビュー | `ts-val-orchestrate` | 「スキルをレビューして」「validate skill」 |

## 同梱ドキュメント

```
docs/
├── guides/
│   ├── overview.md                        # 全体構成マップ・アーキテクチャ原則
│   ├── workflows.md                       # シナリオ別の使い方・フロー図
│   └── skills/                            # 各スキルの詳細ガイド
└── reference/claude/skills/
    ├── knowledge/
    │   └── knowledge-skill-template.md
    └── task-subagent/
        ├── skill-review-checklist.md      # 単体スキル検証チェックリスト（A〜J）
        ├── skill-subagent-review-checklist.md  # ファミリーレビューチェックリスト
        ├── file-placement-checklist.md    # docs vs references 配置ルール
        ├── skill-subagent-architecture.md
        ├── skill-writing-guide.md
        └── subagent-writing-guide.md
```
