# フロントエンド・バックエンド間通信

## 非同期処理

フロントエンド・バックエンド間の通信には[Fetch API](https://developer.mozilla.org/ja/docs/Web/API/Fetch_API)を使います。
Fetch APIは非同期でリクエストを送信するため、レスポンスの待機中もフロントエンドの処理は継続されます。

Fetch APIを使うのではなく、サードパーティ製のライブラリを使用することも考えられますが、その場合でも非同期で処理されることが一般的です。

## リトライ

フロントエンド・バックエンド間の通信では失敗に備えてリトライの機構を用意することで、より安定した通信を行えます。

例えば次に示すHTTPステータスコードが返却された場合に失敗とみなします。

- `500 Internal Server Error`
- `503 Service Unavailable`

リトライはインターバルを置いて失敗時とまったく同じHTTPリクエストを送信します。
どの程度のインターバルを置くかは[切り捨て型指数バックオフ](https://cloud.google.com/storage/docs/exponential-backoff?hl=ja)を用いて算出するのがよいでしょう。
算出方法は次の通りです（単位は秒）。

- （失敗も含めて）HTTPリクエストを送信した回数を`m`とする
- `0`から`1`までのランダム値を`n`とする
- `2のm乗 + n`とあらかじめ定めた最大インターバルのうち小さい方の値を選択する

例えばHTTPリクエストを送信した回数を`4`（つまり、これから4回目のリトライを行う）、このときに得られたランダム値を`0.5`、最大インターバルを`32`とするとインターバルは`16.5`秒となります。

リトライの最大回数を決めておき、それを超えて失敗した場合はエラーが発生したことをユーザーへ知らせて処理を終了します。

### リトライにおけるバックエンド実装の注意点

HTTPリクエストがバックエンドに到達し、適切に処理された後に何かしらの要因で前段のサーバーなどでエラーになる可能性があります。
そういった場合にリトライされると、同じ内容のHTTPリクエストが複数回バックエンドで処理されることになります。

APIが次に示す特徴のうちどちらかを備えていれば前述のような状況になっても問題はありません。

- 状態が変更されない（主に`GET`メソッドで行われるデータ取得系のAPI）
- 同じ内容のHTTPリクエストであれば何度処理しても同じ結果になる（冪等性）

APIがこれらの性質を持たない場合、アプリケーションに不正な状態をもたらす可能性があります。
そのため、二重送信を防止する仕組みなどを取り入れて対策する必要があります。

