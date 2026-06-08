# useEffect

## このステップのゴール

- useEffectでコンポーネントのマウント時に処理を実行できます
- APIからデータを取得して表示できます

## 前提知識・環境

- 07-list を完了していること

## 実践

`src/App.jsx` を編集します。

### 1. レンダリング中にAPIフェッチできない問題

`src/App.jsx` を以下に書き換えます。

```jsx
import { useState } from "react";

function App() {
  const [todos, setTodos] = useState([]);

  fetch("https://jsonplaceholder.typicode.com/todos?_limit=5")
    .then((res) => res.json())
    .then((data) => setTodos(data));

  return (
    <ul>
      {todos.map((todo) => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  );
}

export default App;
```

ブラウザの開発者ツール（F12）のNetworkタブを開きます。リクエストが止まらず繰り返されていることを確認します。

stateが更新されると再レンダリングが起き、再レンダリングのたびにフェッチが実行され、さらにstateが更新されるという無限ループになっています。確認できたら、ターミナルで `Ctrl+C` を押して開発サーバーを停止します。

### 2. useEffectの基本

ターミナルで `npm run dev` を実行して開発サーバーを再起動します。`src/App.jsx` を以下に書き換えます。

```jsx
import { useState, useEffect } from "react";

function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("レンダリング後に実行されます");
  });

  return (
    <>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </>
  );
}

export default App;
```

ボタンをクリックするたびにコンソールにメッセージが表示されることを確認します。

`useEffect` はデフォルトでレンダリングのたびに実行されます。**第2引数に空配列 `[]` を渡すとマウント時のみ実行されます**。

```jsx
useEffect(() => {
  console.log("マウント時のみ実行されます");
}, []);
```

### 3. APIからデータを取得する

`useEffect` の中でデータを取得し、stateに保存します。

```jsx
import { useState, useEffect } from "react";

function App() {
  const [todos, setTodos] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((res) => res.json())
      .then((data) => setTodos(data));
  }, []);

  return (
    <ul>
      {todos.map((todo) => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  );
}

export default App;
```

ページを読み込んだとき、APIからデータが取得されリストが表示されることを確認します。

## まとめ

- `useEffect` はレンダリング後に実行される
- 第2引数に `[]` を渡すとマウント時のみ実行される
- `useEffect` の中でAPIからデータを取得し、stateに保存する

## 一次情報・参考資料

- [React: useEffect](https://ja.react.dev/reference/react/useEffect)
- [React: Effectで同期する](https://ja.react.dev/learn/synchronizing-with-effects)
