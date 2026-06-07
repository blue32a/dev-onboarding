# ドキュメント構造

## このステップのゴール

- Live ServerでHTMLをブラウザで確認できます
- HTMLドキュメントの基本構造を作れます
- 文字コード・ビューポート・タイトルを設定できます

## 前提知識・環境

- VS Codeがインストールされていること
- JavaScriptコンテンツ（01〜10）を完了していること

## 実践

このステップは `01-document-structure/` ディレクトリを起点に進めます。

### 1. Live Serverをセットアップする

HTMLはブラウザで表示して確認します。VS Code拡張「Live Server」を使うと、ファイルを保存するたびにブラウザが自動更新されます。

VS Codeの拡張機能タブで「Live Server」（作者: Ritwick Dey）を検索してインストールします。

`01-document-structure/index.html` をVS Codeで開き、右クリック →「Open with Live Server」を選択します。ブラウザが起動してHTMLファイルが表示されます。以降はファイルを保存するたびに自動で更新されます。

### 2. HTMLドキュメントの骨格を作る

`index.html` に以下を書きます。

```html
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    こんにちは
  </body>
</html>
```

ブラウザに「こんにちは」と表示されることを確認します。

| 部分 | 役割 |
| --- | --- |
| `<!DOCTYPE html>` | HTML5文書であることをブラウザに宣言する |
| `<html>` | ドキュメント全体を囲むルート要素 |
| `<head>` | ブラウザ向けの設定情報を置く領域（画面に表示されない） |
| `<body>` | 画面に表示されるコンテンツを置く領域 |

### 3. メタ情報を設定する

セクション2のコードに `lang` 属性とメタ情報を追加して、完成形にします。

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>はじめてのHTML</title>
  </head>
  <body>
    こんにちは
  </body>
</html>
```

ブラウザのタブに「はじめてのHTML」と表示されることを確認します。

| 設定 | 役割 |
| --- | --- |
| `lang="ja"` | ページの言語を日本語に指定する。スクリーンリーダーや検索エンジンが参照する |
| `meta charset="UTF-8"` | 文字コードをUTF-8に指定する。日本語を正しく表示するために必要 |
| `meta name="viewport"` | スマートフォンなど画面幅に合わせて表示を調整する |
| `title` | ブラウザのタブに表示されるページタイトル |

## まとめ

- `<!DOCTYPE html>` から始まり `html > head + body` の構造がHTMLドキュメントの骨格
- `head` にはメタ情報を、`body` には表示するコンテンツを書く
- `meta charset="UTF-8"` で文字コードを指定し、`meta name="viewport"` でモバイル対応する
- Live Serverを使うとファイル保存のたびにブラウザが自動更新される

**次のステップ:** [02 テキスト](../02-text/README.md) では、見出し・段落・リストを学びます。

## 一次情報・参考資料

- [MDN: HTMLの基本](https://developer.mozilla.org/ja/docs/Learn_web_development/Getting_started/Your_first_website/Creating_the_content)
- [MDN: \<meta\>](https://developer.mozilla.org/ja/docs/Web/HTML/Element/meta)
- [Live Server - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
