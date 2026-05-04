# ストリーム

## このステップのゴール

- 大きなファイルをメモリに乗せずに効率よく処理できます
- `createReadStream` / `createWriteStream` でファイルをストリームで処理できます
- `pipeline` でストリームを安全に接続できます

## 前提知識・環境

- 06-error-handling を完了していること

## 実践

`main.js` にコードを書きながら進めます。実行は `node main.js` です。

### 1. ストリームとは何か

`fs.promises.readFile` はファイル全体をメモリに読み込んでから処理します。数GBのファイルを処理する場合、メモリが不足することがあります。

ストリームはデータを小さなチャンク（断片）に分けて順次処理します。ファイル全体をメモリに載せる必要がなく、読み込みながら処理を進められます。

### 2. Readable ストリームでファイルを読む

`createReadStream` でファイルをストリームとして読み込めます。`highWaterMark` でチャンクサイズ（バイト）を指定できます。

```javascript
import { createReadStream } from "node:fs";
import { join } from "node:path";

const filePath = join(import.meta.dirname, "sample.txt");
const stream = createReadStream(filePath, {
  encoding: "utf-8",
  highWaterMark: 64,  // 64バイトずつ読み込む
});

stream.on("data", (chunk) => {
  console.log("チャンク:", chunk);
});

stream.on("end", () => {
  console.log("読み込み完了");
});
```

`data` イベントがチャンクごとに発火し、最後に `end` イベントが発火します。

### 3. Writable ストリームでファイルに書く

`createWriteStream` でファイルへの書き込みストリームを作成できます。`write()` でチャンクを書き込み、`end()` で完了します。

```javascript
import { createWriteStream } from "node:fs";
import { join } from "node:path";

const outputPath = join(import.meta.dirname, "output.txt");
const stream = createWriteStream(outputPath);

stream.write("1行目\n");
stream.write("2行目\n");
stream.end("3行目\n");

stream.on("finish", () => {
  console.log("書き込み完了");
});
```

### 4. pipeline でストリームを接続する

Readableの出力をWritableの入力に接続することをパイピングといいます。`stream/promises` の `pipeline` はエラー発生時に自動でクリーンアップするため、`pipe()` より安全です。

```javascript
import { createReadStream, createWriteStream } from "node:fs";
import { pipeline } from "node:stream/promises";
import { join } from "node:path";

const inputPath = join(import.meta.dirname, "sample.txt");
const outputPath = join(import.meta.dirname, "output.txt");

await pipeline(
  createReadStream(inputPath),
  createWriteStream(outputPath)
);

console.log("コピー完了");
```

`pipeline` の間に Transform ストリームを挿入することで、読み込みながら変換して書き込むといった処理を構成できます。

## まとめ

このステップでは以下を学びました。

- ストリームはデータをチャンク単位で処理するため、大きなファイルをメモリ効率よく処理できる
- `createReadStream` / `createWriteStream` でファイルをストリームとして扱える
- `stream/promises` の `pipeline` でストリームを安全に接続でき、エラー時のクリーンアップも自動で行われる

**次のステップ:** [08 パッケージマネージャー](../08-package-manager/README.md) では、npmによるパッケージ管理を学びます。

## 一次情報・参考資料

- [Node.js: Stream](https://nodejs.org/docs/latest/api/stream.html)
- [Node.js: stream/promises pipeline](https://nodejs.org/docs/latest/api/stream.html#streampipelinestreams-options)
- [Node.js: fs.createReadStream](https://nodejs.org/docs/latest/api/fs.html#fscreatereadstreampath-options)
