# JSX

## このステップのゴール

- JSXでUIの構造を記述できます
- HTMLとJSXの違いを使い分けられます
- JSXの中でJavaScript式を埋め込めます

## 前提知識・環境

- 01-setup を完了していること

## 実践

`workspace/app/` で開発サーバーを起動した状態で進めます（`npm run dev`）。`src/App.jsx` を編集します。

### 1. App.jsxを書き換える

`src/App.jsx` の内容を以下に書き換えます。

```jsx
function App() {
  return (
    <div>
      <h1>Hello, React!</h1>
    </div>
  );
}

export default App;
```

ブラウザに「Hello, React!」と表示されることを確認します。

### 2. HTMLとJSXの違いを確認する

JSXはHTMLに似ていますが、いくつかの違いがあります。

**`class` → `className`**

`class` はJavaScriptの予約語のため、JSXでは `className` を使います。

```jsx
// HTML
<div class="container">...</div>

// JSX
<div className="container">...</div>
```

**空要素は自己閉じタグにする**

```jsx
<br />
<input type="text" />
<img src="photo.jpg" alt="写真" />
```

**ルート要素は1つにする**

JSXのreturnには1つのルート要素が必要です。複数の要素を返したいときはフラグメント（`<> </>`）で包みます。

```jsx
// エラー: 2つのルート要素がある
return (
  <h1>タイトル</h1>
  <p>本文</p>
);

// OK: フラグメントで包む
return (
  <>
    <h1>タイトル</h1>
    <p>本文</p>
  </>
);
```

### 3. JavaScript式を埋め込む

`{}` を使うとJavaScriptの式を埋め込めます。`{}` に入れられるのは式（値を返すもの）のみです。`if` 文や `for` 文は使えません。

```jsx
function App() {
  const name = "React";
  const isLoggedIn = true;

  return (
    <>
      <h1>Hello, {name}!</h1>
      <p>現在時刻: {new Date().toLocaleTimeString()}</p>
      {isLoggedIn && <p>ログイン中です</p>}
      {isLoggedIn ? <p>ログアウト</p> : <p>ログイン</p>}
    </>
  );
}

export default App;
```

条件付きレンダリングには `&&`（条件が真のときだけ表示）や三項演算子を使います。

## まとめ

- `class` は `className`、空要素は自己閉じタグ、ルート要素は1つ
- `{}` でJavaScript式を埋め込める
- 条件付きレンダリングには `&&` や三項演算子を使う

**次のステップ:** [03 コンポーネント](../03-components/README.md) では、UIを部品として分割する方法を学びます。

## 一次情報・参考資料

- [React: JSXでマークアップを記述する](https://ja.react.dev/learn/writing-markup-with-jsx)
- [React: JSXに中括弧でJavaScriptを含める](https://ja.react.dev/learn/javascript-in-jsx-with-curly-braces)
