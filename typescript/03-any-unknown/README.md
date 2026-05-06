# anyとunknown

## このステップのゴール

- anyを使わずにunknownで型安全にコードを書けます
- 型アサーション（`as`）を適切な場面で使えます

## 前提知識・環境

- 02-basic-types を完了していること

## 実践

`main.ts` にコードを書きながら進めます。実行は `npx tsx main.ts` です。

### 1. anyの問題点を確認する

`any` はどんな型にも代入でき、型チェックを無効にします。型エラーが出なくなる一方で、実行時エラーの原因になります。

```typescript
let value: any = "hello";
value = 123;
value = true;

// any はメソッド呼び出しもエラーにならない
value.toUpperCase(); // 実行時エラー: value.toUpperCase is not a function
```

`any` を使うとTypeScriptの型チェックの恩恵を失います。型が不明な場合は `unknown` を使います。

### 2. unknownを使う

`unknown` は「型が不明」を表す型です。`any` と異なり、型を絞り込まないと操作できません。

```typescript
let value: unknown = "hello";

// 型を絞り込む前は操作できない
// value.toUpperCase(); // エラー

if (typeof value === "string") {
  console.log(value.toUpperCase()); // 絞り込み後は string として操作できる
}
```

`unknown` を受け取って型を確認してから処理する関数の例です。

```typescript
function printLength(value: unknown): void {
  if (typeof value === "string") {
    console.log(value.length);
  } else if (Array.isArray(value)) {
    console.log(value.length);
  } else {
    console.log("length は取得できません");
  }
}

printLength("hello");  // 5
printLength([1, 2, 3]); // 3
printLength(42);        // length は取得できません
```

### 3. 型アサーション（as）を使う

TypeScriptが型を判断できない場合に、`as` で型を明示的に指定できます。

`JSON.parse` の戻り値は `any` 型です。返ってくる値の構造をTypeScriptは知らないため、型アサーションで形状を明示します。

```typescript
const data = JSON.parse('{"name": "Alice", "age": 30}') as { name: string; age: number };
console.log(data.name); // Alice
```

`unknown` に対して型アサーションを使う例です。

```typescript
function parseData(raw: unknown): string {
  return raw as string;
}
```

### 4. 型アサーションの注意点

`as` は型チェックをスキップするため、誤った型を指定すると実行時エラーになります。TypeScriptが証明できない変換には二重アサーション（`as unknown as 型`）が必要ですが、これは型安全性を大きく損ないます。

```typescript
const value = "hello" as unknown as number; // コンパイルは通るが危険
```

`as` は「自分が正しいと確信している場合」にのみ使います。型の絞り込みで対応できる場合はそちらを優先します。

## まとめ

- `any` は型チェックを無効にするため、型が不明な場合は `unknown` を使う
- `unknown` は型を絞り込んでから操作する必要があり、型安全性を保てる
- `as` でTypeScriptが判断できない型を明示できるが、誤用すると実行時エラーになる

**次のステップ:** [04 オブジェクトの型](../04-object-types/README.md) では、オブジェクトの型を定義する方法を学びます。

## 一次情報・参考資料

- [TypeScript: any](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#any)
- [TypeScript: unknown](https://www.typescriptlang.org/docs/handbook/2/functions.html#unknown)
- [TypeScript: Type Assertions](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions)
