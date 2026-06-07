# 属性・id・class・data-*

## このステップのゴール

- 要素に属性を付加して挙動や情報を制御できます
- id・classで要素を識別・分類できます
- data-*属性でカスタムデータを要素に持たせられます
- リンクで別のページや同一ページ内に移動できます

## 前提知識・環境

- 03-nesting を完了していること

## 実践

`index.html` にコードを書きながら進めます。変更はLive Serverで確認します。

### 1. グローバル属性を使う

属性は `属性名="値"` の形式で要素の開始タグに書きます。すべての要素に使える属性を**グローバル属性**といいます。

```html
<!-- lang: 要素の言語を指定する -->
<p lang="en">This is written in English.</p>

<!-- title: マウスオーバーで表示されるツールチップ -->
<abbr title="HyperText Markup Language">HTML</abbr>

<!-- hidden: 要素を非表示にする -->
<p hidden>この段落は非表示です</p>
```

`hidden` のように値を省略できる属性を**論理属性**といいます。属性が存在するだけで有効になります。

### 2. id・classで要素を識別・分類する

`id` は1ページに1つだけの一意な識別子です。`class` は複数の要素に同じ名前を付けられます。

```html
<h1 id="page-title">ページのタイトル</h1>

<p class="note">注意事項1</p>
<p class="note">注意事項2</p>

<!-- 複数のclassをスペース区切りで指定できる -->
<p class="note important">重要な注意事項</p>
```

`id` はページ内リンクのターゲットに使えます。

```html
<a href="#section1">セクション1へ</a>

<h2 id="section1">セクション1</h2>
```

`id` と `class` は主にCSSでスタイルを当てたり、JavaScriptで要素を操作したりするために使います。

### 3. data-*属性でカスタムデータを持たせる

`data-` で始まる属性を使うと、要素に任意のデータを持たせられます。JavaScriptから `dataset` プロパティで参照できます。

```html
<ul>
  <li data-user-id="1" data-role="admin">Alice</li>
  <li data-user-id="2" data-role="editor">Bob</li>
  <li data-user-id="3" data-role="viewer">Carol</li>
</ul>
```

ブラウザの開発者ツールで要素を確認し、data-*属性がHTMLに付与されていることを確認します。

JavaScriptから参照する例です（JavaScriptコンテンツで学習済みの内容）。

```javascript
const items = document.querySelectorAll("li");
items.forEach((item) => {
  console.log(item.dataset.userId, item.dataset.role);
});
// 1 admin
// 2 editor
// 3 viewer
```

`data-user-id` のようにハイフンで繋いだ名前は、`dataset.userId` のようにキャメルケースで参照します。

### 4. リンクを作る

`a` 要素でリンクを作ります。`href` 属性にリンク先のURLを指定します。

```html
<p>詳細は<a href="https://developer.mozilla.org/ja/">MDN</a>を参照してください。</p>
```

外部サイトを別タブで開くには `target="_blank"` を指定します。セキュリティ上、`rel="noopener"` もあわせて指定します。

```html
<a href="https://developer.mozilla.org/ja/" target="_blank" rel="noopener">MDN（別タブで開く）</a>
```

`id` を使うと、同じページ内の特定箇所へのリンクも作れます。

```html
<a href="#section1">セクション1へ移動</a>

<h2 id="section1">セクション1</h2>
```

クリックして、`id` を指定した要素まで画面がスクロールすることを確認します。

## まとめ

- 属性は `属性名="値"` の形式で開始タグに書く。値を省略できる論理属性もある
- `id` は一意な識別子（ページに1つ）、`class` は複数要素への分類。CSSとJavaScriptとの接続点になる
- `data-*` 属性で要素にカスタムデータを持たせ、JavaScriptから `dataset` で参照できる
- `a` 要素の `href` でリンク先を指定する。`id` と `#` を組み合わせてページ内リンクも作れる

**次のステップ:** [05 セマンティック要素](../05-semantic/README.md) では、意味を持った構造化を学びます。

## 一次情報・参考資料

- [MDN: グローバル属性](https://developer.mozilla.org/ja/docs/Web/HTML/Global_attributes)
- [MDN: data-*](https://developer.mozilla.org/ja/docs/Web/HTML/Global_attributes/data-*)
- [MDN: HTMLElement.dataset](https://developer.mozilla.org/ja/docs/Web/API/HTMLElement/dataset)
- [MDN: \<a\>](https://developer.mozilla.org/ja/docs/Web/HTML/Element/a)
