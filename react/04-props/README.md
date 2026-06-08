# props

## このステップのゴール

- propsで親コンポーネントから子コンポーネントにデータを渡せます
- propsを使ってコンポーネントを再利用できます

## 前提知識・環境

- 03-components を完了していること

## 実践

`src/App.jsx` を編集します。

### 1. データが固定されているコンポーネントの問題

`src/App.jsx` を以下に書き換えます。

```jsx
function GreetingAlice() {
  return <p>こんにちは、Alice！</p>;
}

function GreetingBob() {
  return <p>こんにちは、Bob！</p>;
}

function App() {
  return (
    <>
      <GreetingAlice />
      <GreetingBob />
    </>
  );
}

export default App;
```

データが固定されたコンポーネントは、同じ見た目で異なるデータを表示したい場合に対応できません。人数が増えるたびにコンポーネントを複製しなければならず、管理しにくくなります。

**props** を使うと、呼び出し元からデータを渡して動的に変えられます。

### 2. propsを渡して受け取る

コンポーネントを呼び出すときに属性として渡し、関数の引数 `props` で受け取ります。

```jsx
function Greeting(props) {
  return <p>こんにちは、{props.name}！</p>;
}

function App() {
  return (
    <>
      <Greeting name="Alice" />
      <Greeting name="Bob" />
      <Greeting name="Carol" />
    </>
  );
}

export default App;
```

引数を分割代入で受け取ると簡潔に書けます。

```jsx
function Greeting({ name }) {
  return <p>こんにちは、{name}！</p>;
}
```

### 3. 複数のpropsを渡す

```jsx
function UserCard({ name, role }) {
  return (
    <div>
      <p>{name}</p>
      <p>{role}</p>
    </div>
  );
}

function App() {
  return (
    <>
      <UserCard name="Alice" role="エンジニア" />
      <UserCard name="Bob" role="デザイナー" />
    </>
  );
}

export default App;
```

## まとめ

- propsは親から子へのデータの受け渡し
- 呼び出し時に属性として渡し、関数の引数で受け取る
- propsでコンポーネントを再利用できる

**次のステップ:** [05 イベント](../05-events/README.md) では、クリックやフォーム入力のイベントハンドリングを学びます。

## 一次情報・参考資料

- [React: コンポーネントにpropsを渡す](https://ja.react.dev/learn/passing-props-to-a-component)
