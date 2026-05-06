# 交差型

## このステップのゴール

- 交差型（`&`）で複数の型を組み合わせた新しい型を作れます

## 前提知識・環境

- 06-union-types を完了していること

## 実践

`main.ts` にコードを書きながら進めます。実行は `npx tsx main.ts` です。

### 1. 型の重複を解消する

複数のオブジェクト型に共通のプロパティが重複しているコードを考えます。

```typescript
interface User {
  id: number;
  name: string;
  createdAt: string;
  updatedAt: string;
}

interface Product {
  id: number;
  price: number;
  createdAt: string;
  updatedAt: string;
}
```

`createdAt` と `updatedAt` が両方に重複しています。共通部分を変更したいとき、すべての型を修正する必要があります。

交差型（`&`）を使うと、複数の型を組み合わせて新しい型を作れます。共通部分を独立した型として定義し、`&` で組み合わせます。

```typescript
interface Timestamped {
  createdAt: string;
  updatedAt: string;
}

interface User {
  id: number;
  name: string;
}

interface Product {
  id: number;
  price: number;
}

type TimestampedUser = User & Timestamped;
type TimestampedProduct = Product & Timestamped;

const user: TimestampedUser = {
  id: 1,
  name: "Alice",
  createdAt: "2024-01-01",
  updatedAt: "2024-01-01",
};

console.log(user);
```

`TimestampedUser` は `User` と `Timestamped` の全プロパティを持ちます。`Timestamped` の変更は一か所で済みます。

### 2. interfaceのextendsと比較する

`interface` の拡張には `extends` を使えます。

```typescript
interface Timestamped {
  createdAt: string;
  updatedAt: string;
}

interface User extends Timestamped {
  id: number;
  name: string;
}

const user: User = {
  id: 1,
  name: "Alice",
  createdAt: "2024-01-01",
  updatedAt: "2024-01-01",
};

console.log(user);
```

`type` には `extends` がないため、同様の拡張には `&` を使います。

```typescript
type Timestamped = {
  createdAt: string;
  updatedAt: string;
};

type User = {
  id: number;
  name: string;
} & Timestamped;

const user: User = {
  id: 1,
  name: "Alice",
  createdAt: "2024-01-01",
  updatedAt: "2024-01-01",
};

console.log(user);
```

`interface` の拡張には `extends`、`type` の拡張には `&` を使います。

## まとめ

- 交差型（`&`）で複数の型を組み合わせると、全プロパティを持つ新しい型を作れる
- 共通のプロパティをひとつの型にまとめ、各型に `&` で組み合わせると重複を解消できる
- `interface` の拡張には `extends`、`type` の拡張には `&` を使う

**次のステップ:** [08 エラーの読み方](../08-errors/README.md) では、TypeScriptのエラーメッセージの読み解き方を学びます。

## 一次情報・参考資料

- [TypeScript: Intersection Types](https://www.typescriptlang.org/docs/handbook/2/objects.html#intersection-types)
