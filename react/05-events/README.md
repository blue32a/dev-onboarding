# イベント

## このステップのゴール

- クリックなどのイベントをハンドリングできます
- イベントオブジェクトからフォームの入力値を取得できます

## 前提知識・環境

- 04-props を完了していること

## 実践

`workspace/app/` で開発サーバーを起動した状態で進めます（`npm run dev`）。`src/App.jsx` を編集します。

### 1. クリックイベントを処理する

`onClick` にイベントハンドラ関数を渡します。

```jsx
function App() {
  function handleClick() {
    console.log("クリックされました");
  }

  return <button onClick={handleClick}>クリック</button>;
}

export default App;
```

ボタンをクリックするたびにコンソールにメッセージが表示されることを確認します。

`onClick={handleClick}` と書きます。`onClick={handleClick()}` のように `()` を付けると、クリック時ではなくレンダリング時に実行されてしまうため注意します。

### 2. フォームの入力値を取得する

イベントハンドラの引数 `e`（イベントオブジェクト）から入力値を取得できます。

```jsx
function App() {
  function handleChange(e) {
    console.log(e.target.value);
  }

  return <input type="text" onChange={handleChange} />;
}

export default App;
```

テキストボックスに入力するたびにコンソールに入力値が表示されることを確認します。

## まとめ

- `onClick` などのイベントハンドラに関数を渡す。`()` を付けずに渡すことに注意
- イベントオブジェクト `e` から `e.target.value` で入力値を取得できる

**次のステップ:** [06 state](../06-state/README.md) では、イベントと組み合わせてUIを動的に更新する状態管理を学びます。

## 一次情報・参考資料

- [React: イベントへの応答](https://ja.react.dev/learn/responding-to-events)
