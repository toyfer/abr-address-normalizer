# abr-address-normalizer

入力した住所を「アドレス・ベース・レジストリ（ABR）」の正規表記に変換して表示する、**単一HTMLファイルの静的Webアプリ**です。

- ビルド不要（npm / Node.js 不要）
- APIキー不要・バックエンド不要・データベース不要
- GitHub Pages などの静的ホスティングでそのまま動作

正規化エンジンは [Geolonia `@geolonia/normalize-japanese-addresses`](https://github.com/geolonia/normalize-japanese-addresses)（MIT License）を使用し、デジタル庁が公開する「アドレス・ベース・レジストリ」をデータソースとします。

## 動作イメージ

住所を入力して「正規化」ボタンを押すと、以下を表示します。

| 項目 | 説明 |
|---|---|
| 都道府県 | 例: `北海道` |
| 市区町村 | 例: `札幌市西区` |
| 町字（大字・丁目） | 例: `二十四軒二条二丁目` |
| 街区符号・住居符号／地番 | 例: `3-3` |
| 正規化済み住所（連結） | 都道府県〜番地を連結した文字列 |
| 正規化レベル | 1=都道府県 / 2=市区町村 / 3=町丁目 / 8=街区符号・住居符号または地番 まで判別できたことを示します |
| 緯度・経度 | 正規化結果の代表点（ある場合） |
| 正規化できなかった部分 | 判別不能だった入力の残余文字列 |

## GitHub Pages での公開手順

1. このリポジトリの **Settings → Pages** を開く
2. **Build and deployment** の **Source** で `Deploy from a branch` を選択
3. Branch は `main` / `(root)` を選んで **Save**
4. 数分後、以下のURLで公開されます:

   ```
   https://<ユーザー名>.github.io/abr-address-normalizer/
   ```

> GitHub Actions による `actions/deploy-pages` を使う方法もありますが、本アプリはビルド工程が不要なため、ブランチ配置（上記手順）が最も確実です。

## ローカルでの動作確認

`index.html` をダブルクリックして直接ブラウザで開くだけでも動作します（住所データはCDNから取得します）。ローカルサーバーを立てる場合は:

```sh
# Python の場合
python3 -m http.server 8080

# Node.js がある場合
npx serve .
```

## デスクトップアプリ化（任意）

1. **ブラウザの「アプリとしてインストール」**（ゼロ実装）
   公開URLを Chrome「保存して共有 → インストール」や Edge「アプリ → このサイトをアプリとしてインストール」でインストールすると、独立ウィンドウのデスクトップアプリとして起動できます。
2. **Tauri / Electron でラップ**（配布用）
   `frontendDist` / `loadFile()` に `index.html` を指定するだけで静的フロントエンドとして組み込めます。

## ファイル構成

```text
.
├── index.html   # アプリ本体（これだけ）
├── .nojekyll    # GitHub Pages の Jekyll 処理を無効化
└── README.md
```

## ライセンス・帰属

- 正規化ライブラリ: [`@geolonia/normalize-japanese-addresses`](https://github.com/geolonia/normalize-japanese-addresses) — MIT License
- データソース: デジタル庁「[アドレス・ベース・レジストリ](https://www.digital.go.jp/policies/base_registry_address/)」

本リポジトリ内のアプリケーションコードは MIT License とします。
