# モジュールシステム

## このステップのゴール

- CommonJSの `require` / `module.exports` でモジュールを分割できます
- Node.js組み込みモジュールをインポートして使えます
- ES ModulesとCommonJSの違いと使い分けを理解できます

## 前提知識・環境

- 01-setup を完了していること
- JavaScriptのES Modules（`import` / `export`）を理解していること

## 実践

`main.js` にコードを書きながら進めます。実行は `node main.js` です。

### 1. CommonJSでモジュールを分割する

Node.jsのデフォルトのモジュールシステムはCommonJS（CJS）です。`module.exports` でモジュールの外に公開し、`require()` で読み込みます。

`utils.js` を作成します。

```javascript
function formatPrice(price) {
  return `¥${price.toLocaleString()}`;
}

const TAX_RATE = 0.1;

module.exports = { formatPrice, TAX_RATE };
```

`main.js` から読み込みます。

```javascript
const { formatPrice, TAX_RATE } = require("./utils.js");

console.log(formatPrice(1980)); // ¥1,980
console.log(TAX_RATE);          // 0.1
```

`node main.js` で実行して確認します。

### 2. 組み込みモジュールを使う

Node.jsには多数の組み込みモジュールが用意されています。`require()` でパスを指定せず名前だけで読み込めます。

```javascript
const os = require("os");
const path = require("path");

console.log(os.platform());  // "win32" / "darwin" / "linux"
console.log(os.homedir());   // ホームディレクトリのパス
console.log(path.sep);       // パス区切り文字（"/" または "\\"）
```

### 3. ES ModulesをNode.jsで使う

ブラウザと同じ `import` / `export` 構文をNode.jsでも使えます。`package.json` に `"type": "module"` を追加することで有効になります。

同じディレクトリに `package.json` を作成します。

```json
{
  "type": "module"
}
```

`main.js` を書き換えます。

```javascript
import os from "node:os";
import path from "node:path";

console.log(os.platform());
console.log(path.sep);
```

`node:` プレフィックスは組み込みモジュールであることを明示する書き方です（省略可ですが、明示が推奨されます）。

### 4. CommonJSとES Modulesの違いを理解する

| 項目 | CommonJS | ES Modules |
| --- | --- | --- |
| 構文 | `require` / `module.exports` | `import` / `export` |
| Node.jsのデフォルト | ✓ | ✗（`"type": "module"` が必要） |
| ブラウザとの共通構文 | ✗ | ✓ |
| `__dirname` / `__filename` | ✓ | ✗（`import.meta.dirname` を使う） |

既存のNode.jsコードやnpmパッケージにはCommonJSが多く使われています。新規プロジェクトではES Modulesが主流です。このコンテンツ以降のステップではES Modulesを使います。

## まとめ

このステップでは以下を学びました。

- CommonJSは `require()` / `module.exports` で、既存のNode.jsコードの大半で使われている
- ES ModulesはブラウザJavaScriptと同じ構文で、`package.json` に `"type": "module"` を追加することで使える
- 組み込みモジュールは `require("node:モジュール名")` または `import ... from "node:モジュール名"` で使える

**次のステップ:** [03 ファイル操作](../03-files/README.md) では、Node.jsでファイルの読み書きを行います。

## 一次情報・参考資料

- [Node.js: CommonJS modules](https://nodejs.org/docs/latest/api/modules.html)
- [Node.js: ES modules](https://nodejs.org/docs/latest/api/esm.html)
- [Node.js 組み込みモジュール一覧](https://nodejs.org/docs/latest/api/)
