# XSS（クロスサイトスクリプティング）対策

XSSとは、ウェブアプリケーションにスクリプトを埋め込める脆弱性がある場合に、これを悪用して利用者のブラウザ上で不正なスクリプトを実行させる攻撃です。

XSSはHTMLを動的に書き出す際、危険な文字を適切にエスケープすることで対策が可能です。

基本的にはSPAの開発に使用するライブラリのリファレンスを読み、XSSへ対策します。

例えばReactであれば[JSX](https://ja.reactjs.org/docs/introducing-jsx.html#jsx-prevents-injection-attacks)を使うことにより、埋め込まれた値をレンダリングされる前にエスケープ処理を行うことでXSSを防止します。
また、ReactにはHTMLを直接設定できる[dangerouslySetInnerHTML](https://ja.reactjs.org/docs/dom-elements.html#dangerouslysetinnerhtml)というAPIがありますが、これの使用を禁止するのがよいでしょう。
