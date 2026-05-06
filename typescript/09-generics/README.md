# ジェネリクス

## このステップのゴール

- ジェネリクスで型を引数として受け取る汎用的な関数を書けます
- Partial・Readonly・Pick・Omit・Recordなどのユーティリティ型を使えます

## 前提知識・環境

- 08-errors を完了していること

## 実践

`main.ts` にコードを書きながら進めます。実行は `npx tsx main.ts` です。

### 1. ジェネリック関数を書く

配列の先頭要素を返す関数を、文字列と数値それぞれで書いてみます。

```typescript
function firstString(items: string[]): string | undefined {
  return items[0];
}

function firstNumber(items: number[]): number | undefined {
  return items[0];
}

console.log(firstString(["Alice", "Bob"])); // Alice
console.log(firstNumber([85, 92, 78]));     // 85
```

ロジックはまったく同じなのに、型ごとに関数を用意しなければなりません。`any` で統一することもできますが、戻り値の型情報が失われます。

```typescript
function first(items: any[]): any {
  return items[0];
}

const name = first(["Alice", "Bob"]);
name.toFixed(2); // 文字列なのに数値メソッドを呼んでもエラーにならない
```

ジェネリクスを使うと、型を保ちながら1つの関数で対応できます。

```typescript
function first<T>(items: T[]): T | undefined {
  return items[0];
}

const name = first(["Alice", "Bob"]); // string | undefined
const score = first([85, 92, 78]);    // number | undefined

console.log(name);  // Alice
console.log(score); // 85
```

`<T>` で型を引数として受け取ります。呼び出し時に渡した引数から `T` の型が自動で推論されます。

### 2. 型引数に制約を付ける

`extends` で型引数が満たすべき条件を指定できます。

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { id: 1, name: "Alice", email: "alice@example.com" };

console.log(getProperty(user, "name"));  // Alice
console.log(getProperty(user, "email")); // alice@example.com
console.log(getProperty(user, "age"));   // エラー: Argument of type '"age"' is not assignable to parameter of type 'keyof { id: number; name: string; email: string; }'.
```

`keyof T` は型 `T` のプロパティ名のUnion型です。存在しないプロパティのアクセスをコンパイル時に防げます。

### 3. ユーティリティ型を使う

TypeScriptには既存の型を変換するユーティリティ型が組み込まれています。

**Partial** — 全プロパティをオプショナルにします。更新処理などで一部のプロパティだけ渡す場合に使います。

```typescript
interface User {
  id: number;
  name: string;
  email: string;
}

function updateUser(id: number, changes: Partial<User>): void {
  console.log(`ユーザー ${id} を更新:`, changes);
}

updateUser(1, { name: "Bob" }); // name だけ渡せる
```

**Readonly** — 全プロパティを読み取り専用にします。

```typescript
const config: Readonly<{ host: string; port: number }> = {
  host: "localhost",
  port: 3000,
};

config.host = "example.com"; // エラー: Cannot assign to 'host' because it is a read-only property.
```

**Pick** — 指定したプロパティだけを取り出します。

```typescript
type UserPreview = Pick<User, "id" | "name">;

const preview: UserPreview = { id: 1, name: "Alice" };
console.log(preview); // { id: 1, name: 'Alice' }
```

**Omit** — 指定したプロパティを除いた型を作ります。

```typescript
type UserWithoutEmail = Omit<User, "email">;

const user: UserWithoutEmail = { id: 1, name: "Alice" };
console.log(user); // { id: 1, name: 'Alice' }
```

**Record** — キーと値の型を指定してオブジェクトの型を作ります。

```typescript
type RoleLabel = Record<"admin" | "editor" | "viewer", string>;

const labels: RoleLabel = {
  admin: "管理者",
  editor: "編集者",
  viewer: "閲覧者",
};
console.log(labels); // { admin: '管理者', editor: '編集者', viewer: '閲覧者' }
```

## まとめ

- ジェネリクスは `<T>` で型を引数として受け取り、型を保ちながら汎用的な関数を書ける
- `extends` で型引数に制約を付けられる。`keyof T` で型のプロパティ名を取得できる
- ユーティリティ型（Partial・Readonly・Pick・Omit・Record）で既存の型を変換できる

## 一次情報・参考資料

- [TypeScript: Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html)
- [TypeScript: Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)
