# モジュール

## この技術で何ができるか

- コードを複数のファイルに分割して管理しやすくできます
- 関数や定数を別ファイルからインポートして再利用できます
- グローバルスコープの汚染を防ぎ、名前の衝突を避けられます

## 前提知識・環境

- 02-basics を完了していること
- Live Server で開いていること（`file://` では ES Modules は動作しません）

## ハンズオン

`index.html` を Live Server で開き、`utils.js` と `main.js` にコードを書きながら進めます。

### a. ファイルを分割して責務ごとにコードを管理できるようにする

1つのファイルにすべての処理を書いていると、ファイルが長くなるにつれて見通しが悪くなります。`export` をつけることで、そのファイルの外からも使える関数や定数を定義できます。責務ごとにファイルを分けることで、それぞれが何をするファイルかが明確になります。

`utils.js` に以下を書きます。

```javascript
export const TAX_RATE = 0.1;

export function formatPrice(price) {
  return `¥${price.toLocaleString()}`;
}
```

### b. 別ファイルのコードをimportして利用できるようにする

`export` しただけでは他のファイルから使えません。`import` することで、分割したファイルの関数や定数を呼び出せるようになります。`import` では `{}` の中に使いたい名前を列挙します（named import）。

ES Modules を使うには、HTMLの `<script>` タグに `type="module"` が必要です（`index.html` には設定済みです）。

`main.js` に以下を書き、ページに価格が表示されることを確認します。

```javascript
import { formatPrice, TAX_RATE } from "./utils.js";

const price = 1980;
const tax   = price * TAX_RATE;
const total = price + tax;

document.querySelector("#price").textContent = formatPrice(price);
document.querySelector("#tax").textContent   = formatPrice(tax);
document.querySelector("#total").textContent = formatPrice(total);
```

### c. モジュールに機能を追加して複数箇所から再利用できるようにする

モジュールに機能を追加すると、import している側でも使えるようになります。税込価格を計算する関数を `utils.js` に追加して、`main.js` から使ってみましょう。

```javascript
// utils.js に追加
export function withTax(price) {
  return price * (1 + TAX_RATE);
}
```

`main.js` の import に `withTax` を追加し、計算に使ってみます。

### d. default exportの使い方を理解してnamed exportと使い分けられるようにする

named export（`export function`）は複数の関数・定数をひとつのファイルから export するのに使います。一方、`export default` はファイルの「主役」となるひとつのものに使います。import 側では `{}` なしで好きな名前をつけられます。

新しいファイル `greet.js` を作成します。

```javascript
// greet.js
export default function greet(name) {
  return `こんにちは、${name}さん`;
}
```

`main.js` で import して確認します。

```javascript
import greet from "./greet.js";
console.log(greet("Alice"));
```

## まとめ

このステップでは以下を学びました。

- `export` で関数・定数を他のファイルから使えるようにできる
- `import { ... } from` で named export を取り込める
- `export default` でファイルの主役を定義し、import 側で自由に名前をつけられる
- ES Modules を使うには `<script type="module">` が必要

**次のステップ:** JavaScriptの全ステップはここで完了です。

## 一次情報・参考資料

- [MDN: export](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/export)
- [MDN: import](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/import)
- [MDN: JavaScript モジュール](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Modules)
