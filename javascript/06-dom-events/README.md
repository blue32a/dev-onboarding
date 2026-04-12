# DOMイベント

## この技術で何ができるか

- ボタンクリックや文字入力などのユーザー操作に反応する処理を書けます
- フォームの送信をJavaScriptで制御できます
- イベントが発生した要素の情報を取得できます

## 前提知識・環境

- 05-dom-selector を完了していること

## ハンズオン

`index.html` を Live Server で開き、`main.js` にコードを書きながら進めます。

### a. ユーザーのクリック操作を起点に処理を実行できるようにする

`addEventListener(イベント名, コールバック関数)` を使うと、指定したイベントが発生したときに処理を実行できます。クリックのたびに状態を更新してDOMに反映するのは、インタラクティブなUIの基本パターンです。

```javascript
const btn = document.querySelector("#increment-btn");
const countEl = document.querySelector("#count");
let count = 0;

btn.addEventListener("click", () => {
  count++;
  countEl.textContent = count;
});
```

### b. テキスト入力の内容をリアルタイムに処理できるようにする

`input` イベントはキー入力のたびに発火します。コールバック関数の第1引数にはイベントオブジェクト（`e`）が渡され、`e.target` でイベントが発生した要素を、`e.target.value` で入力値を取得できます。

```javascript
const input = document.querySelector("#name-input");
const display = document.querySelector("#input-display");

input.addEventListener("input", (e) => {
  display.textContent = e.target.value;
});
```

### c. フォームのデフォルト動作を制御してJavaScriptで処理できるようにする

フォームを送信するとデフォルトではページがリロードされ、JavaScriptの処理が中断してしまいます。`e.preventDefault()` でデフォルト動作を止めることで、入力値をJavaScript側で自由に扱えます。

まず `e.preventDefault()` なしで送信してページがリロードされることを確認します。次に以下のコードを書きます。

```javascript
const form = document.querySelector("#search-form");
const searchInput = document.querySelector("#search-input");
const result = document.querySelector("#search-result");

form.addEventListener("submit", (e) => {
  e.preventDefault();
  result.textContent = `「${searchInput.value}」で検索しました`;
});
```

## まとめ

このステップでは以下を学びました。

- `addEventListener` でユーザー操作に反応する処理を登録できる
- イベントオブジェクト（`e`）から発生した要素や入力値を取得できる
- `e.preventDefault()` でフォームのデフォルト動作（ページリロード）を止められる

**次のステップ:** [07 非同期処理](../07-async/) では、通信やタイマーなど時間のかかる処理を扱うための非同期処理の仕組みを学びます。

## 一次情報・参考資料

- [MDN: addEventListener](https://developer.mozilla.org/ja/docs/Web/API/EventTarget/addEventListener)
- [MDN: イベントリファレンス](https://developer.mozilla.org/ja/docs/Web/Events)
- [MDN: Event.preventDefault()](https://developer.mozilla.org/ja/docs/Web/API/Event/preventDefault)
