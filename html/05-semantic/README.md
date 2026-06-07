# セマンティック要素

## このステップのゴール

- セマンティック要素でページの構造を意味的に表現できます
- `div` とセマンティック要素を使い分けられます

## 前提知識・環境

- 04-attributes を完了していること

## 実践

`index.html` にコードを書きながら進めます。変更はLive Serverで確認します。

### 1. divだけで作る問題点を確認する

次のコードを書きます。

```html
<div class="header">
  <div class="nav">
    <a href="#">ホーム</a>
    <a href="#">について</a>
  </div>
</div>
<div class="main">
  <div class="article">
    <h1>記事のタイトル</h1>
    <p>記事の本文です。</p>
  </div>
</div>
<div class="footer">
  <p>© 2024 サイト名</p>
</div>
```

ブラウザ上の表示には問題ありませんが、`div` はコンテンツの意味を持ちません。ブラウザの開発者ツールでElementsタブを開くと、すべて `div` の羅列になっています。スクリーンリーダーはこの構造から「どこがナビゲーションで、どこがメインコンテンツか」を判断できません。

### 2. ページ全体をセマンティックに構造化する

`div` をセマンティック要素に置き換えます。

```html
<header>
  <nav>
    <a href="#">ホーム</a>
    <a href="#">について</a>
  </nav>
</header>
<main>
  <article>
    <h1>記事のタイトル</h1>
    <p>記事の本文です。</p>
  </article>
</main>
<footer>
  <p>© 2024 サイト名</p>
</footer>
```

| 要素 | 役割 |
| --- | --- |
| `header` | ページまたはセクションのヘッダー。ロゴ・タイトル・ナビゲーションを含む |
| `nav` | 主要なナビゲーションリンクのまとまり |
| `main` | ページのメインコンテンツ。1ページに1つ |
| `footer` | ページまたはセクションのフッター。著作権・連絡先などを含む |

### 3. コンテンツをセマンティックに分割する

```html
<main>
  <article>
    <h1>TypeScriptとは</h1>
    <p>TypeScriptはJavaScriptに型を追加した言語です。</p>

    <section>
      <h2>特徴</h2>
      <p>静的型付けによりバグを早期発見できます。</p>
    </section>

    <section>
      <h2>使い方</h2>
      <p>tscコマンドでコンパイルします。</p>
    </section>
  </article>

  <aside>
    <h2>関連リンク</h2>
    <ul>
      <li><a href="#">TypeScript公式サイト</a></li>
    </ul>
  </aside>
</main>
```

| 要素 | 役割 |
| --- | --- |
| `article` | 単独で成立するコンテンツ。ブログ記事・ニュース記事など |
| `section` | テーマでまとまったコンテンツのひとまとまり |
| `aside` | メインコンテンツに関連するが補足的な情報。サイドバーなど |

## まとめ

- `div` は意味を持たない汎用コンテナ。意味を持つ場所にはセマンティック要素を使う
- `header`・`nav`・`main`・`footer` でページ全体の骨格を作る
- `article`・`section`・`aside` でコンテンツを意味ごとに分割する

**次のステップ:** [06 フォーム](../06-forms/README.md) では、ユーザー入力を受け付けるフォームを学びます。

## 一次情報・参考資料

- [MDN: コンテンツセクショニング](https://developer.mozilla.org/ja/docs/Web/HTML/Element#コンテンツセクショニング)
- [MDN: \<article\>](https://developer.mozilla.org/ja/docs/Web/HTML/Element/article)
- [MDN: \<section\>](https://developer.mozilla.org/ja/docs/Web/HTML/Element/section)
