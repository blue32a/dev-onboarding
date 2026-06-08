# state

## このステップのゴール

- useStateで状態を持つコンポーネントを作れます
- 状態の変化でUIが自動更新されることを確認できます
- フォームの入力値をstateで管理できます

## 前提知識・環境

- 05-events を完了していること

## 実践

`src/App.jsx` を編集します。

### 1. 通常の変数では画面が更新されない

ボタンをクリックしてカウントを増やすコードを書きます。

```jsx
function App() {
  let count = 0;

  function increment() {
    count = count + 1;
    console.log(count);
  }

  return (
    <>
      <p>カウント: {count}</p>
      <button onClick={increment}>+1</button>
    </>
  );
}

export default App;
```

ボタンをクリックしてもブラウザの表示は変わりません。コンソールでは値が増えていることを確認します。

Reactは **stateが変わったとき** だけ再レンダリングします。通常の変数の変化は検知しません。

### 2. useStateで状態を管理する

`useState` を使うと、値の変化をReactが検知して自動で再レンダリングします。

```jsx
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  function increment() {
    setCount(count + 1);
  }

  return (
    <>
      <p>カウント: {count}</p>
      <button onClick={increment}>+1</button>
    </>
  );
}

export default App;
```

ボタンをクリックするたびにカウントが増え、画面が更新されることを確認します。

`useState(0)` は初期値 `0` でstateを作ります。`[count, setCount]` は分割代入で、`count` が現在の値、`setCount` が値を更新する関数です。stateの更新には必ず `setCount` を使います。

### 3. フォームの入力値をstateで管理する

前のステップでは `e.target.value` で入力値を取得しました。この値をstateに保存すると、入力内容をUIに反映できます。これを**制御コンポーネント**といいます。

```jsx
import { useState } from "react";

function App() {
  const [name, setName] = useState("");

  function handleChange(e) {
    setName(e.target.value);
  }

  return (
    <>
      <input type="text" value={name} onChange={handleChange} />
      <p>入力値: {name}</p>
    </>
  );
}

export default App;
```

`value={name}` でstateと入力欄を同期し、`onChange` でstateを更新します。入力するたびにリアルタイムで `<p>` の内容が変わることを確認します。

## まとめ

- 通常の変数を書き換えても画面は更新されない
- `useState` でstateを作り、setter関数で更新する
- stateが更新されるとReactがコンポーネントを再レンダリングする
- 制御コンポーネント: `value` をstateで管理し、`onChange` でstateを更新する

**次のステップ:** [07 リスト](../07-list/README.md) では、配列データからリストを動的に描画する方法を学びます。

## 一次情報・参考資料

- [React: stateでデータを保持する](https://ja.react.dev/learn/state-a-components-memory)
- [React: 制御コンポーネント](https://ja.react.dev/reference/react-dom/components/input#controlling-an-input-with-a-state-variable)
