# ARIAKE OCTA — 配布・マニュアル

本リポジトリは **ARIAKE OCTA** の **公開配布用** です。  
アプリ本体（ZIP）のダウンロードと、ユーザー向けマニュアルを提供します。

## ダウンロード

**Mac は本リポジトリの `v1.2.3-mac` を使わないでください（廃止）。** フルアプリは [MNV_analysis_pro の v1.2.4-mac](https://github.com/yasuoyanagijp-maker/MNV_analysis_pro/releases/tag/v1.2.4-mac) です（2026-09-01 時点で利用施設が動作確認済み）。

| OS | 入手先 |
|----|--------|
| macOS（Apple Silicon） | [`ARIAKE_OCTA_mac.zip`](https://github.com/yasuoyanagijp-maker/MNV_analysis_pro/releases/download/v1.2.4-mac/ARIAKE_OCTA_mac.zip) |
| macOS（Intel） | [`ARIAKE_OCTA_macOS_Intel_v1.2.4.zip`](https://github.com/yasuoyanagijp-maker/MNV_analysis_pro/releases/download/v1.2.4-mac/ARIAKE_OCTA_macOS_Intel_v1.2.4.zip) |
| Windows | 本リポジトリの [Releases](https://github.com/yasuoyanagijp-maker/ARIAKE_OCTA-distribution/releases) の `ARIAKE_OCTA.zip`（`v1.2.3-win`） |

Mac の入れ方: 古い `ARIAKE_OCTA.app` をアプリケーションから削除し、上の ZIP を展開して **`インストール.command` を右クリック →「開く」**。ターミナルで `xattr` / `codesign` する必要はありません。手順の詳細は [documentation/mac_v1.2.3_connection_error.md](documentation/mac_v1.2.3_connection_error.md)。

本リポジトリ Latest の `v1.2.4-optovue-3mm-patch` は、**すでに v1.2.4 が入っている** Mac 向けの小さなパッチです。v1.2.3 の代わりにはなりません。

## マニュアル

| 内容 | リンク |
|------|--------|
| 操作・起動（詳細） | [USER_MANUAL.md](USER_MANUAL.md) |
| 操作の要点（Confirm Selection 等） | [documentation/ARIAKE_OCTA_操作マニュアル_簡易版.md](documentation/ARIAKE_OCTA_操作マニュアル_簡易版.md) |
| 詳細ユーザーマニュアル V2 | [documentation/ARIAKE_OCTA_詳細ユーザーマニュアル_V2.md](documentation/ARIAKE_OCTA_詳細ユーザーマニュアル_V2.md) |
| 多施設グレーディング通知（各サイト／Team YY） | [documentation/collaboration.md](documentation/collaboration.md) |
| ROI の指定方法（手動囲み・血管同定） | [documentation/roi_method.md](documentation/roi_method.md) |
| Mac は v1.2.4（v1.2.3-mac は廃止） | [documentation/mac_v1.2.3_connection_error.md](documentation/mac_v1.2.3_connection_error.md) |

## ログイン（初回起動時）

- **ユーザー名**: ローマ字表記  
- **パスワード**: `ariake2024`

## 画像の選択（重要）

解析開始時は **画像ファイル単位ではなくフォルダ単位** で指定してください。

1. 新しいフォルダを作成する  
2. 解析したい画像をそのフォルダに入れる  
3. アプリでその **フォルダ** を選び、「Confirm Selection」を押す  

## お問い合わせ

柳 靖雄（お花茶屋眼科）  
yasuo.yanagi.jp@gmail.com

---

*ソースコードは非公開リポジトリで管理しています。本リポジトリは配布物とマニュアルのみを公開しています。*
