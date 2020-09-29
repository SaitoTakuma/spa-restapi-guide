# ファイルダウンロード

ファイルダウンロードは[Fetch API](https://developer.mozilla.org/ja/docs/Web/API/Fetch_API)を使用して取得したデータをJavaScriptを用いてダウンロードさせます。

バックエンドではダウンロードさせたいデータをレスポンスボディに設定します。
[REST API設計](./api-design.md)でも述べた通り、ファイルダウンロードではJSONに限らず任意のフォーマットを用いてデータを送信します。

URLをブラウザで直接開いてダウンロードさせる方式ではないため、[Content-Dispositionヘッダ](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Content-Disposition)の付与は任意とします。

フロントエンドではファイルデータを含むHTTPレスポンスを取得すると、ファイルデータからBlobオブジェクトを作成し、その[Blobオブジェクトを表すURIを生成](https://developer.mozilla.org/ja/docs/Web/API/URL/createObjectURL)します。
そして`a`要素を動的に生成し、`href`属性へBlobオブジェクトを表すURIを、`download`属性へファイル名をそれぞれ設定し、`click`メソッドを実行してダウンロードさせます。

!!! Note
    メモリリーク回避のため、生成したBlobオブジェクトを表すURIと`a`要素は使い終わったら破棄するようにします。
