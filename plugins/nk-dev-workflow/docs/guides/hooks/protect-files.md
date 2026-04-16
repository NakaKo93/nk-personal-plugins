# protect-files（ファイル保護フック）

**種別**: PreToolUse hook（Read / Write / Edit / Update / MultiEdit / Delete）

**何をするか**: 操作対象のファイルパスが保護パターンに一致した場合にブロックする。
秘密情報・証明書・SSH 鍵など機密性の高いファイルへの意図しないアクセスを防ぐ。

**ブロック対象パターン**:
- `.env`, `secrets/`, `credentials`, `service-account`
- ファイル名: `token`, `secret`, `apikey`, `api_key`
- 拡張子: `.pem`, `.key`, `.p12`, `.pfx`, `.jks`, `.keystore`
- SSH 鍵: `id_rsa`, `id_ed25519`, `id_ecdsa`, `id_dsa`, `.ssh/`

**動作**:
- 一致した場合 → `{"decision": "block", "reason": "..."}` を返して操作を拒否
- 一致しない場合 → `{"decision": "allow"}` を返して通過
