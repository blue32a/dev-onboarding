# 関数の型

## このステップのゴール

- 引数と戻り値に型を付けられます
- オプショナル引数とデフォルト値を型安全に扱えます
- コールバック引数に型を指定して、渡し間違いをコンパイル時に検出できます

## 前提知識・環境

- 04-object-types を完了していること

## 実践

`main.ts` にコードを書きながら進めます。実行は `npx tsx main.ts` です。

### 1. 引数と戻り値の型を書く

次のコードを書いて実行します。

```typescript
function add(a: any, b: any): any {
  return a + b;
}

console.log(add(1, 2));   // 3
console.log(add("1", 2)); // "12" — 数値加算のつもりが文字列結合になる
```

引数が `any` だと、誤った型を渡しても検出できません。引数と戻り値に型を付けることで、呼び出し側の誤りをコンパイル時に検出できます。

```typescript
function add(a: number, b: number): number {
  return a + b;
}

console.log(add("1", 2)); // エラー: Argument of type 'string' is not assignable to parameter of type 'number'.
console.log(add(1, 2));   // 3
```

引数は `引数名: 型`、戻り値は `)` の後に `: 型` で指定します。戻り値がない関数には `void` を使います。

```typescript
function log(message: string): void {
  console.log(message);
}
```

### 2. オプショナル引数とデフォルト値

`?` を付けると省略可能な引数になります。省略した場合の値は `undefined` です。

```typescript
function greet(name: string, greeting?: string): string {
  const g = greeting ?? "こんにちは";
  return `${g}、${name}さん`;
}

console.log(greet("Alice"));            // こんにちは、Aliceさん
console.log(greet("Alice", "おはよう")); // おはよう、Aliceさん
```

デフォルト値はJavaScriptと同じ構文で指定できます。デフォルト値がある引数は型アノテーションを省略できます。

```typescript
function greet(name: string, greeting = "こんにちは"): string {
  return `${greeting}、${name}さん`;
}
```

### 3. コールバック関数の型を定義する

コールバック関数の型は `(引数: 型) => 戻り値の型` で表します。

```typescript
function applyTwice(value: number, fn: (n: number) => number): number {
  return fn(fn(value));
}

console.log(applyTwice(3, (n) => n * 2)); // 12
```

### 4. 関数型をtype aliasで定義する

複数の場所で同じ関数型を使う場合は `type` で定義します。

```typescript
type Formatter = (value: string) => string;

const toUpper: Formatter = (v) => v.toUpperCase();
const trim: Formatter = (v) => v.trim();

function format(value: string, formatters: Formatter[]): string {
  return formatters.reduce((acc, fn) => fn(acc), value);
}

console.log(format("  hello world  ", [trim, toUpper])); // HELLO WORLD
```

## まとめ

- 引数は `引数名: 型`、戻り値は `: 型` で指定する。戻り値がない場合は `void`
- `?` でオプショナル引数、デフォルト値はJavaScriptと同じ構文で指定できる
- コールバック関数の型は `(引数: 型) => 戻り値の型` で表す

**次のステップ:** [06 Union型](../06-union-types/README.md) では、複数の型のどれかを表すUnion型を学びます。

## 一次情報・参考資料

- [TypeScript: More on Functions](https://www.typescriptlang.org/docs/handbook/2/functions.html)
