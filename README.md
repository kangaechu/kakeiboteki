# 家計簿的（kakeiboteki）

家計簿(Google Sheet)のフロントエンドUI

## Google Cloud 側の設定

OAuth スコープは `drive.file` を使っており、Google Picker で選んだスプレッドシートだけにアクセスします。
そのため Cloud プロジェクトで以下が必要です。

- Google Sheets API と Google Picker API を有効化する
- API キーは Picker の表示にだけ使う（Sheets API の呼び出しは OAuth トークンのみ）。次の制限をかけておく
  - アプリケーションの制限: HTTP リファラー。公開 URL（`https://storage.googleapis.com/kangaechu-kakeibo/*`）と、Picker の表示に必要な `https://docs.google.com/*`
  - API の制限: Google Picker API のみ

## OAuth 同意画面用のページとロゴ

- `docs/` にホームページ（`index.html`）とプライバシーポリシー（`privacy.html`）を置いています。OAuth 同意画面を本番公開するときに必要な URL として、GitHub Pages などあなたが所有権確認できるドメインで公開して登録します。
- `assets/logo/` に同意画面用のロゴ（120px / 512px の PNG と元の SVG）を置いています。ロゴを登録すると Google のブランド確認が必要になります。

## 使い方

1. 「Google でログイン」ボタンで Google アカウントにログインする
2. 初回は Picker が開くので、家計簿のスプレッドシートを選ぶ。選んだファイルの ID はブラウザの localStorage に保存される
3. 年が変わって新しいスプレッドシートを使うときは、「シートを変更」ボタンから新しいファイルを選び直す

ファイルへのアクセス権は Google アカウントごとに付与されるため、複数人で使う場合はそれぞれが一度 Picker で選ぶ必要があります。
