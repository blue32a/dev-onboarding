# fetch

## このステップのゴール

- 外部のAPIからデータを取得してページに表示できます
- JavaScriptのオブジェクトとJSON文字列を相互に変換できます
- ボタン操作などのタイミングでデータを動的に取得できます

## 前提知識・環境

- 07-async を完了していること

## 実践

`index.html` を Live Server で開き、`main.js` にコードを書きながら進めます。

### 1. fetchAPIを使って外部サーバーからデータを取得できるようにする

`fetch(url)` はHTTPリクエストを送り、Promiseを返します。`async/await` と組み合わせて使います。レスポンスの取得は2段階になっており、1回目の `await` でHTTPレスポンス（ヘッダー）を受け取り、2回目の `await response.json()` でボディをJavaScriptオブジェクトに変換します。

このステップでは [JSONPlaceholder](https://jsonplaceholder.typicode.com/) を使います。JSONPlaceholderはテスト・学習用のフェイクREST APIで、ユーザー・投稿・コメントなどのダミーデータを返します。登録不要で使えます。

```javascript
const btn = document.querySelector("#fetch-btn");

btn.addEventListener("click", async () => {
  const response = await fetch("https://jsonplaceholder.typicode.com/users");
  const users = await response.json();
  console.log(users);
});
```

ボタンをクリックして取得したデータを確認します。開発者ツールの **Network** タブでリクエストとレスポンスの内容も確認しましょう。

### 2. 取得したデータをDOMに反映してページに表示できるようにする

データを取得するだけでは画面には何も表示されません。取得後にDOMを操作してページに反映することで、はじめてユーザーに見える形になります。`fetch()` はネットワークエラー以外では失敗しないため、404や500のエラーレスポンスでも `response` オブジェクトは返ります。`response.ok` でリクエストが成功したか確認できます。

```javascript
const btn = document.querySelector("#fetch-btn");
const status = document.querySelector("#status");
const list = document.querySelector("#user-list");

btn.addEventListener("click", async () => {
  status.textContent = "取得中...";
  list.innerHTML = "";

  const response = await fetch("https://jsonplaceholder.typicode.com/users");
  const users = await response.json();

  status.textContent = `${users.length} 件取得しました`;
  users.forEach(({ name, email }) => {
    const li = document.createElement("li");
    li.textContent = `${name}（${email}）`;
    list.appendChild(li);
  });
});
```

### 3. APIとのデータ交換で使うJSON変換を理解する

JSONはJavaScriptのオブジェクト・配列を文字列として表現するフォーマットです。APIとのデータのやり取りで広く使われています。`JSON.stringify()` でオブジェクトをJSON文字列に、`JSON.parse()` でJSON文字列をオブジェクトに変換できます（`response.json()` は内部で `JSON.parse` を実行しています）。

`main.js` の末尾に追加して確認しましょう。

```javascript
const user = { name: "Alice", age: 25 };
const json = JSON.stringify(user);
console.log(json);
console.log(typeof json); // "string"

const parsed = JSON.parse(json);
console.log(parsed.name);
console.log(typeof parsed); // "object"
```

## まとめ

このステップでは以下を学びました。

- `fetch()` と `async/await` を組み合わせてAPIからデータを取得できる
- `response.json()` でレスポンスのボディをオブジェクトに変換できる
- `JSON.stringify()` / `JSON.parse()` でオブジェクトとJSON文字列を相互変換できる

**次のステップ:** [09 エラーハンドリング](../09-error-handling/README.md) では、通信の失敗など予期しないエラーが発生したときにアプリを止めずに処理する方法を学びます。

## 一次情報・参考資料

- [MDN: fetch()](https://developer.mozilla.org/ja/docs/Web/API/Window/fetch)
- [MDN: Response.json()](https://developer.mozilla.org/ja/docs/Web/API/Response/json)
- [MDN: JSON](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/JSON)
