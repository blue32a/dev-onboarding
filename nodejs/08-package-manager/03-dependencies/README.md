# 依存関係

## このステップのゴール

- `dependencies` と `devDependencies` の違いを説明できます
- semver の表記（`^`・`~`）を読んで意味を説明できます
- `npm install --save-dev` で開発用パッケージをインストールできます

## 前提知識・環境

- 02-install を完了していること

## 実践

### 1. dependencies と devDependencies

`package.json` の依存関係には2種類あります。

| フィールド | 用途 | 例 |
| --- | --- | --- |
| `dependencies` | 本番環境でも必要なパッケージ | express, uuid |
| `devDependencies` | 開発時のみ必要なパッケージ | typescript, eslint, jest |

`--save-dev`（または `-D`）オプションで `devDependencies` に追加できます。

```
npm install --save-dev eslint
```

```json
{
  "dependencies": {
    "uuid": "^9.0.0"
  },
  "devDependencies": {
    "eslint": "^8.0.0"
  }
}
```

本番環境では `npm install --omit=dev` を使うことで `devDependencies` のパッケージを除いてインストールできます。これによりデプロイサイズを削減できます。

### 2. semver を読む

npmのバージョンは **semver**（Semantic Versioning）という規則に従っています。

```
1.2.3
│ │ └── patch: バグ修正
│ └──── minor: 後方互換性のある機能追加
└────── major: 後方互換性のない変更（破壊的変更）
```

`package.json` に記述されるバージョン範囲の記号：

| 記法 | 意味 | 例 |
| --- | --- | --- |
| `^1.2.3` | major が同じ範囲で最新 | `>=1.2.3 <2.0.0` |
| `~1.2.3` | minor が同じ範囲で最新 | `>=1.2.3 <1.3.0` |
| `1.2.3` | 完全に固定 | `1.2.3` のみ |

`^` が最もよく使われます。minor やpatchの更新は取り込みつつ、破壊的変更（major更新）は避けるという意図です。

### 3. パッケージを更新する

インストール済みパッケージのうち更新があるものを確認できます。

```
npm outdated
```

```
Package  Current  Wanted  Latest
uuid     9.0.0    9.0.1   9.0.1
```

`npm update` で `package.json` のバージョン範囲内で最新のバージョンに更新します。

```
npm update
```

## まとめ

- `dependencies` は本番・開発両方で使う依存関係、`devDependencies` は開発時のみ
- semver は `major.minor.patch` の形式で、`^` は major を固定しつつ minor/patch の更新を受け入れる
- `npm outdated` で更新確認、`npm update` でバージョン範囲内の最新に更新できる

**次のステップ:** [04 npm scripts](../04-scripts/README.md) では、よく使うコマンドをスクリプトとして登録する方法を学びます。

## 一次情報・参考資料

- [Semantic Versioning](https://semver.org/lang/ja/)
- [npm: dependencies と devDependencies](https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file)
- [npm update](https://docs.npmjs.com/cli/v10/commands/npm-update)
