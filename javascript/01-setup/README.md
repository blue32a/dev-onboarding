# セットアップ・実行環境

## このステップのゴール

このステップを完了すると：

- JavaScriptのコードをブラウザで実行できます
- コードの出力・エラーをブラウザの開発者ツールで確認できます
- 以降のすべてのステップで共通して使う環境が整います

## 前提知識・環境

- 特になし（このステップが出発点です）

## 実践

### 1. JavaScriptを実行できる環境を整える

JavaScriptはブラウザが実行します。コードを書くためのエディタと、実行・確認するためのブラウザの両方を揃える必要があります。

1. [VSCode 公式サイト](https://code.visualstudio.com/) からダウンロードしてインストールします
2. VSCode の拡張機能タブ（`Ctrl+Shift+X`）を開き、「Live Server」を検索してインストールします

### 2. ファイルをHTTPサーバー経由で配信できるようにする

ブラウザでファイルを直接開く（`file://`）と、セキュリティ制約によってES Modulesなど一部の機能が動作しません。Live Serverを使うと `http://localhost` でファイルを配信できるため、以降のすべてのステップで同じ環境を使えます。

1. VSCode でこのリポジトリのフォルダを開きます
2. `index.html` を右クリックし、`Open with Live Server` を選択します
3. ブラウザが自動で開き、ページが表示されることを確認します

### 3. コードをブラウザで実行し、外部ファイルに切り出す

JavaScriptのコードはHTMLの `<script>` タグの中に直接書けます。`<script>` タグは `</body>` の直前に置きます。HTMLは上から順に読み込まれるため、`<head>` などに置くとHTMLの要素がまだ存在しない状態でスクリプトが実行されてしまいます。`</body>` 直前に置くことで、すべての要素が読み込まれた後に実行されます。

`index.html` の `<body>` に以下のように追加して保存します。

```html
<body>
  <h1>セットアップ</h1>

  <script>
    console.log("Hello, World!");
  </script>
</body>
```

開発者ツール（`F12`）の **Console** タブを開き、ログが出力されていることを確認します。

コードが増えるにつれHTMLの中に書き続けると管理しにくくなります。別ファイルに切り出すことでHTMLとJavaScriptの関心を分けられます。

1. `main.js` を作成し、`<script>` タグ内のコードをそのまま移動します

```javascript
console.log("Hello, World!");
```

2. `index.html` の `<script>` タグを `<script src="main.js"></script>` に書き換えます

```html
<body>
  <h1>セットアップ</h1>

  <script src="main.js"></script>
</body>
```

3. ページを確認し、同じログが出力されることを確認します。以降のすべてのステップでは `main.js` にコードを書きます。

## まとめ

このステップでは以下を学びました。

- JavaScriptはHTMLの `<script>` タグに直接書くか、外部ファイルを `<script src="...">` で読み込んでブラウザが実行する
- `<script>` は `</body>` 直前に置くことで、HTMLの要素が読み込まれた後にスクリプトが実行される
- 開発者ツールのConsoleで `console.log` の出力を確認できる

**次のステップ:** [02 基本構文](../02-basics/README.md) では変数・型・関数・配列・オブジェクトなど、JavaScriptの基本的な書き方を学びます。

## 一次情報・参考資料

- [VSCode 公式サイト](https://code.visualstudio.com/)
- [Live Server - VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
- [Chrome DevTools ドキュメント](https://developer.chrome.com/docs/devtools/)
- [MDN: コンソール API リファレンス](https://developer.mozilla.org/ja/docs/Web/API/console)
