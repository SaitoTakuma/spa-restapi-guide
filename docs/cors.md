# CORS（オリジン間リソース共有）

フロントエンドをCDN(Content Delivery Network)から配信するなどの理由で、フロントエンドとバックエンドで異なるドメイン名を持つ場合があります。

ドメイン名が異なるとブラウザの同一オリジンポリシーによりアクセスが制限されてしまうため、CORSを使用します。

- 参考資料：[オリジン間リソース共有 (CORS) - HTTP | MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/CORS)

CORSに関連するHTTPレスポンスヘッダの設定例は次の通りです。

|HTTPレスポンスヘッダ|設定する値|備考|
|---|---|---|
|`Access-Control-Allow-Origin`|フロントエンドのURL||
|`Access-Control-Allow-Methods`|`GET`、`POST`、`PUT`、`DELETE`、`PATCH`、`OPTIONS`|プリフライトリクエストのために`OPTIONS`を許可します|
|`Access-Control-Allow-Headers`|`Content-Type`|アプリケーションに必要なヘッダを設定します|
|`Access-Control-Max-Age`|`86400`|単位が秒のため、この例では24時間となっています|
|`Access-Control-Allow-Credentials`|`true`|Cookieを送信する場合は`true`にします|

## Cookieの送信

先の表にあるように、CORSを使用しながらCookieを送信したい場合はHTTPレスポンスヘッダに`Access-Control-Allow-Credentials: true`を設定する必要があります。

また、前述のようにフロントエンドとバックエンドでドメイン名が異なる環境において`Set-Cookie`レスポンスヘッダで`SameSite`属性を使用する場合、値を`None`にする必要があります。
`SameSite=None`の場合は`Secure`属性が必須のため、`Secure`属性を付与してHTTPSで通信するようにします。

