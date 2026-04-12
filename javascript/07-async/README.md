# 非同期処理

## この技術で何ができるか

- 時間のかかる処理（通信・タイマーなど）が完了するまで待てます
- 処理の完了を待ちながら、他の処理をブロックしません
- 非同期処理の結果を受け取って次の処理に使えます

## 前提知識・環境

- 04-callback を完了していること

## ハンズオン

`index.html` を Live Server で開き、`main.js` にコードを書きながら進めます。

### a. 非同期処理の動作を観察してその必要性を理解する

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

### b. Promiseを使って非同期処理の完了後に処理を続けられるようにする

`setTimeout` のコールバック内にさらにコールバックを書くと、ネストが深くなって読みにくくなります（コールバック地獄）。**Promise** は非同期処理の「結果を将来受け取る約束」を表すオブジェクトで、`.then()` で完了後の処理をつなげて書けます。

```javascript
const wait = (ms) => new Promise(resolve => setTimeout(resolve, ms));

wait(1000).then(() => console.log("1秒経ちました"));
console.log("wait を呼んだ直後");
```

### c. async/awaitで非同期処理を読みやすく書けるようにする

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
- `async/await` を使うと非同期処理を同期処理のように読みやすく書ける

**次のステップ:** [08 fetch](../08-fetch/) では、`async/await` を活用して外部APIからデータを取得する方法を学びます。

## 一次情報・参考資料

- [MDN: Promise](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [MDN: async function](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/async_function)
- [MDN: await](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/await)
