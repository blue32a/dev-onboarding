# セットアップ

## このステップのゴール

- TypeScriptとtsxをインストールできます
- tscでTypeScriptをJavaScriptにコンパイルして実行できます
- tsxでTypeScriptファイルを直接実行できます

## 前提知識・環境

- Node.js v24（LTS）以上がインストールされていること
- npmの基本操作ができること（Node.jsコンテンツ08-package-managerを完了していること）

## 実践

このステップは `typescript/` ディレクトリを起点に進めます。

### 1. package.jsonを確認する

`typescript/` ディレクトリに `package.json` が用意されています。

```json
{
  "type": "module"
}
```

`"type": "module"` はES Modulesを使用することをNode.jsに伝えるフィールドです。

### 2. TypeScriptをインストールする

`typescript/` ディレクトリで以下を実行します。

```
npm install --save-dev typescript tsx
```

`typescript` はTypeScriptコンパイラ（`tsc`）を提供します。`tsx` はTypeScriptファイルをコンパイル不要で直接実行できるツールです。`--save-dev` を指定すると、`package.json` の `devDependencies` に追記され、`node_modules/` にインストールされます。

インストール後、バージョンを確認します。

```
npx tsc --version
npx tsx --version
```

### 3. tsconfig.jsonを設定する

`01-setup/` ディレクトリに `tsconfig.json` が用意されています。TypeScriptコンパイラの設定ファイルです。現在は空の状態なので、以下のオプションを追記します。

| オプション | 役割 |
| --- | --- |
| `target` | コンパイル後のJavaScriptのバージョン |
| `strict` | 厳格な型チェックを有効にする（推奨） |

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "strict": true
  }
}
```

`strict: true` は型の抜け漏れを防ぐための厳格モードです。新規プロジェクトでは常に有効にします。

### 4. 型エラーを体験する

`01-setup/main.ts` に以下を書きます。

```typescript
const message: string = 123;
console.log(message);
```

`01-setup/` ディレクトリで `npx tsc` を実行します。

```
error TS2322: Type 'number' is not assignable to type 'string'.
```

実行前にエラーが報告されました。JavaScriptでは実行するまで気づけないミスを、TypeScriptはコンパイル時に検出します。

### 5. tscでコンパイルして実行する

型エラーを修正してコンパイルします。`main.ts` を書き換えます。

```typescript
const message: string = "Hello, TypeScript!";
console.log(message);
```

`npx tsc` でコンパイルします。

```
npx tsc
```

エラーが出なければ、`main.js` が生成されます。TypeScriptのコードが、Node.jsが実行できるJavaScriptに変換されました。

生成された `main.js` を `node` で実行します。

```
node main.js
```

`Hello, TypeScript!` が出力されることを確認します。

### 6. tsxで直接実行する

`tsc` によるコンパイルと `node` による実行の2ステップを、`tsx` は1コマンドで行えます。

```
npx tsx main.ts
```

開発中のちょっとした確認など、コンパイル済みのファイルが不要なときに便利です。

## まとめ

- `npm install --save-dev <パッケージ名>` でパッケージをインストールすると `package.json` の `devDependencies` に自動で追記される
- `tsconfig.json` でコンパイラの設定を管理する。`strict: true` を必ず有効にする
- `npx tsc` でTypeScriptをJavaScriptにコンパイルし、`node` で実行できる
- `npx tsx main.ts` でコンパイルと実行を1コマンドで行える

**次のステップ:** [02 基本の型](../02-basic-types/README.md) では、TypeScriptの型の書き方を学びます。

## 一次情報・参考資料

- [TypeScript 公式サイト](https://www.typescriptlang.org/)
- [tsconfig.json リファレンス](https://www.typescriptlang.org/tsconfig)
- [tsx](https://github.com/privatenumber/tsx)
