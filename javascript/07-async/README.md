# 非同期処理

## このステップのゴール

- 時間のかかる処理（通信・タイマーなど）が完了するまで待てます
- 処理の完了を待ちながら、他の処理をブロックしません
- 非同期処理の結果を受け取って次の処理に使えます

## 前提知識・環境

- 04-callback を完了していること

## 実践

`index.html` を Live Server で開き、`main.js` にコードを書きながら進めます。

### 1. 非同期処理の動作を観察してその必要性を理解する

JavaScriptはシングルスレッドで動作します。処理を上から順に実行する「同期処理」と、完了を待たずに次の行に進む「非同期処理」があります。

まず非同期処理の動作を自分の目で確認します。出力の順番が直感に反することに気づくはずです。

```javascript
console.log("開始");
setTimeout(() => {
  console.log("1秒後");
}, 1000);
console.log("終了");
```

「開始」→「終了」→「1秒後」の順になることを確認します。`setTimeout` は非同期処理のため、コールバックの実行を待たずに次の行に進んでいます。

### 2. Promiseを使って非同期処理の完了後に処理を続けられるようにする

`setTimeout` のコールバック内にさらにコールバックを書くと、ネストが深くなって読みにくくなります（コールバック地獄）。**Promise** は非同期処理の「結果を将来受け取る約束」を表すオブジェクトで、`.then()` で完了後の処理をつなげて書けます。

```javascript
const wait = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

wait(1000).then(() => console.log("1秒経ちました"));
console.log("wait を呼んだ直後");
```

Promiseはタイマー以外にも広く使われます。`new Promise()` に `resolve`（成功）と `reject`（失敗）を渡すことで、任意の処理をPromiseとして表現できます。`.catch()` で失敗時の処理を書けます。

以下はデータ取得をPromiseで模した例です。次のステップで学ぶ `fetch()` と同じ `.then()` / `.catch()` のパターンで使えます。

```javascript
// ユーザー取得を模した例。resolve・rejectは即座に呼ばれるため
// この例は同期的に解決される。fetch() では非同期で解決される。
function loadUser(id) {
  const users = { 1: "Alice", 2: "Bob" };
  if (users[id]) {
    return Promise.resolve({ id, name: users[id] });
  } else {
    return Promise.reject(new Error("ユーザーが見つかりません"));
  }
}

loadUser(1).then((user) => console.log(user.name)); // "Alice"
loadUser(99).catch((e) => console.log(e.message)); // "ユーザーが見つかりません"
```

### 3. async/awaitで非同期処理を読みやすく書けるようにする

Promise チェーンが続くと処理の流れを追いにくくなります。`async/await` を使うと、非同期処理を上から下に読める形で書けます。`await` はPromiseの完了を待ってから次の行に進みます。`await` は `async` と宣言した関数の中でしか使えません。

```javascript
async function run() {
  console.log("開始");
  await wait(1000);
  console.log("1秒経過");
  await wait(500);
  console.log("さらに0.5秒経過");
}

run();
console.log("run() を呼んだ直後");
```

出力の順番を確認し、`run()` を呼んだ直後の行が先に実行されることを観察します。

## まとめ

このステップでは以下を学びました。

- JavaScriptは非同期処理を待たずに次の行に進む
- Promiseを使うと非同期処理の完了後に続く処理を`.then()`でつなげられる
- `new Promise((resolve, reject) => { ... })` のように任意の処理をPromiseとして表現できる
- `async/await` を使うと非同期処理を同期処理のように読みやすく書ける

**次のステップ:** [08 fetch](../08-fetch/README.md) では、`async/await` を活用して外部APIからデータを取得する方法を学びます。

## 一次情報・参考資料

- [MDN: Promise](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [MDN: async function](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/async_function)
- [MDN: await](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/await)
