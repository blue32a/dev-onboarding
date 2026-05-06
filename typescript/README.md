# TypeScript

TypeScriptはJavaScriptに静的型付けを追加した言語です。コンパイル時に型エラーを検出し、コードの意図を型で表現することで、バグを早期に防ぎ、チームでの開発を助けます。

このコンテンツでは、TypeScriptの型システムの基本をハンズオン形式で体験しながら、型安全なコードを書くための立ち上がりを支援します。

## 前提

- JavaScriptコンテンツ（01〜10）を完了していること
- Node.js v24（LTS）以上がインストールされていること

## ステップ一覧

| ステップ | 内容 |
| --- | --- |
| [01 セットアップ](./01-setup/README.md) | TypeScriptのインストール・tsc・tsconfig.json・実行方法 |
| [02 基本の型](./02-basic-types/README.md) | 型アノテーション・型推論・プリミティブ型・配列 |
| [03 anyとunknown](./03-any-unknown/README.md) | anyの問題点・unknownとの使い分け・型アサーション（as） |
| [04 オブジェクトの型](./04-object-types/README.md) | interface・type alias・オプショナルプロパティ・構造的型付け |
| [05 関数の型](./05-function-types/README.md) | 引数と戻り値の型・オプショナル引数・コールバック |
| [06 Union型](./06-union-types/README.md) | Union型・リテラル型・型の絞り込み・never |
| [07 交差型](./07-intersection-types/README.md) | 交差型（`&`）・型の組み合わせ |
| [08 エラーの読み方](./08-errors/README.md) | よくあるエラーパターン・エラーメッセージの読み解き方 |
| [09 ジェネリクス](./09-generics/README.md) | ジェネリクスの基本・ユーティリティ型 |
