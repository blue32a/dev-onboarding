# npm scripts

## このステップのゴール

- `scripts` フィールドにコマンドを登録して `npm run` で実行できます
- `start`・`test` などの特別なスクリプト名を理解できます
- プロジェクトの実行手順を npm scripts に集約する意義を説明できます

## 前提知識・環境

- 03-dependencies を完了していること

## 実践

### 1. npm scripts を登録する

`package.json` の `scripts` フィールドにコマンドを登録できます。

```json
{
  "type": "module",
  "scripts": {
    "start": "node main.js",
    "dev": "node --watch main.js"
  }
}
```

`npm run <スクリプト名>` で実行します。

```
npm run dev
```

`node --watch` はファイルの変更を検知して自動でプロセスを再起動するオプションです。

### 2. 特別なスクリプト名

`start` と `test` は特別なスクリプト名で、`run` を省略して実行できます。

```
npm start   # npm run start と同じ
npm test    # npm run test と同じ
```

よく使われるスクリプト名の慣習：

| スクリプト名 | 用途 |
| --- | --- |
| `start` | アプリケーションの起動 |
| `dev` | 開発用サーバーの起動（ウォッチモードなど） |
| `test` | テストの実行 |
| `build` | ビルド処理（TypeScriptのコンパイルなど） |
| `lint` | コード静的解析 |

### 3. npm scripts を使う意義

長いコマンドやオプションをスクリプトに登録しておくことで：

- チームメンバーが `npm start` だけで起動できる
- コマンドの詳細を覚えなくてよい
- `package.json` を見れば何ができるかわかる

プロジェクトに参加したときは、まず `package.json` の `scripts` を確認する習慣をつけると良いです。

## まとめ

- `scripts` フィールドにコマンドを登録し、`npm run <名前>` で実行できる
- `start`・`test` は `run` を省略できる特別なスクリプト名
- npm scripts にコマンドを集約することで、チームの実行手順を統一できる

## 一次情報・参考資料

- [npm scripts](https://docs.npmjs.com/cli/v10/using-npm/scripts)
- [npm run](https://docs.npmjs.com/cli/v10/commands/npm-run-script)
