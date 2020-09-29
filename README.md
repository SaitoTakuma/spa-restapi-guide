# SPA + REST API構成のアプリケーション方式設計ガイド

[SPA + REST API構成のサービス開発リファレンス](https://fintan.jp/?p=5952)が提供するコンテンツの1つです。
SPAとREST APIの構成からなるウェブアプリケーションを開発する際に有用な方式設計の例を提供します。

ガイドはGitHub Pagesでホスティングされており、次のURLで公開しています。

- https://fintan-contents.github.io/spa-restapi-guide/

## ドキュメント執筆に必要なソフトウェア

本ドキュメントの執筆には次のソフトウェアを使用しています。

- [Python 3.8](https://www.python.jp/)
- [MkDocs 1.1.2](https://www.mkdocs.org/)
- [Material for MkDocs 5.5.12](https://squidfunk.github.io/mkdocs-material/)

ドキュメントを静的サイトとして生成するためMkdocsを使用しています。
Material for MkDocsはHTMLへ出力する際に適用されるテーマ（デザイン）です。

Material for MkDocsが提供しているDokcerイメージを使用しても構いません。
その場合はDockerをインストールしてください。

- [Docker 19.03](https://www.docker.com/)

また、必要に応じてテキストエディタをインストールしてください。

## ローカルでの表示方法

MkDocsはHTTPサーバーを立ててドキュメントを表示しつつ、Markdownへの修正をリアルタイムにHTMLへ反映させることが可能です。
MkDocsのHTTPサーバーを立てるには次のコマンドを実行してください。

```
$ mkdocs serve
```

HTTPサーバーが起動したらブラウザで [http://localhost:8000](http://localhost:8000) を開いてください。

HTTPサーバーを停止する場合は`Ctrl + C`を押してください。

Dockerイメージを使いたい場合は次のコマンドを実行するとHTTPサーバーが起動します。

```
$ docker run -it --rm -p 8000:8000 -v $(pwd):/docs squidfunk/mkdocs-material@sha256:c1e9396754016164fc360444cc6629e7dd7ad0423a9e76218abc521d7d800397 serve -a 0.0.0.0:8000
```

停止は`Ctrl + C`です。

## ドキュメントのビルド方法

MkDocsを使用してドキュメントをビルドし、HTMLファイルやCSSファイルを出力することも可能です。
次のコマンドでビルドできます。

```
$ mkdocs build
```

HTMLファイルやCSSファイルは`site`ディレクトリへ出力されます。
この`site`ディレクトリをNginxやApacheなどのHTTPサーバーでホスティングするとドキュメントを見ることができます。

Dockerイメージを使ってドキュメントをビルドする場合は次のコマンドを実行してください。

```
$ docker run --rm -v $(pwd):/docs squidfunk/mkdocs-material@sha256:c1e9396754016164fc360444cc6629e7dd7ad0423a9e76218abc521d7d800397 build
```

---

※ このドキュメントは[Fintan コンテンツ 使用許諾条項](https://fintan.jp/?page_id=201)の下に提供されています。

※ このドキュメントに記載されている会社名、製品名は、各社の登録商標または商標です。

