# コールバック

## このステップのゴール

- 関数を値として別の関数に渡せます
- 処理の「タイミング」と「内容」を分離して柔軟なコードを書けます
- `addEventListener` や `setTimeout` などのコールバックを読み書きできます

## 前提知識・環境

- 03-errors を完了していること

## 実践

`index.html` を Live Server で開き、`main.js` にコードを書きながら進めます。

### 1. 関数を値として渡せることを理解する

JavaScriptでは関数は値の一種です。数値や文字列と同じように変数に代入したり、別の関数の引数として渡したりできます。引数として渡された関数を**コールバック関数**と呼びます。

まず関数を変数に代入して、値として扱えることを確認します。

```javascript
const greet = (name) => `こんにちは、${name}さん`;

console.log(greet);          // 関数オブジェクト自体
console.log(greet("Alice")); // 呼び出した結果
```

次に関数を別の関数の引数として渡します。`apply` は受け取った関数（コールバック）を呼び出す関数です。

```javascript
const apply = (fn, value) => fn(value);

console.log(apply(greet, "Bob"));
```

`greet` という関数を `apply` に渡し、`apply` の中で実行されることを確認します。

### 2. コールバックで処理の内容を呼び出し元から切り離せるようにする

コールバックを使うと、「何回繰り返すか」と「各回に何をするか」のように、処理の制御と内容を分離できます。内容だけを差し替えることで、同じ制御ロジックを再利用できます。

```javascript
const repeat = (count, callback) => {
  for (let i = 0; i < count; i++) {
    callback(i);
  }
};

repeat(3, (i) => console.log(`${i + 1}回目`));
repeat(3, (i) => console.log(i * 10));
```

同じ `repeat` に異なるコールバックを渡すことで、出力が変わることを確認します。

### 3. 配列メソッドのコールバックを使いこなす

`forEach` / `map` / `filter` はコールバックを受け取る配列メソッドです。「各要素に何をするか」をコールバックで渡します。コールバックを名前付き関数として切り出すと、処理の意図がより明確になります。

```javascript
const products = [
  { name: "ノート",   price: 150 },
  { name: "ペン",     price: 80  },
  { name: "消しゴム", price: 60  },
];

const formatProduct = (p) => `${p.name}: ¥${p.price}`;

products.forEach((p) => console.log(formatProduct(p)));

const affordable = products.filter((p) => p.price < 100);
console.log(affordable.map((p) => p.name));
```

### 4. コールバックが後から呼ばれるパターンに慣れる

コールバックは「今すぐ実行」ではなく「後で実行」されることがあります。`setTimeout` は指定した時間が経過したあとにコールバックを呼び出します。コールバックを渡した直後にそのコールバックが実行されるわけではないことを確認します。

```javascript
console.log("1. 登録");

setTimeout(() => {
  console.log("3. コールバック実行");
}, 1000);

console.log("2. 登録の直後");
```

この「後で呼ばれる」パターンは、DOMイベント（クリックされたとき）や非同期処理（通信が完了したとき）でも同じ仕組みです。

## まとめ

このステップでは以下を学びました。

- JavaScriptでは関数を変数に代入したり、引数として渡したりできる
- 引数として渡された関数をコールバック関数と呼ぶ
- コールバックで処理の制御と内容を分離し、柔軟に差し替えられる
- `forEach` / `map` / `filter` はコールバックを受け取る配列メソッド
- コールバックは今すぐではなく「後で」呼び出されることがある

**次のステップ:** [05 DOMセレクタ](../05-dom-selector/README.md) では、JavaScriptでHTMLの要素を取得・操作する方法を学びます。

## 一次情報・参考資料

- [MDN: コールバック関数](https://developer.mozilla.org/ja/docs/Glossary/Callback_function)
- [MDN: Array.prototype.forEach()](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- [MDN: setTimeout()](https://developer.mozilla.org/ja/docs/Web/API/Window/setTimeout)
