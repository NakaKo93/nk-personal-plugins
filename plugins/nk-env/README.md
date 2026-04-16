# nk-env

環境用安全フックのプラグイン。
危険なコマンドや不正な Bash 記法をブロックする。

## フック

| イベント | フック | 役割 |
|---|---|---|
| PreToolUse（Bash） | `block-dangerous.sh` | 危険なコマンドをブロック |
| PreToolUse（Bash） | `block-compound-bash.sh` | `&&` `\|\|` `;` によるコマンド連結をブロック |
| UserPromptSubmit | `no-compound-bash.sh` | Bash 連結禁止ルールをプロンプトに注入 |

### block-dangerous.sh がブロックするパターン

- `rm -rf /`、`rm -rf ~`、`rm -rf .`
- `terraform apply/destroy --auto-approve`
- `git push --force`、`git push -f`
- `git push * main`、`git push * master`
- `DROP TABLE`、`DROP DATABASE`
