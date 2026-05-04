# インストール

## このステップのゴール

- `npm install` でパッケージをインストールしてコードから使えます
- `node_modules` と `package-lock.json` の役割を理解して適切に管理できます
- `.gitignore` を設定して `node_modules` をGitの管理対象から除外できます

## 前提知識・環境

- 01-what-is-npm を完了していること

## 実践

### 1. パッケージをインストールする

`npm install <パッケージ名>` でパッケージをインストールできます。

ここでは `uuid`（ユニークIDを生成するパッケージ）を使って仕組みを確認します。

```
npm install uuid
```

インストール後、`package.json` に `dependencies` フィールドが追加されます。

```json
{
  "dependencies": {
    "uuid": "^9.0.0"
  }
}
```

`main.js` を作成してインポートします。ES Modulesを使うため、`package.json` に `"type": "module"` を追加してから実行します。

```json
{
  "type": "module",
  "dependencies": {
    "uuid": "^9.0.0"
  }
}
```

```javascript
import { v4 as uuidv4 } from "uuid";

console.log(uuidv4()); // 例: "110e8400-e29b-41d4-a716-446655440000"
console.log(uuidv4()); // 実行するたびに異なるIDが生成される
```

```
node main.js
```

### 2. node_modules を確認する

インストールしたパッケージの実体は `node_modules/` ディレクトリに保存されます。

```
node_modules/
└── uuid/
    └── ...（パッケージのファイル群）
```

`node_modules` はサイズが大きくなるため、Gitには含めません。`.gitignore` に追加します。

```
node_modules/
```

`.gitignore` に追加することで、`git add` の対象から除外されます。

### 3. package-lock.json を理解する

`npm install` を実行すると `package-lock.json` が生成されます。このファイルにはインストールされたパッケージの正確なバージョンが記録されます。

`package.json` には `"uuid": "^9.0.0"` のように範囲で記述されますが、実際にインストールされたバージョンは `package-lock.json` に固定されます。

`package-lock.json` をGitに含めることで、他の開発者が同じ環境で `npm install` を実行したときに同じバージョンがインストールされます。

```
# 既存プロジェクトをクローンしたあとの手順
npm install   # package-lock.json を元に node_modules を復元
```

## まとめ

- `npm install <パッケージ名>` でパッケージをインストールし、`import` で使える
- `node_modules/` はインストールされたパッケージの実体。サイズが大きいためGitには含めない
- `package-lock.json` はインストール時のバージョンを固定するファイル。Gitに含める

**次のステップ:** [03 依存関係](../03-dependencies/README.md) では、依存関係の種類とバージョン管理を学びます。

## 一次情報・参考資料

- [npm install](https://docs.npmjs.com/cli/v10/commands/npm-install)
- [package-lock.json](https://docs.npmjs.com/cli/v10/configuring-npm/package-lock-json)
