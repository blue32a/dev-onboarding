# npmとは

## このステップのゴール

- パッケージマネージャーが解決する問題を説明できます
- レジストリから必要なパッケージを見つけてインストールできます
- `package.json` を読んでプロジェクトの依存関係と実行コマンドを把握できます

## 前提知識・環境

- 07-streams を完了していること

## 実践

### 1. npmの役割を確認する

JavaScriptのエコシステムには、他の開発者が公開した再利用可能なコードがあります。これを**パッケージ**と呼びます。パッケージマネージャーがない場合、パッケージを使うには手動でのダウンロード・依存関係の解決・バージョン管理が必要です。**npm**（Node Package Manager）を使うと、これらをコマンド一つで解決できます。

npmはレジストリとCLIツールの2つからなります。**レジストリ**は `https://www.npmjs.com/` で公開されているパッケージのデータベースです。**CLIツール**はターミナルから `npm` コマンドを実行してレジストリからパッケージを取得する仕組みです。Node.jsをインストールすると `npm` も同時にインストールされます。

バージョンを確認します。

```
npm --version
```

### 2. package.json を生成する

`package.json` はプロジェクトのマニフェスト（設定ファイル）です。このプロジェクトが何であるか、どのパッケージに依存しているかを記述します。`npm init -y` で自動生成できます。

```
npm init -y
```

生成された `package.json` の主要フィールドを確認します。

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

| フィールド | 役割 |
| --- | --- |
| `name` | パッケージ名 |
| `version` | バージョン番号 |
| `description` | 説明文 |
| `main` | エントリポイントのファイルパス |
| `scripts` | npm scripts（後のステップで学びます） |

## まとめ

- パッケージマネージャーは依存パッケージのダウンロード・管理を自動化する
- npmはレジストリ（パッケージのデータベース）とCLIツールの2つからなる
- `package.json` はプロジェクトのマニフェストで、`npm init -y` で生成できる

**次のステップ:** [02 インストール](../02-install/README.md) では、パッケージのインストールと生成されるファイルを確認します。

## 一次情報・参考資料

- [npm 公式サイト](https://www.npmjs.com/)
- [npm ドキュメント](https://docs.npmjs.com/)
- [package.json フィールド一覧](https://docs.npmjs.com/cli/v10/configuring-npm/package-json)
