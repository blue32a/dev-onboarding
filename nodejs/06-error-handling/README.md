# エラーハンドリング

## このステップのゴール

- Node.js固有のエラーコード（`ENOENT` など）を理解して対処できます
- `EventEmitter` の `error` イベントを適切に処理できます
- `unhandledRejection` で未処理のPromiseエラーを検出できます

## 前提知識・環境

- 05-process-cli を完了していること
- `try` / `catch` と `async` / `await` を理解していること

## 実践

`main.js` にコードを書きながら進めます。実行は `node main.js` です。

### 1. Node.js固有のエラーコードを扱う

Node.jsのシステムエラーには `code` プロパティがあります。ファイルが存在しない場合は `ENOENT`（Error NO ENTry）が設定されます。

```javascript
import { readFile } from "node:fs/promises";

try {
  await readFile("存在しないファイル.txt", "utf-8");
} catch (err) {
  console.log(err.code);     // ENOENT
  console.log(err.message);  // no such file or directory: ...
}
```

エラーコードで分岐することで、状況に応じた処理ができます。

```javascript
import { readFile, writeFile } from "node:fs/promises";
import { join } from "node:path";

const filePath = join(import.meta.dirname, "config.json");

try {
  const content = await readFile(filePath, "utf-8");
  console.log("設定を読み込みました:", content);
} catch (err) {
  if (err.code === "ENOENT") {
    console.log("設定ファイルが見つかりません。デフォルト設定を作成します。");
    await writeFile(filePath, JSON.stringify({ version: 1 }, null, 2));
  } else {
    throw err;
  }
}
```

`ENOENT` 以外の予期しないエラーは `throw` で再スローします。

主なエラーコード：

| コード | 意味 |
| --- | --- |
| `ENOENT` | ファイル・ディレクトリが存在しない |
| `EEXIST` | すでに存在する |
| `EACCES` | アクセス権限がない |
| `EADDRINUSE` | ポートがすでに使用中 |

### 2. EventEmitter の error イベント

`EventEmitter` は `error` イベントを特別に扱います。`error` イベントのリスナーが登録されていない状態でエラーが発生すると、プロセスがクラッシュします。

```javascript
import { EventEmitter } from "node:events";

const emitter = new EventEmitter();

// error リスナーを登録していない状態でエラーを発生させる
// emitter.emit("error", new Error("未処理のエラー"));  // プロセスがクラッシュする

// error リスナーを登録する
emitter.on("error", (err) => {
  console.log("エラーをキャッチしました:", err.message);
});

emitter.emit("error", new Error("エラーが発生しました"));
// エラーをキャッチしました: エラーが発生しました
```

ストリームや `http.createServer()` のようなNode.jsの組み込みクラスも `EventEmitter` を継承しています。本番コードでは `error` リスナーを必ず登録します。

### 3. 未処理の Promise エラーを検出する

`await` し忘れたPromiseがRejectされると、エラーが握りつぶされる場合があります。`unhandledRejection` イベントで検出できます。

```javascript
process.on("unhandledRejection", (reason) => {
  console.error("未処理のPromiseエラー:", reason);
  process.exit(1);
});

// await を忘れた Promise
Promise.reject(new Error("このエラーは処理されない"));
```

現代のNode.jsでは未処理のRejectionはデフォルトでプロセスを終了させます。`unhandledRejection` を登録することで、終了前にログ出力などの後処理ができます。

## まとめ

このステップでは以下を学びました。

- Node.jsのシステムエラーには `code` プロパティがあり、`ENOENT` などで状況を判別できる
- `EventEmitter` の `error` イベントはリスナーがないとプロセスがクラッシュするため、必ず登録する
- `process.on("unhandledRejection", ...)` で未処理のPromiseエラーを検出できる

**次のステップ:** [07 ストリーム](../07-streams/README.md) では、大きなデータを効率的に処理するストリームを学びます。

## 一次情報・参考資料

- [Node.js: Error クラス](https://nodejs.org/docs/latest/api/errors.html)
- [Node.js: EventEmitter](https://nodejs.org/docs/latest/api/events.html#class-eventemitter)
- [Node.js: process イベント](https://nodejs.org/docs/latest/api/process.html#process-events)
