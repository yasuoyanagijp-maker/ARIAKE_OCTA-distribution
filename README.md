# ARIAKE OCTA — 配布・マニュアル

本リポジトリは **ARIAKE OCTA** の **公開配布用** です。  
アプリ本体（ZIP）のダウンロードと、ユーザー向けマニュアルを提供します。

## ダウンロード

[Releases](https://github.com/yasuoyanagijp-maker/ARIAKE_OCTA-distribution/releases) から OS に合わせて ZIP を取得してください。

| OS | ファイル名の目安 |
|----|------------------|
| macOS（Apple Silicon） | `ARIAKE_OCTA_mac.zip` 等 |
| macOS（Intel） | `ARIAKE_OCTA_macOS_Intel_*.zip` |
| Windows | `ARIAKE_OCTA.zip` |

**Mac v1.2.3 の既知の不具合:** ログイン画面は出ても、同時に「ARIAKE_OCTA quit unexpectedly」となり、ログインが **Connection Error: All connection attempts failed** になることがあります。パスワードや施設コード（CUSTOM 含む）の誤りではありません。同梱の `xattr` / `cp` / `open` だけでは直りません。説明と診断手順は [documentation/mac_v1.2.3_connection_error.md](documentation/mac_v1.2.3_connection_error.md)。Latest の `v1.2.4-optovue-3mm-patch` は v1.2.4 向けの小さなパッチで、v1.2.3 の代わりにはなりません。Mac は **v1.2.4 のフル ZIP**（本リポジトリ未掲載の場合は研究事務局へ）または Windows 版を使ってください。

## マニュアル

| 内容 | リンク |
|------|--------|
| 操作・起動（詳細） | [USER_MANUAL.md](USER_MANUAL.md) |
| 操作の要点（Confirm Selection 等） | [documentation/ARIAKE_OCTA_操作マニュアル_簡易版.md](documentation/ARIAKE_OCTA_操作マニュアル_簡易版.md) |
| 詳細ユーザーマニュアル V2 | [documentation/ARIAKE_OCTA_詳細ユーザーマニュアル_V2.md](documentation/ARIAKE_OCTA_詳細ユーザーマニュアル_V2.md) |
| 多施設グレーディング通知（各サイト／Team YY） | [documentation/collaboration.md](documentation/collaboration.md) |
| ROI の指定方法（手動囲み・血管同定） | [documentation/roi_method.md](documentation/roi_method.md) |
| Mac v1.2.3 起動クラッシュ / Connection Error | [documentation/mac_v1.2.3_connection_error.md](documentation/mac_v1.2.3_connection_error.md) |

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
