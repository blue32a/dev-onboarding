# アクセシビリティ

## このステップのゴール

- スクリーンリーダーに伝わる代替テキストを書けます
- WAI-ARIAで要素の役割・状態を補足できます
- キーボードで操作できるページを確認できます

## 前提知識・環境

- 08-table を完了していること

## 実践

`index.html` にコードを書きながら進めます。変更はLive Serverで確認します。

### 1. 代替テキストを目的に応じて書く

`alt` 属性は画像が表示できない場合やスクリーンリーダーが読み上げる際に使われます。画像の見た目ではなく、**文脈における役割**を説明します。

```html
<!-- 情報を伝える画像: 内容を説明する -->
<img src="sales-chart.png" alt="2024年売上グラフ。Q4が前年比120%で最高値" />

<!-- リンク内の画像: リンク先を説明する -->
<a href="/home">
  <img src="logo.png" alt="ホームに戻る" />
</a>

<!-- 装飾的な画像: alt=""（空）にしてスキップさせる -->
<img src="divider.png" alt="" />
```

### 2. ランドマークで構造を伝える

セマンティック要素（`header`・`main`・`nav` など）は自動的にランドマークになります。スクリーンリーダーのユーザーはランドマークを使ってページ内を素早く移動できます。

`div` など意味のない要素をランドマークとして使いたい場合は `role` 属性で補足します。

```html
<div role="navigation" aria-label="メインメニュー">
  <a href="#">ホーム</a>
  <a href="#">ブログ</a>
</div>
```

`aria-label` で要素に名前を付けられます。同じランドマークが複数ある場合に区別するためにも使います。

```html
<nav aria-label="メインナビゲーション">
  <a href="#">ホーム</a>
</nav>
<nav aria-label="フッターナビゲーション">
  <a href="#">プライバシーポリシー</a>
</nav>
```

### 3. aria-*属性で状態を補足する

WAI-ARIAの属性で、HTMLだけでは伝えられない状態や関係を補足します。

```html
<!-- 開閉状態を伝える -->
<button aria-expanded="false" aria-controls="menu">メニュー</button>
<ul id="menu" hidden>
  <li><a href="#">ホーム</a></li>
  <li><a href="#">ブログ</a></li>
</ul>

<!-- 装飾的なアイコンを読み飛ばさせる -->
<button>
  <span aria-hidden="true">★</span>
  お気に入りに追加
</button>

<!-- 追加の説明を関連付ける -->
<label for="password">パスワード</label>
<input type="password" id="password" aria-describedby="password-hint" />
<p id="password-hint">8文字以上、英数字を含む</p>
```

### 4. キーボードナビゲーションを確認する

マウスを使わず `Tab` キーだけでページ内の全操作ができるか確認します。次のHTMLを書き、Tabキーで順番に移動できることを確認します。

```html
<nav>
  <a href="#">ホーム</a>
  <a href="#">ブログ</a>
</nav>
<main>
  <h1>お問い合わせ</h1>
  <form>
    <label for="name">名前</label>
    <input type="text" id="name" />
    <label for="message">メッセージ</label>
    <textarea id="message"></textarea>
    <button type="submit">送信</button>
  </form>
</main>
```

リンク・入力欄・ボタンがTabキーで順番にフォーカスされることを確認します。フォーカスが当たった要素にはブラウザが枠線（フォーカスリング）を表示します。

## まとめ

- `alt` は画像の見た目ではなく文脈における役割を書く。装飾的な画像は `alt=""`
- セマンティック要素はランドマークになる。`role` と `aria-label` で補足できる
- `aria-expanded`・`aria-hidden`・`aria-describedby` で状態や関係を補足する
- Tabキーでページ内の全操作ができることを確認する

## 一次情報・参考資料

- [MDN: WAI-ARIAの基本](https://developer.mozilla.org/ja/docs/Learn_web_development/Core/Accessibility/WAI-ARIA_basics)
- [WAI-ARIA オーサリングプラクティス](https://www.w3.org/WAI/ARIA/apg/)
- [MDN: アクセシビリティ](https://developer.mozilla.org/ja/docs/Web/Accessibility)
