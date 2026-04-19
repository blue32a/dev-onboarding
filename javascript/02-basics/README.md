# JavaScriptの基本構文

## このステップのゴール

- データを変数に保存して使い回せます
- 条件によって処理を分岐させたり、繰り返し実行できます
- 処理をまとめて関数として定義し、再利用できます
- 複数のデータをまとめて配列・オブジェクトで管理できます

## 前提知識・環境

- 01-setup を完了していること

## 実践

`index.html` を Live Server で開き、`main.js` にコードを書きながら進めます。コードを保存するたびにブラウザがリロードされ、Console に結果が表示されます。

### 1. 値を変数に保存して後から参照・再利用できるようにする

値に名前をつけて変数に保存することで、後から何度でも参照・再利用できます。変数宣言には3種類あります。`const` は再代入できない定数、`let` は再代入できる変数を宣言します。`var` という古い書き方もありますが、スコープの扱いがバグの原因になりやすいため、現代では `let` / `const` を使います。意図せず値を書き換えてしまうバグを防ぐため、特に理由がなければ `const` を使うのが基本です。

テンプレートリテラル（バッククォートで囲む書き方）を使うと、文字列の中に変数を `${}` で埋め込んで整形できます。

```javascript
const productName = "ノート";
const price = 150;

console.log(`${productName}: ¥${price}`);
```

`productName = "ペン"` と書き換えてみましょう。`const` に再代入しようとするとエラーになります。次に `const` を `let` に変えると再代入できることを確認します。

### 2. 変数の型を把握してデバッグに役立てる

JavaScriptは変数宣言時に型を指定しません。`typeof` を使うと値の型を確認できます。`null` の型が予想と異なる点は歴史的な仕様です。

```javascript
console.log(typeof productName); // "string"
console.log(typeof price); // "number"
console.log(typeof null); // "object"（歴史的な仕様）
console.log(typeof undefined); // "undefined"
```

### 3. 条件によって処理を変えられるようにする

`if / else` を使うと、条件によって実行する処理を変えられます。条件の比較には `===`（型も含めて一致するか）を使います。`==` は型を変換して比較するため、予期しない動作につながることがあります。

```javascript
const inStock = true;

if (inStock) {
  console.log("購入できます");
} else {
  console.log("在庫切れです");
}
```

`inStock` を `false` に変えて、結果が変わることを確認します。また `1 === 1`・`1 === "1"`・`1 == "1"` をそれぞれ `console.log` で確認しましょう。

### 4. 繰り返し処理でコードの重複をなくす

同じ処理を複数回書くと管理が難しくなります。ループを使うと、データが増えてもコードを変えずに対応できます。`for...of` は配列の要素を順に取り出す書き方で、インデックスが不要な場合に使います。インデックスが必要な場合は従来の `for` ループを使います。

```javascript
const items = ["ノート", "ペン", "消しゴム", "定規", "ホッチキス"];

// 要素のみ使う場合
for (const item of items) {
  console.log(item);
}

// インデックスが必要な場合
for (let i = 0; i < items.length; i++) {
  console.log(`${i + 1}番目: ${items[i]}`);
}
```

### 5. 処理を関数にまとめて再利用できるようにする

同じ処理を複数の場所に書くと、仕様変更のときに全箇所を修正する必要が生じます。関数にまとめておくと変更箇所が1か所になります。

```javascript
function calcTax(price) {
  return price * 1.1;
}

console.log(calcTax(150));
console.log(calcTax(80));
```

現代のJavaScriptではアロー関数という短い書き方が広く使われています。同じ意味のコードです。

```javascript
const calcTax = (price) => price * 1.1;
```

### 6. 配列メソッドでデータを変換・絞り込めるようにする

`map` は各要素を変換した新しい配列、`filter` は条件に合う要素だけの新しい配列を返します。いずれも元の配列は変えません。

```javascript
const prices = [150, 80, 200];

const withTax = prices.map((p) => calcTax(p));
console.log(withTax);

const expensive = prices.filter((p) => p >= 100);
console.log(expensive);
```

### 7. 関連するデータをオブジェクトでひとまとめに管理する

関連するデータを別々の変数で管理すると、追加・削除のたびに複数の変数を操作しなければなりません。オブジェクトにまとめると1つの変数で扱えます。プロパティへのアクセスはドット記法（`user.name`）とブラケット記法（`user["name"]`）の2通りがあります。

```javascript
const products = [
  { name: "ノート", price: 150 },
  { name: "ペン", price: 80 },
  { name: "消しゴム", price: 60 },
];

products.forEach((p) => console.log(`${p.name}: ¥${p.price}`));
```

## まとめ

このステップでは以下を学びました。

- `const` / `let` で変数を宣言し、再代入が不要なら `const` を使うのが基本
- `if / else` で処理を分岐できる
- `for...of` で配列の要素を順に処理できる
- 関数にまとめることで処理を再利用できる
- 配列と `map` / `filter` でデータを変換・絞り込みできる
- オブジェクトで関連するデータをひとまとめにできる

**次のステップ:** [03 エラーの読み方](../03-errors/README.md) では、エラーメッセージの読み方と問題解決のアプローチを学びます。

## 一次情報・参考資料

- [MDN: JavaScriptの基礎](https://developer.mozilla.org/ja/docs/Learn_web_development/Core/Scripting)
- [MDN: 配列](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [MDN: オブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Object)
