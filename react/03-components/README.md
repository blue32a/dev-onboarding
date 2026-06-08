# コンポーネント

## このステップのゴール

- 関数コンポーネントを定義して使えます
- コンポーネントをファイルに分割できます

## 前提知識・環境

- 02-jsx を完了していること

## 実践

`src/App.jsx` を編集します。

### 1. コンポーネントを分割する理由を確認する

`App.jsx` にすべてのUIを書き続けると、ファイルが肥大化して管理しにくくなります。

```jsx
function App() {
  return (
    <div>
      <header>
        <h1>サイト名</h1>
        <nav>
          <a href="#">ホーム</a>
          <a href="#">ブログ</a>
        </nav>
      </header>
      <main>
        <h2>記事タイトル</h2>
        <p>記事の本文...</p>
      </main>
      <footer>
        <p>© 2024</p>
      </footer>
    </div>
  );
}
```

UIを**コンポーネント**として分割すると、再利用・管理がしやすくなります。

### 2. コンポーネントを定義する

Reactのコンポーネントは**JSXを返す関数**です。関数名は**大文字**で始めます。

```jsx
function Header() {
  return (
    <header>
      <h1>サイト名</h1>
    </header>
  );
}

function App() {
  return (
    <div>
      <Header />
      <main>
        <p>コンテンツ</p>
      </main>
    </div>
  );
}

export default App;
```

`<Header />` のように大文字で始まるタグがコンポーネントの呼び出しです。小文字のタグはHTMLの要素として扱われます。

### 3. ファイルに分割する

`src/Header.jsx` を新規作成します。

```jsx
// src/Header.jsx
function Header() {
  return (
    <header>
      <h1>サイト名</h1>
    </header>
  );
}

export default Header;
```

`src/App.jsx` からimportして使います。

```jsx
// src/App.jsx
import Header from "./Header";

function App() {
  return (
    <div>
      <Header />
      <main>
        <p>コンテンツ</p>
      </main>
    </div>
  );
}

export default App;
```

## まとめ

- コンポーネントはJSXを返す関数。名前は大文字で始める
- `<ComponentName />` の形で呼び出す
- `export default` でエクスポートし、`import` で読み込む

**次のステップ:** [04 props](../04-props/README.md) では、コンポーネントにデータを渡す方法を学びます。

## 一次情報・参考資料

- [React: 最初のコンポーネント](https://ja.react.dev/learn/your-first-component)
- [React: コンポーネントのインポートとエクスポート](https://ja.react.dev/learn/importing-and-exporting-components)
