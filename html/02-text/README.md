# テキスト

## このステップのゴール

- 見出しと段落でテキストを階層化できます
- リストで項目を整理できます

## 前提知識・環境

- 01-document-structure を完了していること

## 実践

`index.html` にコードを書きながら進めます。変更はLive Serverで確認します。

### 1. 見出しと段落で文章を構造化する

テキストだけを `<body>` に書くと、すべて同じ見た目になります。

```html
<body>
  HTMLの基本
  HTMLはWebページを作るための言語です。
  見出しとは何か
  見出しはコンテンツのタイトルを表します。
</body>
```

見た目の区別がなく、どこが題名でどこが本文かわかりません。`h1`〜`h6` と `p` を使って意味ごとに分けます。

```html
<body>
  <h1>HTMLの基本</h1>
  <p>HTMLはWebページを作るための言語です。</p>
  <h2>見出しとは何か</h2>
  <p>見出しはコンテンツのタイトルを表します。</p>
</body>
```

`h1`〜`h6` は重要度の順に使います。`h1` はページに1つ、`h2`〜`h6` はセクションの深さに応じて使います。

### 2. リストで項目を整理する

順序のない項目には `ul`（unordered list）、順序のある手順には `ol`（ordered list）を使います。

```html
<h2>好きな食べ物</h2>
<ul>
  <li>寿司</li>
  <li>ラーメン</li>
  <li>カレー</li>
</ul>

<h2>HTMLを学ぶ手順</h2>
<ol>
  <li>ドキュメント構造を学ぶ</li>
  <li>テキスト要素を学ぶ</li>
  <li>フォームを学ぶ</li>
</ol>
```

## まとめ

- `h1`〜`h6` で見出しの階層を作り、`p` で段落を表す
- `ul` は順序なし、`ol` は順序ありのリスト。項目は `li` で囲む

**次のステップ:** [03 入れ子構造](../03-nesting/README.md) では、要素の正しい入れ子ルールを学びます。

## 一次情報・参考資料

- [MDN: HTMLテキストの基礎](https://developer.mozilla.org/ja/docs/Learn_web_development/Core/Structuring_content/Headings_and_paragraphs)
- [MDN: リストの作成](https://developer.mozilla.org/ja/docs/Learn_web_development/Core/Structuring_content/Lists)
