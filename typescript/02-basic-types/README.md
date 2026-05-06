# 基本の型

## このステップのゴール

- 変数に型アノテーションを付けてコンパイル時に型の誤りを検出できます
- 型アノテーションを書く箇所と省略できる箇所を判断できます
- string・number・boolean・配列・null・undefinedの型を使えます

## 前提知識・環境

- 01-setup を完了していること

## 実践

`main.ts` にコードを書きながら進めます。実行は `npx tsx main.ts` です。

### 1. 型アノテーションで型の誤りをコンパイル時に検出する

このステップには `main.js` が用意されています。まずJavaScriptの場合を確認します。

```
node main.js
```

出力は `"未集計10"` になります。`score` に文字列が代入されていますが、JavaScriptはエラーにならず、数値演算のつもりが文字列結合になっています。

次に `main.ts` に型アノテーションを付けた同じコードを書きます。

```typescript
let score: number = 100;
score = "未集計";
console.log(score + 10);
```

`npx tsc` を実行すると、実行前に型の誤りが報告されます。

```
error TS2322: Type 'string' is not assignable to type 'number'.
```

変数名の後に `: 型名` と書くのが型アノテーションです。JavaScriptでは実行するまで気づけなかった誤りが、コンパイル時に検出できます。他のプリミティブ型も確認します。

```typescript
const name: string = "Alice";
const active: boolean = true;

console.log(name, active);
```

### 2. 型推論を確認する

TypeScriptは初期値から型を自動的に推論するため、毎回型アノテーションを書く必要はありません。

```typescript
const name = "Alice";  // string と推論される
const score = 100;     // number と推論される
const active = true;   // boolean と推論される
```

推論された型に反する代入はエラーになります。

```typescript
let count = 0;
count = "hello"; // エラー: Type 'string' is not assignable to type 'number'.
```

VS Codeでは変数にカーソルを当てると推論された型が表示されます。

### 3. 配列の型を書く

配列の型は `型名[]` で表します。

```typescript
const names: string[] = ["Alice", "Bob", "Carol"];
const scores: number[] = [85, 92, 78];

console.log(names[0]);      // Alice
console.log(scores.length); // 3
```

配列の要素も型チェックされます。

```typescript
const names: string[] = ["Alice", 123]; // エラー: Type 'number' is not assignable to type 'string'.
```

### 4. nullとundefinedを扱う

`null` や `undefined` の見落としは実行時エラーの主な原因です。`strict: true` の環境では、明示的に許可しないと代入できません。

```typescript
let value: string = "hello";
value = null; // エラー: Type 'null' is not assignable to type 'string'.
```

`null` を受け入れる場合は `| null` で型に追加します。

```typescript
let value: string | null = null;
value = "hello";
console.log(value);
```

`| null` を明示することで、nullになりうる変数が一目でわかります。

## まとめ

- `変数名: 型名` で型アノテーションを付け、型の誤りをコンパイル時に検出できる
- TypeScriptは初期値から型を推論するため、毎回型アノテーションを書く必要はない
- 配列の型は `型名[]` で表す
- `strict: true` では null と undefined を `| null` / `| undefined` で明示しないと代入できない

**次のステップ:** [03 anyとunknown](../03-any-unknown/README.md) では、型安全性を損なう `any` と、安全な代替である `unknown` を学びます。

## 一次情報・参考資料

- [TypeScript: Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)
- [TypeScript: Type Inference](https://www.typescriptlang.org/docs/handbook/type-inference.html)
