# ファイル操作

## このステップのゴール

- `fs.promises` でファイルを非同期に読み書きできます
- `path` モジュールでパスを安全に組み立てられます
- `import.meta.dirname` でスクリプトの場所を基準にパスを解決できます

## 前提知識・環境

- 02-modules を完了していること
- `async` / `await` の基本を理解していること

## 実践

`main.js` にコードを書きながら進めます。実行は `node main.js` です。

### 1. ファイルを読む

`fs.promises` はファイル操作の非同期APIです。`await` で結果を受け取れます。

```javascript
import { readFile } from "node:fs/promises";
import { join } from "node:path";

const filePath = join(import.meta.dirname, "sample.txt");
const content = await readFile(filePath, "utf-8");
console.log(content);
```

`import.meta.dirname` は実行中のファイルがあるディレクトリのパスです。これを基準に `join()` でパスを組み立てることで、どのディレクトリから実行しても正しいパスを参照できます。

`sample.txt` の内容がターミナルに出力されることを確認します。

### 2. ファイルに書く

`writeFile` でファイルに文字列を書き込めます。ファイルが存在しない場合は新規作成、存在する場合は上書きされます。

```javascript
import { writeFile, readFile } from "node:fs/promises";
import { join } from "node:path";

const outputPath = join(import.meta.dirname, "output.txt");

await writeFile(outputPath, "書き込みのテスト\n");
console.log("書き込み完了");

const content = await readFile(outputPath, "utf-8");
console.log(content);
```

実行後、`output.txt` が作成されていることを確認します。

### 3. ディレクトリを操作する

`mkdir` でディレクトリを作成できます。`{ recursive: true }` を指定すると、すでに存在する場合もエラーにならず、途中のディレクトリも同時に作成されます。

`readdir` でディレクトリ内のファイル一覧を取得できます。

```javascript
import { mkdir, writeFile, readdir } from "node:fs/promises";
import { join } from "node:path";

const dirPath = join(import.meta.dirname, "work");
await mkdir(dirPath, { recursive: true });

await writeFile(join(dirPath, "a.txt"), "ファイルA");
await writeFile(join(dirPath, "b.txt"), "ファイルB");

const files = await readdir(dirPath);
console.log(files); // [ 'a.txt', 'b.txt' ]
```

### 4. path モジュールを使う

`path` モジュールはパス文字列を操作するユーティリティです。OSによってパス区切り文字が異なるため（Windows は `\`、macOS/Linux は `/`）、文字列連結ではなく `path` モジュールを使います。

```javascript
import { join, basename, extname, dirname } from "node:path";

const filePath = join("/users", "alice", "document.txt");
console.log(filePath);               // /users/alice/document.txt
console.log(basename(filePath));     // document.txt
console.log(extname(filePath));      // .txt
console.log(dirname(filePath));      // /users/alice
```

## まとめ

このステップでは以下を学びました。

- `fs.promises` の `readFile` / `writeFile` / `mkdir` / `readdir` でファイルシステムを非同期に操作できる
- `import.meta.dirname` でスクリプトのディレクトリを取得し、`path.join` でパスを組み立てる
- `path` モジュールはOS依存のパス区切りを吸収してくれる

**次のステップ:** [04 HTTPサーバー](../04-http-server/README.md) では、Node.jsでHTTPサーバーを作成します。

## 一次情報・参考資料

- [Node.js: fs.promises](https://nodejs.org/docs/latest/api/fs.html#promises-api)
- [Node.js: path](https://nodejs.org/docs/latest/api/path.html)
- [Node.js: import.meta.dirname](https://nodejs.org/docs/latest/api/esm.html#importmetadirname)
