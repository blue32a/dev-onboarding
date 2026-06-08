# セットアップ

## このステップのゴール

- Reactプロジェクトを作成できます
- 開発サーバーを起動してブラウザで確認できます
- Reactプロジェクトのファイル構成を把握できます

## 前提知識・環境

- Node.jsがインストールされていること（`node -v` で確認）

## 実践

このステップには `workspace/` ディレクトリが用意されています。

### 1. プロジェクトを作成する

ViteはReactプロジェクトの土台を作り、開発サーバーを提供するツールです。

ターミナルで `workspace/` ディレクトリに移動し、Viteを使ってReactプロジェクトを作成します。

```sh
cd workspace
npm create vite@latest app -- --template react
cd app
npm install
```

`npm create vite@latest app -- --template react` は `app` という名前のプロジェクトをViteのReactテンプレートで作成するコマンドです。`npm install` は `package.json` に記載された依存パッケージをインストールします。

`workspace/app/` にプロジェクトが作成されます。

### 2. 開発サーバーを起動する

```sh
npm run dev
```

ブラウザで `http://localhost:5173` を開き、Reactのデフォルト画面が表示されることを確認します。ファイルを保存するたびにブラウザが自動更新されます。

### 3. ファイル構成を確認する

```
app/
├── index.html          # HTMLのエントリーポイント
├── package.json        # 依存関係の定義
├── vite.config.js      # Viteの設定
└── src/
    ├── main.jsx        # ReactをHTMLにマウントする起点
    ├── App.jsx         # メインのコンポーネント（主にここを編集する）
    └── App.css         # App用のスタイル
```

`src/App.jsx` を開きます。Viteのデフォルトコードが書かれています。このコードは次のステップで書き換えます。

## まとめ

- `npm create vite@latest` でReactプロジェクトを作成する
- `npm run dev` で開発サーバーを起動する
- `src/App.jsx` がメインの編集対象

**次のステップ:** [02 JSX](../02-jsx/README.md) では、ReactのマークアップであるJSXを学びます。

## 一次情報・参考資料

- [Vite: はじめに](https://ja.vitejs.dev/guide/)
- [React: クイックスタート](https://ja.react.dev/learn)
