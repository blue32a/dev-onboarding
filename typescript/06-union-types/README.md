# Union型

## このステップのゴール

- Union型で複数の型のうちどれかを表現できます
- typeofやinを使って型を絞り込めます
- neverを使って全ケースの網羅性をチェックできます

## 前提知識・環境

- 05-function-types を完了していること

## 実践

`main.ts` にコードを書きながら進めます。実行は `npx tsx main.ts` です。

### 1. Union型で受け入れる型を限定する

IDが数値の場合も文字列の場合もある関数を考えます。`any` を使うと意図しない型も通ってしまいます。

```typescript
function printId(id: any): void {
  console.log(`ID: ${id}`);
}

printId(1);     // OK
printId("abc"); // OK
printId(true);  // エラーにならない — booleanも通ってしまう
```

Union型を使うと、受け入れる型を「数値または文字列」に限定できます。

```typescript
function printId(id: number | string): void {
  console.log(`ID: ${id}`);
}

printId(1);     // OK
printId("abc"); // OK
printId(true);  // エラー: Argument of type 'boolean' is not assignable to parameter of type 'string | number'.
```

`|` で複数の型を組み合わせます。いずれかの型の値を受け入れつつ、それ以外を拒否できます。

### 2. リテラル型を使う

文字列や数値そのものを型として使えます。Union型と組み合わせることで、取りうる値を限定できます。

```typescript
type Direction = "north" | "south" | "east" | "west";

function move(direction: Direction): void {
  console.log(`${direction}に移動します`);
}

move("north"); // north に移動します
move("up");    // エラー: Argument of type '"up"' is not assignable to parameter of type 'Direction'.
```

### 3. 型の絞り込みを行う

Union型の値を操作する前に、実際の型を確認して絞り込みます。

`typeof` で型を確認します。

```typescript
function formatValue(value: number | string): string {
  if (typeof value === "string") {
    return value.toUpperCase();
  }
  return value.toFixed(2);
}

console.log(formatValue("hello")); // HELLO
console.log(formatValue(3.14));    // 3.14
```

`in` でプロパティの存在を確認します。

```typescript
interface Circle {
  kind: "circle";
  radius: number;
}

interface Rectangle {
  kind: "rectangle";
  width: number;
  height: number;
}

type Shape = Circle | Rectangle;

function getArea(shape: Shape): number {
  if ("radius" in shape) {
    return Math.PI * shape.radius ** 2;
  }
  return shape.width * shape.height;
}

console.log(getArea({ kind: "circle", radius: 5 }));           // 78.53...
console.log(getArea({ kind: "rectangle", width: 4, height: 3 })); // 12
```

### 4. 判別可能なUnion型を使う

共通のプロパティで型を区別する設計を**判別可能なUnion型**といいます。絞り込みが簡潔になります。

```typescript
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "rectangle"; width: number; height: number };

function getArea(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "rectangle":
      return shape.width * shape.height;
  }
}

console.log(getArea({ kind: "circle", radius: 5 }));
console.log(getArea({ kind: "rectangle", width: 4, height: 3 }));
```

### 5. neverで網羅性チェックをする

前のセクションの `getArea` に `default` を追加し、`Shape` に `triangle` を追加します。

```typescript
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "rectangle"; width: number; height: number }
  | { kind: "triangle"; base: number; height: number }; // 追加

function getArea(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "rectangle":
      return shape.width * shape.height;
    default:
      return 0; // triangle の処理を書き忘れたまま
  }
}

console.log(getArea({ kind: "triangle", base: 4, height: 3 })); // 0 — 正しくは 6 のはず
```

`triangle` の処理を書き忘れていますが、コンパイルエラーにはなりません。`default: return 0` が受け皿になり、誤った結果をサイレントに返します。

`never` を使うと、全ケースを処理しているかをコンパイル時に確認できます。`default` を書き換えます。

```typescript
function getArea(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "rectangle":
      return shape.width * shape.height;
    default:
      const _exhaustive: never = shape; // エラー: Type '{ kind: "triangle"; ... }' is not assignable to type 'never'.
      throw new Error(`未対応のShape: ${JSON.stringify(_exhaustive)}`);
  }
}
```

全ケースを `case` で処理すれば `default` に到達しないため `never` に代入できます。未処理のケースが残っていると `never` への代入がエラーになり、処理の追加漏れをコンパイル時に検出できます。`triangle` の `case` を追加してエラーが消えることを確認します。

## まとめ

- `|` でUnion型を定義し、複数の型のうちどれかを受け入れる。`any` と異なり、それ以外の型を拒否できる
- リテラル型とUnion型を組み合わせると、取りうる値を限定できる
- `typeof` や `in` で型を絞り込んでから操作する
- `never` を使った網羅性チェックで、ケースの追加漏れをコンパイル時に検出できる

**次のステップ:** [07 交差型](../07-intersection-types/README.md) では、複数の型を組み合わせる交差型を学びます。

## 一次情報・参考資料

- [TypeScript: Union Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types)
- [TypeScript: Narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
- [TypeScript: never](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-never-type)
