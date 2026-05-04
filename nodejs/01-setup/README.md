# セットアップ

## このステップのゴール

- Node.jsのスクリプトをターミナルから実行できます
- REPLを使ってコードをその場で試せます
- ブラウザでは動かないファイル操作やHTTPサーバーをJavaScriptで扱える環境を準備できます

## 前提知識・環境

- ターミナルの基本操作ができること（ディレクトリの移動・コマンドの実行）
- Node.js v24（LTS）以上（このコンテンツでは `import.meta.dirname`・`--env-file` など v22 以降の機能を使用します）

## 実践

### 1. Node.jsをインストールする

[Node.js 公式サイト](https://nodejs.org/) からv24（LTS）をダウンロードしてインストールします。

インストール後、ターミナルで以下を実行してバージョンを確認します。

```
node --version
```

### 2. スクリプトを実行する

ブラウザではHTMLを経由してJavaScriptを実行しましたが、Node.jsでは `.js` ファイルを直接実行できます。

`main.js` に以下を書き、ターミナルで `node main.js` を実行します。

```javascript
console.log("Hello, Node.js!");
```

`Hello, Node.js!` がターミナルに出力されることを確認します。

### 3. REPLを使う

ターミナルで `node` とだけ入力すると、対話的にJavaScriptを実行できるREPL（Read-Eval-Print Loop）が起動します。

```
$ node
> 1 + 1
2
> "hello".toUpperCase()
'HELLO'
> .exit
```

`.help` でコマンド一覧を確認できます。終了は `.exit` または `Ctrl+C` を2回押します。

### 4. ブラウザとの違いを確認する

Node.jsとブラウザはどちらもJavaScriptを実行しますが、実行環境が異なります。`main.js` に以下を書いて確認します。

```javascript
console.log(typeof window);    // "undefined"（ブラウザでは "object"）
console.log(typeof process);   // "object"（Node.js固有のグローバルオブジェクト）
console.log(typeof document);  // "undefined"（DOMは存在しない）
```

`process` はNode.js固有のグローバルオブジェクトで、実行環境の情報や制御に使います。

| 機能 | ブラウザ | Node.js |
| --- | --- | --- |
| DOM操作 | ✓ | ✗ |
| ファイルシステム | ✗ | ✓ |
| HTTPサーバー | ✗ | ✓ |
| `window` | ✓ | ✗ |
| `process` | ✗ | ✓ |

## まとめ

このステップでは以下を学びました。

- `node <ファイル名>` でJavaScriptファイルをターミナルから実行できる
- REPLを使ってコードをその場で試せる
- Node.jsにはDOM（`window` / `document`）がなく、代わりにファイルシステムやHTTPサーバーなどのサーバーサイド機能がある

**次のステップ:** [02 モジュールシステム](../02-modules/README.md) では、Node.jsのモジュールシステムを学びます。

## 一次情報・参考資料

- [Node.js 公式サイト](https://nodejs.org/)
- [Node.js ドキュメント](https://nodejs.org/docs/latest/api/)
