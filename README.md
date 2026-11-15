# 家計簿的（kakeiboteki）

Google スプレッドシートの家計簿に、スマホやブラウザから収支をさっと記録するウェブアプリです。

- アプリ: https://kangaechu.github.io/kakeiboteki/
- アプリの説明: https://kangaechu.github.io/kakeiboteki/about.html
- プライバシーポリシー: https://kangaechu.github.io/kakeiboteki/privacy.html

## 使い方

1. 「Google でログイン」ボタンで Google アカウントにログインする
2. 初回はファイル選択画面が開くので、家計簿のスプレッドシートを選ぶ
3. 支出か収入かを選び、お財布・日付・費目・金額・備考を入力して「登録」を押すと、スプレッドシートの `CURRENT` シートに 1 行追加される
4. 年が変わって新しいスプレッドシートを使うときは、「シートを変更」ボタンから選び直す

アプリがアクセスできるのは、ここで選んだスプレッドシートだけです。複数人で使う場合は、それぞれの Google アカウントで一度ファイルを選ぶ必要があります。

## スプレッドシートの構成

[テンプレート](https://docs.google.com/spreadsheets/d/1YTAhHjq4BesvHWEy3GhUEyZf9ucc_VXMgmLSNHytd_s/copy)をコピーして使えます。自分で用意する場合は次の構成にします。

- `設定` シート: 1 行目は見出し。2 行目以降の A 列にお財布、B 列に支出の費目、C 列に収入の費目の選択肢を並べる。支出の費目の先頭が登録後の既定値になる。C 列が空なら収入の切り替えは表示されない
- `CURRENT` シート: A 列から順に、登録時刻・日付・お財布・費目・収入額・支出額・備考。収入額と支出額は選んだ種類の片方だけに入る

## 開発者向け

`docs/` 配下の静的ファイルを GitHub Pages で配信しています。main に push すると反映されます。

Google Cloud 側には次の設定が必要です。

- Google Sheets API と Google Picker API を有効化する
- OAuth クライアント ID（ウェブアプリケーション）の「承認済みの JavaScript 生成元」に `https://kangaechu.github.io` を登録する
- API キーは Picker の表示にだけ使う。制限は次のとおり
  - アプリケーションの制限: HTTP リファラー。`https://kangaechu.github.io/*` と `https://docs.google.com/*`。パスまで含めた `https://kangaechu.github.io/kakeiboteki/*` にすると、リファラーをオリジンだけに切り詰める Safari で Picker が開けなくなる
  - API の制限: Google Picker API のみ
- OAuth 同意画面には、ホームページに `about.html`、プライバシーポリシーに `privacy.html` の URL、承認済みドメインに `kangaechu.github.io` を登録する。ロゴを登録すると Google のブランド確認が必要になる
