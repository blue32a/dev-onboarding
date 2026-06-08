# リスト

## このステップのゴール

- 配列データからリストを動的に描画できます
- keyプロパティが必要な理由を説明できます

## 前提知識・環境

- 06-state を完了していること

## 実践

`src/App.jsx` を編集します。

### 1. JSXの中でforループは使えない

配列から `for` 文でリストを生成しようとするとエラーになります。

```jsx
// エラー: JSXの中でfor文は使えない
function App() {
  const fruits = ["りんご", "バナナ", "みかん"];
  return (
    <ul>
      {for (const fruit of fruits) { // SyntaxError
        <li>{fruit}</li>
      }}
    </ul>
  );
}
```

JSXの `{}` には**式**しか書けません。`for` 文は式ではなく文なので使えません。

### 2. mapでリストを描画する

`Array.map()` は配列を別の配列に変換する式なので、JSXの中で使えます。

```jsx
function App() {
  const fruits = ["りんご", "バナナ", "みかん"];

  return (
    <ul>
      {fruits.map((fruit) => (
        <li>{fruit}</li>
      ))}
    </ul>
  );
}

export default App;
```

リストが表示されます。ブラウザのコンソールに警告が表示されていることを確認します。

Reactはリストを再レンダリングするとき、`key` を使ってどの要素が変わったかを特定します。`key` がないと効率よく差分を検知できないため、警告が表示されます。各要素に `key` を追加します。

```jsx
{fruits.map((fruit) => (
  <li key={fruit}>{fruit}</li>
))}
```

警告が消えることを確認します。

### 3. オブジェクトの配列を描画する

実際のデータはオブジェクトの配列であることが多いです。`key` にはリスト内で重複しない一意な値を使います。実際のデータではIDを使います。

```jsx
function App() {
  const users = [
    { id: 1, name: "Alice" },
    { id: 2, name: "Bob" },
    { id: 3, name: "Carol" },
  ];

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

export default App;
```

## まとめ

- JSXの中で `for` 文は使えない。`Array.map()` でリストを描画する
- 各要素に `key` プロパティを付ける。リスト内で一意な値を使う
- `key` はReactが変化した要素を効率よく特定するために使う

**次のステップ:** [08 useEffect](../08-effect/README.md) では、コンポーネントの外部との連携（APIフェッチ）を学びます。

## 一次情報・参考資料

- [React: リストのレンダリング](https://ja.react.dev/learn/rendering-lists)
