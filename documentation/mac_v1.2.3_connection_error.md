# Mac v1.2.3 — 起動直後クラッシュとログイン Connection Error（既知の不具合）

三重大学など、**本リポジトリの macOS 配布 `v1.2.3-mac`（フォルダ名 `ARIAKE_OCTA_mac_v1.2.3`）** で次の組み合わせが出た場合の説明です。パスワードや施設コード（CUSTOM / `MIE_UNIV` など）の問題ではありません。

## 典型的な症状

1. `インストール.command` を右クリック →「開く」が Gatekeeper に止められる。  
2. 展開フォルダで、ZIP 同梱の `xattr` / `cp` / `open` はエラーなく終わる。  
3. ログイン画面は出るが、同時に **「ARIAKE_OCTA quit unexpectedly」（予期せず終了）** が出る。  
4. ログインすると **Connection Error: All connection attempts failed**。

操作画面（Flet）は残っていても、同じ Mac 内の解析エンジン（FastAPI、通常は `127.0.0.1` のローカルポート）が落ちている状態です。

## 原因（要約）

`v1.2.3-mac` のパッケージ欠陥です。macOS 27 固有の未対応 API というより、**未公証の ad-hoc 署名 + Hardened Runtime のまま、解析エンジンを別プロセスで起動する**作りです。子プロセスがコード署名違反（クラッシュレポートの `CODESIGNING` / `Invalid Page`）で殺されると、画面だけ残ってログインできません。

同梱手順の `xattr` だけでは直りません。`codesign --sign -` の再署名も **v1.2.3 では不十分**です（Frameworks 内の `*.dist-info` で再署名が失敗することがあり、成功しても子プロセス起動の問題は残ります）。

**必要なのは Mac v1.2.4 のフル ZIP**（解析エンジンを同一プロセス内で起動する修正済み）。このリポジトリの Latest である `v1.2.4-optovue-3mm-patch` は、**すでに v1.2.4 が入っている Mac 向けの小さなパッチ**であり、v1.2.3 の代わりにはなりません。

## いまできる回避

1. **Mac v1.2.4 のフル ZIP** を研究事務局から受け取り、入れ直す（本リポジトリへ v1.2.4 を載せる作業は別途。この文書ではリリースしません）。  
2. すぐ使う必要がある場合は **Windows 版**（`v1.2.3-win`）。病院の電子カルテ用 Windows でファイアウォールに阻まれる場合は、研究用端末を使ってください。  
3. v1.2.3 のまま `xattr` や再署名だけを繰り返しても、この Connection Error は直らない想定です。

Apple Silicon（M1/M2/M3/M4）は `ARIAKE_OCTA_mac.zip`、Intel Mac は `ARIAKE_OCTA_macOS_Intel_*.zip` です。フォルダ名 `ARIAKE_OCTA_mac_v1.2.3` は Apple Silicon 用です。

---

## 返信してほしい診断情報（医師向け・エンジニアでなくてよい）

以下をメールに貼るか、画面を写真に撮って送ってください。コマンドは **コピーしてターミナルに貼るだけ**です。アプリのパスワードや患者情報は送らないでください。

### A. この Mac の種類

画面左上の **リンゴマーク →「このMacについて」** を開き、次をメモまたはスクリーンショットします。

- チップ（M1 / M2 / M3 / M4 か、Intel）  
- macOS の番号（例: 27.0.1）

### B. クラッシュレポート

「ARIAKE_OCTAが予期せず終了しました」が出たら **「レポート」または「詳細」** を押し、全文をコピーします。

出ない・閉じたあとは:

1. **アプリケーション → ユーティリティ → コンソール** を開く  
2. 左の **クラッシュレポート**（または診断レポート）から `ARIAKE_OCTA` を選ぶ  
3. 全文をコピーする  

特に次の語句があるか見てください（あればその行も残す）。

- `CODESIGNING`  
- `Invalid Page`  
- `SIGKILL`  
- `Symbol not found`  
- `Exception Type` / `Termination Reason`

### C. ターミナル（コピー＆ペースト）

**アプリケーション → ユーティリティ → ターミナル** を開き、次を **まとめて貼り付けて Enter** します。黒い画面に出た文字を全部コピーして送ってください。

```bash
echo "==== Mac ===="
sw_vers
sysctl -n machdep.cpu.brand_string
uname -m
echo "==== App ===="
ls -ld /Applications/ARIAKE_OCTA.app
echo "==== Sign ===="
codesign -dv --verbose=4 /Applications/ARIAKE_OCTA.app 2>&1 | head -50
echo "==== Port ===="
lsof -nP -iTCP:8000 -sTCP:LISTEN 2>/dev/null || echo "nothing listening on 8000"
echo "==== Crash files ===="
ls -lt ~/Library/Logs/DiagnosticReports 2>/dev/null | grep -i ARIAKE | head
```

`codesign` のあとに `Permission denied` や `bundle format unrecognized`（`dist-info` の文字）が出ても、それ自体が手がかりなので消さずに送ってください。

### D. 使った ZIP の確認

展開したフォルダ名が次のどちらだったかも書いてください。

- `ARIAKE_OCTA_mac_v1.2.3`（Apple Silicon 用）  
- `ARIAKE_OCTA_macOS_Intel_v1.2.3`（Intel 用）

---

## 変更履歴

| 日付 | 内容 |
|------|------|
| 2026-10-20 | 三重大学報告（macOS 27.0.1）を受け、v1.2.3-mac の既知欠陥と診断手順を公開文書化。 |
