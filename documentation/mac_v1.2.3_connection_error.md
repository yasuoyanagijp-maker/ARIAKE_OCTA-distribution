# Mac v1.2.3 は廃止 — v1.2.4 フル ZIP を使ってください

**本リポジトリの `v1.2.3-mac` は廃止（deprecated）です。**  
三重大学など、`ARIAKE_OCTA_mac_v1.2.3` でログイン画面のあとに「ARIAKE_OCTA quit unexpectedly」と **Connection Error: All connection attempts failed** が出る場合、パスワードや施設コード（CUSTOM / `MIE_UNIV` など）の問題ではありません。古い ZIP を配ってしまったことが原因です。

Mac の正しい入手先は **このリポジトリではなく**、すでに公開済みの v1.2.4 フル ZIP です（2026-09-01 時点で利用施設が動作を確認済み）。

| Mac の種類 | ファイル | リンク |
|------------|----------|--------|
| Apple Silicon（M1 / M2 / M3 / M4） | `ARIAKE_OCTA_mac.zip` | [ダウンロード](https://github.com/yasuoyanagijp-maker/MNV_analysis_pro/releases/download/v1.2.4-mac/ARIAKE_OCTA_mac.zip) |
| Intel | `ARIAKE_OCTA_macOS_Intel_v1.2.4.zip` | [ダウンロード](https://github.com/yasuoyanagijp-maker/MNV_analysis_pro/releases/download/v1.2.4-mac/ARIAKE_OCTA_macOS_Intel_v1.2.4.zip) |

リリース一覧: [v1.2.4-mac](https://github.com/yasuoyanagijp-maker/MNV_analysis_pro/releases/tag/v1.2.4-mac)

このリポジトリの Latest である `v1.2.4-optovue-3mm-patch` は、**すでに v1.2.4 が入っている Mac 向けの小さなパッチ**です。v1.2.3 の代わりにはなりません。

## 入れ直し手順（ターミナルの再署名は不要）

1. アプリが開いていれば終了する。  
2. **古いアプリを削除する**  
   Finder で **アプリケーション** を開き、`ARIAKE_OCTA` をゴミ箱へ。デスクトップの `ARIAKE_OCTA_mac_v1.2.3` フォルダも不要ならゴミ箱へ。  
3. 上の表から、自分の Mac に合う **v1.2.4** ZIP をダウンロードする（「このMacについて」のチップが M1–M4 なら Apple Silicon、Intel なら Intel）。  
4. ZIP をダブルクリックして展開する。  
5. 展開したフォルダの **`インストール.command` を右クリック（Control + クリック）→「開く」**。案内に従ってインストールする。  
6. **ターミナルで `xattr` や `codesign` を実行しない。** v1.2.4 のインストーラーが隔離属性の解除と再署名を行います。v1.2.3 用に書いてあった Terminal 手順は使わないでください。

Gatekeeper が「開発元を確認できない」と出ても、**右クリック → 開く** を選んでください。ダブルクリックだけでは止まることがあります。

## 典型的な症状（v1.2.3 のとき）

1. `インストール.command` を右クリック →「開く」が Gatekeeper に止められる。  
2. 展開フォルダで、ZIP 同梱の `xattr` / `cp` / `open` はエラーなく終わる。  
3. ログイン画面は出るが、同時に **「ARIAKE_OCTA quit unexpectedly」（予期せず終了）** が出る。  
4. ログインすると **Connection Error: All connection attempts failed**。

操作画面は残っていても、同じ Mac 内の解析エンジンが落ちている状態です。

## 原因（要約）

`v1.2.3-mac` のパッケージ欠陥です。macOS 27 固有の未対応 API というより、**未公証の ad-hoc 署名 + Hardened Runtime のまま、解析エンジンを別プロセスで起動する**作りです。子プロセスがコード署名違反（クラッシュレポートの `CODESIGNING` / `Invalid Page`）で殺されると、画面だけ残ってログインできません。

v1.2.3 同梱の `xattr` だけでは直りません。`codesign --sign -` も **v1.2.3 では不十分**です。**v1.2.4 フル ZIP に入れ直してください。**

すぐ Windows が必要な場合のみ、このリポジトリの `v1.2.3-win` を使います。病院の電子カルテ用 Windows でファイアウォールに阻まれる場合は研究用端末を使ってください。

---

## 入れ直しても直らないとき（診断・任意）

v1.2.4 を入れたあとも同じ英文が出る場合だけ、以下を送ってください。コマンドはコピーしてターミナルに貼るだけです。パスワードや患者情報は送らないでください。

### A. この Mac の種類

**リンゴマーク →「このMacについて」** — チップ（M1–M4 か Intel）と macOS の番号。

### B. クラッシュレポート

「ARIAKE_OCTAが予期せず終了しました」の **「レポート」または「詳細」**。なければ **アプリケーション → ユーティリティ → コンソール** のクラッシュレポートから `ARIAKE_OCTA` を選ぶ。`CODESIGNING` / `Invalid Page` / `SIGKILL` / `Symbol not found` の行があれば残す。

### C. ターミナル

**アプリケーション → ユーティリティ → ターミナル** に次を貼り付け、出た文字を全部コピーします。

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

### D. 使った ZIP

展開フォルダ名（`ARIAKE_OCTA_mac_v1.2.4` など）と、上の v1.2.4 リンクから取ったかどうかを書いてください。`ARIAKE_OCTA_mac_v1.2.3` のままなら、まだ古い ZIP です。

---

## 変更履歴

| 日付 | 内容 |
|------|------|
| 2026-10-20 | `v1.2.3-mac` を廃止とし、公開済み [v1.2.4-mac](https://github.com/yasuoyanagijp-maker/MNV_analysis_pro/releases/tag/v1.2.4-mac) へ誘導。入れ直しは右クリック「開く」のみ（ターミナル再署名なし）。 |
| 2026-10-20 | 三重大学報告（macOS 27.0.1）を受け、v1.2.3-mac の既知欠陥と診断手順を公開文書化。 |
