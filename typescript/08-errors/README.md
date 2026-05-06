# エラーの読み方

## このステップのゴール

- TypeScriptのエラーメッセージの構造を読み解けます
- よくあるエラーパターンに対処できます

## 前提知識・環境

- 06-union-types を完了していること

## 実践

`main.ts` にコードを書きながら進めます。意図的にエラーを起こして `npx tsc` でエラーを確認します。

### 1. "Type 'X' is not assignable to type 'Y'"

最も頻出するエラーです。型が合わない値を代入しようとしています。

```typescript
let name: string = 123;
```

```
error TS2322: Type 'number' is not assignable to type 'string'.
```

**読み方:** `number` を `string` に代入しようとしている。変数の型か代入する値を修正します。

オブジェクトの場合、プロパティの型不一致でも同じエラーが出ます。

```typescript
interface User {
  name: string;
  age: number;
}

const user: User = {
  name: "Alice",
  age: "30", // エラー
};
```

```
error TS2322: Type 'string' is not assignable to type 'number'.
  The expected type comes from property 'age' which is declared here on type 'User'
```

### 2. "Property 'X' does not exist on type 'Y'"

存在しないプロパティにアクセスしようとしています。

```typescript
interface User {
  name: string;
}

const user: User = { name: "Alice" };
console.log(user.email); // エラー
```

```
error TS2339: Property 'email' does not exist on type 'User'.
```

**読み方:** `User` 型に `email` というプロパティはない。プロパティ名のタイポや、型定義の確認が必要です。

### 3. "Argument of type 'X' is not assignable to parameter of type 'Y'"

関数の引数に合わない型の値を渡しています。

```typescript
function greet(name: string): void {
  console.log(`こんにちは、${name}さん`);
}

greet(42); // エラー
```

```
error TS2345: Argument of type 'number' is not assignable to parameter of type 'string'.
```

**読み方:** 関数は `string` を期待しているが `number` を渡している。渡す値の型か関数の引数の型を修正します。

### 4. 入れ子のエラーを読む

複雑な型が絡むと、エラーが複数行にわたります。最も内側の行が具体的な原因です。

```typescript
interface Address {
  city: string;
  zip: number;
}

interface User {
  name: string;
  address: Address;
}

const user: User = {
  name: "Alice",
  address: {
    city: "Tokyo",
    zip: "100-0001", // エラー
  },
};
```

```
error TS2322: Type 'string' is not assignable to type 'number'.
  Types of property 'zip' are incompatible.
    Type 'string' is not assignable to type 'number'.
```

**読み方:** 上から順に「どのプロパティで」「何が起きているか」を追います。最後の行が根本原因です。

## まとめ

- `Type 'X' is not assignable to type 'Y'`: 型が合わない代入・プロパティ
- `Property 'X' does not exist on type 'Y'`: 存在しないプロパティへのアクセス
- `Argument of type 'X' is not assignable to parameter of type 'Y'`: 関数の引数の型不一致
- 入れ子のエラーは最も内側の行が根本原因

**次のステップ:** [09 ジェネリクス](../09-generics/README.md) では、型を引数として受け取るジェネリクスとユーティリティ型を学びます。

## 一次情報・参考資料

- [TypeScript Error Translator（エラーを日本語で確認できるツール）](https://ts-error-translator.vercel.app/)
