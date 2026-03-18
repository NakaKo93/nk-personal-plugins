# nk-skill-craft

スキル作成・レビュープラグイン。
Knowledge Skill（kn-*）から Task Skill（ts-*）・Workflow Skill まで、Claude Code スキルとサブエージェントの作成・検証ライフサイクル全体をカバーする。

## スキル

### Knowledge Skill 作成（cksk）

| スキル | 役割 |
|---|---|
| `ts-cksk-orchestrate` | オーケストレーター — Knowledge Skill 作成をエンドツーエンドで制御 |
| `ts-cksk-analyze` | フェーズ2 — ソースファイルを解析してスキル構造を設計 |
| `ts-cksk-build` | フェーズ3 — SKILL.md と references/ ファイルを作成 |

### Workflow Skill 作成（wfsk）

| スキル | 役割 |
|---|---|
| `ts-wfsk-orchestrate` | オーケストレーター — 要件をスキル・サブエージェントに変換 |
| `ts-wfsk-design` | フェーズ2 — ワークフロー設計書を作成 |
| `ts-wfsk-research` | フェーズ3 — 既存アセットの再利用可否を調査 |
| `ts-wfsk-build-skill` | フェーズ5a — SKILL.md と references/ を作成 |
| `ts-wfsk-build-subagent` | フェーズ5b — サブエージェント Markdown ファイルを作成 |
| `ts-wfsk-review` | フェーズ6 — 作成した全成果物を検証 |

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
| `wfsk-build-skill` | ts-wfsk-build-skill |
| `wfsk-build-subagent` | ts-wfsk-build-subagent |
| `wfsk-review` | ts-wfsk-review |
| `validate-subagent` | ts-val-subagent |

## 使い方

| 目的 | トリガー |
|---|---|
| Knowledge Skill を作る | `ts-cksk-orchestrate` |
| Workflow Skill を作る | `ワークフローを作って`、`skill化したい` |
| スキルをレビュー | `スキルをレビューして`、`validate skill` |

## 同梱ドキュメント

```
docs/reference/claude/skills/
├── knowledge/
│   └── knowledge-skill-template.md
└── task-subagent/
    ├── skill-review-checklist.md
    ├── skill-subagent-review-checklist.md
    ├── skill-subagent-architecture.md
    ├── skill-writing-guide.md
    └── subagent-writing-guide.md
```
