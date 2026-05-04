# HTTPサーバー

## このステップのゴール

- `http` モジュールでHTTPサーバーを起動できます
- リクエストのURLとメソッドに応じてレスポンスを返せます
- JSONレスポンスを返すAPIエンドポイントを作れます

## 前提知識・環境

- 03-files を完了していること
- HTTPリクエスト・レスポンスの基本的な仕組みを理解していること

## 実践

`main.js` にコードを書きながら進めます。起動は `node main.js` です。

### 1. サーバーを起動する

`http.createServer()` でサーバーを作成します。コールバック関数はリクエストを受け取るたびに呼ばれます。

```javascript
import { createServer } from "node:http";

const server = createServer((req, res) => {
  res.writeHead(200, { "Content-Type": "text/plain" });
  res.end("Hello, Node.js!");
});

server.listen(3000, () => {
  console.log("サーバーを起動しました: http://localhost:3000");
});
```

`node main.js` で起動し、ブラウザで `http://localhost:3000` を開きます。`Hello, Node.js!` が表示されることを確認します。

サーバーを停止するには `Ctrl+C` を押します。

### 2. URLでルーティングする

`req.url` でリクエストされたパスを取得できます。パスに応じて異なるレスポンスを返します。

```javascript
import { createServer } from "node:http";

const server = createServer((req, res) => {
  if (req.url === "/") {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("トップページ");
  } else if (req.url === "/about") {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("このサーバーについて");
  } else {
    res.writeHead(404, { "Content-Type": "text/plain" });
    res.end("Not Found");
  }
});

server.listen(3000, () => {
  console.log("サーバーを起動しました: http://localhost:3000");
});
```

ブラウザで `/`、`/about`、`/other` にアクセスして、それぞれのレスポンスを確認します。

### 3. JSONレスポンスを返す

APIでは主にJSONを返します。`JSON.stringify()` でオブジェクトをJSON文字列に変換し、`Content-Type` を `application/json` に設定します。

```javascript
import { createServer } from "node:http";

const users = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" },
];

const server = createServer((req, res) => {
  if (req.url === "/api/users") {
    res.writeHead(200, { "Content-Type": "application/json" });
    res.end(JSON.stringify(users));
  } else {
    res.writeHead(404, { "Content-Type": "application/json" });
    res.end(JSON.stringify({ error: "Not Found" }));
  }
});

server.listen(3000, () => {
  console.log("サーバーを起動しました: http://localhost:3000");
});
```

ブラウザで `http://localhost:3000/api/users` を開き、JSONが返ってくることを確認します。

### 4. リクエストボディを受け取る

POSTリクエストのボディはストリームとして届きます。`data` イベントでチャンクを受け取り、`end` イベントで全体を組み立てます。

`index.html` はLive Server（`http://127.0.0.1:5500`）で配信されるため、Node.jsサーバー（`http://localhost:3000`）とはオリジンが異なります。異なるオリジン間のリクエストはブラウザのCORS制限を受けるため、サーバー側で `Access-Control-Allow-Origin` ヘッダーを返す必要があります。また、`Content-Type: application/json` を含むリクエストの前にブラウザが送るプリフライト（`OPTIONS`）リクエストも処理します。

```javascript
import { createServer } from "node:http";

const server = createServer((req, res) => {
  res.setHeader("Access-Control-Allow-Origin", "*");
  res.setHeader("Access-Control-Allow-Headers", "Content-Type");

  if (req.method === "OPTIONS") {
    res.writeHead(204);
    res.end();
    return;
  }

  if (req.method === "POST" && req.url === "/api/echo") {
    let body = "";
    req.on("data", (chunk) => {
      body += chunk;
    });
    req.on("end", () => {
      const data = JSON.parse(body);
      res.writeHead(200, { "Content-Type": "application/json" });
      res.end(JSON.stringify({ received: data }));
    });
  } else {
    res.writeHead(404);
    res.end();
  }
});

server.listen(3000, () => {
  console.log("サーバーを起動しました: http://localhost:3000");
});
```

`node main.js` でサーバーを起動し、このステップに用意されている `index.html` をLive Serverで開きます。ボタンをクリックしてPOSTリクエストを送り、レスポンスがページに表示されることを確認します。

## まとめ

このステップでは以下を学びました。

- `http.createServer()` でHTTPサーバーを作成し、`server.listen()` でポートをバインドする
- `req.url` と `req.method` でルーティングし、`res.writeHead()` でステータスコードとヘッダーを設定する
- JSONレスポンスは `Content-Type: application/json` と `JSON.stringify()` を組み合わせる

**次のステップ:** [05 プロセスとCLI](../05-process-cli/README.md) では、環境変数やコマンドライン引数の扱いを学びます。

## 一次情報・参考資料

- [Node.js: http モジュール](https://nodejs.org/docs/latest/api/http.html)
- [HTTP レスポンスステータスコード（MDN）](https://developer.mozilla.org/ja/docs/Web/HTTP/Status)
