# エラーの読み方と解決のアプローチ

## この技術で何ができるか

- エラーメッセージから原因箇所を特定できます
- よく遭遇するエラーの種類と発生パターンを把握できます
- エラーを手がかりにして系統的に問題を解決できます

## 前提知識・環境

- 02-basics を完了していること

## ハンズオン

`index.html` を Live Server で開き、`main.js` にコードを書きながら進めます。

### a. エラーメッセージを正確に読んで原因箇所を特定できるようにする

コードが動かないとき、まず確認すべきはコンソールのエラーメッセージです。エラーには必ず「種類」「内容」「発生した場所」が含まれており、そのまま原因を探す手がかりになります。

以下のコードを書いて保存し、エラーが出力されることを確認します。

```javascript
console.log(message);
```

コンソールに表示されたエラーを読みます。

- 最初の単語（`ReferenceError`）がエラーの**種類**です
- `:` 以降（`message is not defined`）がエラーの**内容**です
- 右端の `main.js:1` が**ファイル名と行番号**です

エラーメッセージを読むと、`message` という変数が定義されていないことが原因だとわかります。変数を宣言してから使うよう修正します。

```javascript
const message = "hello";
console.log(message);
```

エラーが消えて値が表示されることを確認します。

### b. よく遭遇するエラーの種類を把握して原因を絞り込めるようにする

エラーの種類（名前）はそのまま原因の分類を示しています。代表的な3種類を実際に発生させて読んでみましょう。**1つずつ書いては確認する**形で進めます。

```javascript
// ReferenceError: 存在しない変数・関数を参照したとき
console.log(undeclaredVariable);
```

```javascript
// TypeError: 値の型に対して不正な操作をしたとき（null や undefined にアクセスするなど）
const user = null;
console.log(user.name);
```

```javascript
// SyntaxError: コードの構文が正しくないとき（実行前に検出される）
const items = [1, 2,;
```

`SyntaxError` はコードが実行される前に検出されるため、ファイル全体が動かなくなります。エラーを確認したら構文を直しておきましょう。

### c. エラーを手がかりにして解決するまでの流れを体験する

エラーの解決は「読む → 場所を特定する → 原因を理解する → 修正する → 確認する」という流れを繰り返します。以下のコードを実行して、エラーまたはおかしな結果を確認し、原因を探して修正してみましょう。

```javascript
const products = [
  { name: "ノート",   price: 150 },
  { name: "ペン",     price: 80  },
  { name: "消しゴム", price: 60  },
];

const total = products.reduce((sum, p) => sum + p.pirce, 0);
console.log(`合計: ¥${total}`);
```

エラーが出ない場合でも、`total` の値が正しいかどうか確認することが大切です。エラーにならないバグ（`pirce` のようなタイポによる `undefined` の混入）があることを覚えておきましょう。

## まとめ

このステップでは以下を学びました。

- エラーメッセージには「種類」「内容」「ファイル名と行番号」が含まれている
- `ReferenceError`（変数未定義）・`TypeError`（型の不正操作）・`SyntaxError`（構文エラー）が代表的なエラー
- エラーにならないバグもあるため、値の確認も重要
- エラーの解決は「読む → 場所を特定 → 原因を理解 → 修正 → 確認」の繰り返し

**次のステップ:** [04 コールバック](../04-callback/) では、関数を値として渡す仕組みと、DOMイベントや非同期処理の土台となるコールバックパターンを学びます。

## 一次情報・参考資料

- [MDN: JavaScript エラーリファレンス](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Errors)
- [MDN: ReferenceError](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/ReferenceError)
- [MDN: TypeError](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/TypeError)
