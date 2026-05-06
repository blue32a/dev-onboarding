# オブジェクトの型

## このステップのゴール

- interfaceでオブジェクトの型を定義できます
- type aliasとinterfaceを使い分けられます
- 構造的型付けの動作を理解し、型の互換性を正しく予測できます

## 前提知識・環境

- 03-any-unknown を完了していること

## 実践

`main.ts` にコードを書きながら進めます。実行は `npx tsx main.ts` です。

### 1. interfaceでオブジェクトの型を定義する

`interface` はオブジェクトの型を定義します。JavaやC#と同様にクラスの実装契約（`implements`）にも使えますが、TypeScriptではオブジェクトの型を記述する用途でも広く使われます。このステップでは後者を扱います。

次のコードを書いて実行します。

```typescript
const user = {
  id: 1,
  name: "Alice",
  emai: "alice@example.com", // typo: emai ではなく email
};

console.log(user.email); // undefined — typoに気づかない
```

プロパティ名のtypoが実行時まで検出できません。`interface` でオブジェクトの型を定義すると、コンパイル時に検出できます。

```typescript
interface User {
  id: number;
  name: string;
  email: string;
}

const user: User = {
  id: 1,
  name: "Alice",
  emai: "alice@example.com", // エラー: Object literal may only specify known properties, and 'emai' does not exist in type 'User'.
};
```

プロパティが足りない場合や型が違う場合もエラーになります。

```typescript
const invalid: User = {
  id: 1,
  name: "Alice",
  // email が足りない → エラー
};
```

### 2. type aliasを使う

`type` キーワードでも同様にオブジェクトの型を定義できます。

```typescript
type Point = {
  x: number;
  y: number;
};

const origin: Point = { x: 0, y: 0 };
console.log(origin);
```

`interface` と `type` の主な違いを確認します。

| | interface | type |
| --- | --- | --- |
| オブジェクトの型定義 | ✓ | ✓ |
| Union型・交差型 *¹ | ✗ | ✓ |
| 拡張（extends） | ✓ | `&` *¹ で代替可 |
| 同名による宣言マージ | ✓ | ✗ |

*¹ Union型・交差型は後のステップで学習します。

オブジェクトの型定義には `interface`、Union型など複合的な型には `type` を使うのが一般的です。

### 3. オプショナルプロパティとreadonly

`?` を付けると省略可能なプロパティになります。`readonly` を付けると変更できないプロパティになります。

```typescript
interface Product {
  readonly id: number;
  name: string;
  description?: string;
}

const product: Product = {
  id: 1,
  name: "TypeScriptハンドブック",
};

console.log(product.description); // undefined

product.id = 2; // エラー: Cannot assign to 'id' because it is a read-only property.
```

### 4. 構造的型付けを体験する

TypeScriptは**構造的型付け**を採用しています。型名ではなく、プロパティの構造が一致していれば代入できます。

```typescript
interface Named {
  name: string;
}

interface User {
  id: number;
  name: string;
  email: string;
}

function greet(value: Named): void {
  console.log(`こんにちは、${value.name}さん`);
}

const user: User = { id: 1, name: "Alice", email: "alice@example.com" };

greet(user); // User は name を持つため Named として扱える
```

`User` は `Named` に必要な `name` プロパティを持つため、`Named` の場所に渡せます。JavaやC#のような**公称型付け**（型名が一致しなければ代入できない）とは異なる動作です。

## まとめ

- `interface` でオブジェクトの型を定義する。プロパティ名のtypoや不足をコンパイル時に検出できる
- `type` でも同様に定義できる。Union型などの複合的な型には `type` を使う
- TypeScriptは構造的型付けのため、型名ではなくプロパティの構造が一致すれば代入できる

**次のステップ:** [05 関数の型](../05-function-types/README.md) では、関数の引数と戻り値に型を付ける方法を学びます。

## 一次情報・参考資料

- [TypeScript: Object Types](https://www.typescriptlang.org/docs/handbook/2/objects.html)
- [TypeScript: Interfaces](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#interfaces)
- [TypeScript: Type Aliases](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-aliases)
