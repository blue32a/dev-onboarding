# エラーハンドリング

## この技術で何ができるか

- エラーが発生してもアプリケーションが止まらない処理を書けます
- エラーの種類に応じたメッセージをユーザーに伝えられます
- 非同期処理（fetch など）のエラーを適切に処理できます

## 前提知識・環境

- 08-fetch を完了していること

## ハンズオン

`index.html` を Live Server で開き、`main.js` にコードを書きながら進めます。

### a. try/catchでエラーを捕捉してアプリを継続できるようにする

エラーを捕捉しないと、発生した時点でJavaScriptの実行が止まってしまいます。まず `try / catch` なしでエラーを発生させ、後続の処理が止まることを確認します。

```javascript
null.property; // TypeError
console.log("ここは実行されない");
```

`try` ブロックに書いた処理でエラーが発生すると、`catch` ブロックに移ります。`catch` の引数（`e`）にはエラーオブジェクトが渡され、`e.name` でエラーの種類、`e.message` で内容を取得できます。

```javascript
try {
  null.property;
} catch (e) {
  console.log(e.name);    // "TypeError"
  console.log(e.message);
}
console.log("ここは実行される");
```

`try / catch` で囲んだことで後続の処理も実行されることを確認します。

### b. 通信エラーをハンドリングしてユーザーに適切なフィードバックを伝える

通信は必ず失敗する可能性があります。エラーハンドリングなしでは失敗時にページが壊れたり、ユーザーが何が起きたかわからなくなります。

`async` 関数ごと `try / catch` で囲むと、`await` 内で発生したエラーも捕捉できます。`fetch()` 自体はネットワークエラーでしか失敗しません。HTTPエラー（404・500など）は `response.ok` で確認し、`throw new Error()` で意図的にエラーを発生させることで `catch` に流せます。

```javascript
const result = document.querySelector("#result");

async function fetchUser(url) {
  try {
    const response = await fetch(url);
    if (!response.ok) {
      throw new Error(`HTTPエラー: ${response.status}`);
    }
    const user = await response.json();
    result.textContent = `取得成功: ${user.name}`;
  } catch (e) {
    result.textContent = `エラー: ${e.message}`;
    console.error(e);
  }
}

document.querySelector("#success-btn").addEventListener("click", () => {
  fetchUser("https://jsonplaceholder.typicode.com/users/1");
});

document.querySelector("#fail-btn").addEventListener("click", () => {
  fetchUser("https://jsonplaceholder.typicode.com/users/0");
});
```

成功・失敗それぞれのボタンを押して動作を確認します。

### c. finallyで成功・失敗に関わらず後処理を確実に実行する

ローディング中の表示やリソースの解放など、結果にかかわらず必ず実行すべき処理があります。`finally` ブロックは `try` が成功しても `catch` に入っても必ず実行されます。`try` と `catch` それぞれに同じ処理を重複して書く必要がなくなります。

`fetchUser` に `finally` を追加します。

```javascript
} finally {
  console.log("fetchUser 終了");
}
```

成功・失敗どちらのボタンを押しても `finally` が実行されることを確認します。

## まとめ

このステップでは以下を学びました。

- `try / catch` でエラーを捕捉し、後続の処理を継続できる
- `e.name` / `e.message` でエラーの種類と内容を取得できる
- `async` 関数を `try / catch` で囲むと非同期処理のエラーも捕捉できる
- `throw new Error()` で意図的にエラーを発生させ `catch` に流せる
- `finally` で成功・失敗に関わらず後処理を確実に実行できる

**次のステップ:** [10 モジュール](../10-modules/) では、コードを複数のファイルに分割して管理しやすくする方法を学びます。

## 一次情報・参考資料

- [MDN: try...catch](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/try...catch)
- [MDN: Error](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Error)
- [MDN: throw](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/throw)
