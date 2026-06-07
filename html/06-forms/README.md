# フォーム

## このステップのゴール

- フォームでユーザー入力を受け付けられます
- inputのtypeを目的に合わせて使い分けられます
- labelとバリデーション属性でユーザーの入力ミスを防げます

## 前提知識・環境

- 05-semantic を完了していること

## 実践

`index.html` にコードを書きながら進めます。変更はLive Serverで確認します。

### 1. フォームの基本構造を作る

`type="text"` のinputだけを並べたフォームを考えます。

```html
<input type="text" />
<input type="text" />
<button>送信</button>
```

入力欄が2つありますが、それぞれ何を入力する欄かわかりません。`form`・`label`・適切な `input` を組み合わせます。

```html
<form>
  <label for="name">名前</label>
  <input type="text" id="name" name="name" />

  <label for="email">メールアドレス</label>
  <input type="email" id="email" name="email" />

  <button type="submit">送信</button>
</form>
```

`label` の `for` と `input` の `id` を一致させると、ラベルをクリックしたときに対応する入力欄にフォーカスが移ります。確認します。

### 2. inputのtypeを使い分ける

`type` で入力形式を制限し、適切なUIをブラウザが提供します。

```html
<form>
  <label for="password">パスワード</label>
  <input type="password" id="password" name="password" />

  <label for="age">年齢</label>
  <input type="number" id="age" name="age" min="0" max="120" />

  <label for="birthday">生年月日</label>
  <input type="date" id="birthday" name="birthday" />

  <fieldset>
    <legend>通知設定</legend>
    <label>
      <input type="checkbox" name="notify-email" />
      メール通知
    </label>
    <label>
      <input type="checkbox" name="notify-push" />
      プッシュ通知
    </label>
  </fieldset>

  <fieldset>
    <legend>性別</legend>
    <label><input type="radio" name="gender" value="male" />男性</label>
    <label><input type="radio" name="gender" value="female" />女性</label>
    <label><input type="radio" name="gender" value="other" />その他</label>
  </fieldset>

  <label for="message">メッセージ</label>
  <textarea id="message" name="message" rows="4"></textarea>

  <label for="country">国</label>
  <select id="country" name="country">
    <option value="jp">日本</option>
    <option value="us">アメリカ</option>
    <option value="uk">イギリス</option>
  </select>

  <button type="submit">送信</button>
</form>
```

各inputをクリック・操作し、ブラウザがどのようなUIを提供するか確認します。

### 3. バリデーション属性で入力を制限する

`required` や `pattern` を使うと、ブラウザが送信前に入力値を検証します。

```html
<form>
  <label for="username">ユーザー名（必須）</label>
  <input
    type="text"
    id="username"
    name="username"
    required
    minlength="3"
    maxlength="20"
    placeholder="3〜20文字で入力"
  />

  <label for="tel">電話番号</label>
  <input
    type="tel"
    id="tel"
    name="tel"
    pattern="[0-9\-]+"
    placeholder="090-1234-5678"
  />

  <button type="submit">送信</button>
</form>
```

何も入力せずに送信ボタンをクリックし、ブラウザのバリデーションメッセージを確認します。

## まとめ

- `form` 要素でフォームの範囲を定義する
- `label` の `for` と `input` の `id` を一致させると、ラベルクリックで入力欄にフォーカスする
- `input` の `type` で入力形式を制限し、ブラウザが適切なUIを提供する
- `required`・`minlength`・`pattern` などのバリデーション属性で送信前に入力値を検証できる

**次のステップ:** [07 メディア](../07-media/README.md) では、画像・動画をページに埋め込む方法を学びます。

## 一次情報・参考資料

- [MDN: Webフォーム](https://developer.mozilla.org/ja/docs/Learn_web_development/Extensions/Forms)
- [MDN: \<input\>](https://developer.mozilla.org/ja/docs/Web/HTML/Element/input)
- [MDN: クライアント側フォームバリデーション](https://developer.mozilla.org/ja/docs/Learn_web_development/Extensions/Forms/Form_validation)
