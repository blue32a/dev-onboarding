# DOMセレクタ

## このステップのゴール

- HTMLの要素をJavaScriptから取得できます
- 取得した要素のテキスト・スタイル・クラスを変更できます
- 複数の要素をまとめて操作できます

## 前提知識・環境

- 04-callback を完了していること
- HTMLの基本的な構造（タグ・id・class属性）を知っていること

## 実践

`index.html` を Live Server で開き、`main.js` にコードを書きながら進めます。

### 1. DOM操作の対象となる要素を取得できるようにする

ブラウザはHTMLを読み込むと、各要素をツリー状のオブジェクト（DOMツリー）として保持します。JavaScriptはこのオブジェクトを通じてHTMLを読み書きします。

`document.querySelector()` はCSSセレクタの書き方で要素を取得します。`#id`・`.class`・`タグ名` など、CSSと同じセレクタが使えます。

```javascript
const title = document.querySelector("#title");
console.log(title);

const firstItem = document.querySelector(".item");
console.log(firstItem);
```

> Console に表示された要素をクリックすると、**Elements** タブで対応するHTMLがハイライトされます。

### 2. 複数の要素をまとめて取得・処理できるようにする

`querySelectorAll()` はセレクタに一致するすべての要素をNodeListとして返します。`forEach` で繰り返すと、全件に同じ処理を適用できます。

```javascript
const items = document.querySelectorAll(".item");
console.log(items.length);
items.forEach(item => console.log(item.textContent));
```

### 3. JavaScriptからページの表示内容を動的に書き換える

取得した要素の `textContent` プロパティを書き換えることで、ページに表示されているテキストをリロードせずに変更できます。これがDOMを通じた動的なUI変更の基本操作です。

```javascript
const title = document.querySelector("#title");
title.textContent = "タイトルを変更しました";
```

### 4. JavaScriptから要素の見た目を動的に制御する

`style` プロパティを使うとインラインスタイルを直接変更できます。ユーザーのアクションや状態に応じて見た目を変えたい場面で使います。`classList` を使うとCSSクラスの追加・削除・切り替えができます。

```javascript
title.style.color = "royalblue";
title.style.fontSize = "2rem";

const desc = document.querySelector(".description");
desc.classList.add("highlight");
console.log(desc.classList);
```

### 5. 動的に要素を生成してページに追加できるようにする

`createElement()` で新しい要素を作り、`appendChild()` で既存の要素に追加できます。APIから取得したデータをリスト表示するなど、以降のステップで繰り返し使うパターンです。

```javascript
const list = document.querySelector("#fruit-list");
const li = document.createElement("li");
li.textContent = "ぶどう";
list.appendChild(li);
```

## まとめ

このステップでは以下を学びました。

- `querySelector` / `querySelectorAll` でHTMLの要素を取得できる
- `textContent` や `style`、`classList` で要素の内容・見た目を変更できる
- `createElement` と `appendChild` で新しい要素を動的に追加できる

**次のステップ:** [06 DOMイベント](../06-dom-events/README.md) では、クリックや入力などのユーザー操作に反応する処理の書き方を学びます。

## 一次情報・参考資料

- [MDN: Document.querySelector()](https://developer.mozilla.org/ja/docs/Web/API/Document/querySelector)
- [MDN: Document.querySelectorAll()](https://developer.mozilla.org/ja/docs/Web/API/Document/querySelectorAll)
- [MDN: Element.classList](https://developer.mozilla.org/ja/docs/Web/API/Element/classList)
