# プロセスとCLI

## このステップのゴール

- `process.env` で環境変数を取得できます
- `process.argv` でコマンドライン引数を受け取れます
- 標準入力から値を受け取る対話型CLIを作れます

## 前提知識・環境

- 04-http-server を完了していること

## 実践

`main.js` にコードを書きながら進めます。実行は `node main.js` です。

### 1. 環境変数を使う

環境変数はプロセスの外から設定を渡す仕組みです。APIキーやデータベースの接続情報など、コードに直接書きたくない値に使われます。

`process.env` で環境変数を取得できます。

```javascript
console.log(process.env.NODE_ENV);   // 設定されていなければ undefined
console.log(process.env.PATH);       // OSのPATH環境変数
```

コマンド実行時に環境変数を設定することもできます。

```
NODE_ENV=production node main.js
```

```javascript
const env = process.env.NODE_ENV ?? "development";
console.log(`実行環境: ${env}`);
```

`??` はnull合体演算子で、左辺が `null` または `undefined` のときに右辺を返します。

### 2. .env ファイルから読み込む

環境変数を `.env` ファイルで管理する慣習があります。Node.js v20.6.0以降では `--env-file` オプションで `.env` ファイルを読み込めます。

`.env` ファイルを作成します。APIキーなどの機密情報を含むため、一般的なプロジェクトでは `.gitignore` に追加してGitの管理対象から除外します。このステップの `.gitignore` にはあらかじめ設定済みです。

```
PORT=8080
APP_NAME=MyApp
```

`--env-file` オプションを付けて実行します。

```
node --env-file=.env main.js
```

```javascript
console.log(process.env.PORT);      // 8080
console.log(process.env.APP_NAME);  // MyApp
```

### 3. コマンドライン引数を受け取る

`process.argv` はコマンドライン引数の配列です。`process.argv[0]` はNodeのパス、`process.argv[1]` はスクリプトのパスで、ユーザーが渡す引数は `process.argv[2]` 以降に入ります。

```javascript
const args = process.argv.slice(2);
console.log(args);
```

```
node main.js hello world
# [ 'hello', 'world' ]
```

引数を使ってCLIツールらしい動作を作ります。

```javascript
const args = process.argv.slice(2);
const name = args[0] ?? "世界";
console.log(`こんにちは、${name}！`);
```

```
node main.js Alice
# こんにちは、Alice！
```

### 4. 標準入力から受け取る

`process.stdin` を使うと、ターミナルからの入力を受け取れます。

```javascript
process.stdout.write("名前を入力してください: ");

process.stdin.setEncoding("utf-8");
process.stdin.once("data", (input) => {
  const name = input.trim();
  console.log(`こんにちは、${name}！`);
  process.exit(0);
});
```

`node main.js` で起動し、ターミナルに名前を入力して Enter を押します。`process.exit(0)` でプロセスを正常終了します。

## まとめ

このステップでは以下を学びました。

- `process.env` で環境変数を取得する。`--env-file` で `.env` ファイルを読み込める
- `process.argv.slice(2)` でユーザーが渡したコマンドライン引数を取得する
- `process.stdin` で標準入力を受け取り、`process.stdout` で出力する
- `process.exit()` でプロセスを終了する（0が正常終了）

**次のステップ:** [06 エラーハンドリング](../06-error-handling/README.md) では、Node.js固有のエラーパターンを学びます。

## 一次情報・参考資料

- [Node.js: process](https://nodejs.org/docs/latest/api/process.html)
- [Node.js: --env-file オプション](https://nodejs.org/docs/latest/api/cli.html#--env-fileconfig)
