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

### 3. コードを書いて即座に結果を観測できるようにする

JavaScriptのコードはHTMLの `<script src="main.js">` タグで読み込みます。Live Serverはファイルの保存を検知してブラウザを自動でリロードするため、コードを書いてすぐ結果を確認できます。

`main.js` に以下を書いて保存します。

```javascript
console.log("Hello, World!");
```

開発者ツール（`F12`）の **Console** タブを開き、ログが出力されていることを確認します。

`console` にはいくつかのメソッドがあります。それぞれ試して表示の違いを確認しましょう。

```javascript
console.log("通常のログ");
console.warn("警告（黄）");
console.error("エラー（赤）");
console.table([
  { name: "Alice", age: 25 },
  { name: "Bob",   age: 30 },
]);
```

### d. 実行中の変数の値を確認してデバッグできるようにする

コードが意図した通りに動かないとき、どこで何が起きているかを確認するためにブレークポイントを使います。実行を任意の行で一時停止し、その時点での変数の値を確認できます。

1. **Sources** タブを開き、左のファイルツリーから `main.js` を選択します
2. 行番号をクリックしてブレークポイントを設定します（青い印が付きます）
3. ページをリロードし（`F5`）、実行がその行で一時停止することを確認します
4. `F10`（Step over）で一行ずつ実行を進め、右パネルの **Scope** で変数の値を確認します

## まとめ

このステップでは以下を学びました。

- JavaScriptはHTMLの `<script>` タグで読み込んでブラウザが実行する
- Live Serverを使うとファイル保存のたびにブラウザが自動でリロードされる
- 開発者ツールのConsoleでログを確認し、Sourcesでブレークポイントを使ってデバッグできる

**次のステップ:** [02 基本構文](../02-basics/) では変数・型・関数・配列・オブジェクトなど、JavaScriptの基本的な書き方を学びます。

## 一次情報・参考資料

- [VSCode 公式サイト](https://code.visualstudio.com/)
- [Live Server - VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
- [Chrome DevTools ドキュメント](https://developer.chrome.com/docs/devtools/)
- [MDN: コンソール API リファレンス](https://developer.mozilla.org/ja/docs/Web/API/console)
