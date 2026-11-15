# 家計簿的（kakeiboteki）

Google スプレッドシートの家計簿に、スマホやブラウザから支出をさっと記録するウェブアプリです。

- アプリ: https://kangaechu.github.io/kakeiboteki/
- プライバシーポリシー: https://kangaechu.github.io/kakeiboteki/privacy.html

## 構成

- `docs/index.html`: アプリ本体。ビルドなしの HTML 1 枚で、Bootstrap と Google の API クライアントを CDN から読み込む
- `docs/privacy.html`: プライバシーポリシー
- `assets/logo/`: ロゴ（SVG と 120px / 512px の PNG）

## 使い方

1. 「Google でログイン」ボタンで Google アカウントにログインする
2. 初回は Picker が開くので、家計簿のスプレッドシートを選ぶ。選んだファイルの ID はブラウザの localStorage に保存される
3. お財布・日付・費目・支出額・備考を入力して「登録」を押すと、スプレッドシートの `CURRENT` シートに 1 行追加される
4. 年が変わって新しいスプレッドシートを使うときは、「シートを変更」ボタンから新しいファイルを選び直す

ファイルへのアクセス権は Google アカウントごとに付与されるため、複数人で使う場合はそれぞれが一度 Picker で選ぶ必要があります。

## スプレッドシートの構成

- `設定` シート: A 列にお財布、B 列に費目の選択肢を並べる。費目の先頭が登録後の既定値になる
- `CURRENT` シート: A 列から順に、登録時刻・日付・お財布・費目・（数式列）・支出額・備考

## 公開

GitHub Pages で main ブランチの `docs/` を配信します。main に push すると自動で反映されます。

## Google Cloud 側の設定

OAuth スコープは `drive.file` を使っており、Google Picker で選んだスプレッドシートだけにアクセスします。

- Google Sheets API と Google Picker API を有効化する
- OAuth クライアント ID（ウェブアプリケーション）の「承認済みの JavaScript 生成元」に `https://kangaechu.github.io` を登録する
- API キーは Picker の表示にだけ使う（Sheets API の呼び出しは OAuth トークンのみ）。次の制限をかけておく
  - アプリケーションの制限: HTTP リファラー。`https://kangaechu.github.io/kakeiboteki/*` と、Picker の表示に必要な `https://docs.google.com/*`
  - API の制限: Google Picker API のみ
- OAuth 同意画面には、ホームページとプライバシーポリシーに上記の URL、承認済みドメインに `kangaechu.github.io` を登録する。ロゴを登録すると Google のブランド確認が必要になる
