# メディア

## このステップのゴール

- 画像を適切にページに埋め込めます
- 動画をページに追加できます
- 画面サイズに応じた画像を提供できます

## 前提知識・環境

- 06-forms を完了していること

## 実践

このステップには `index.html` と画像ファイルが用意されています。コードを書きながら進めます。変更はLive Serverで確認します。

### 1. 画像を埋め込む

`img` 要素で画像を埋め込みます。

```html
<img src="photo.jpg" width="400" height="300" alt="東京タワーの写真" />
```

`alt` 属性は画像が表示できないときや、スクリーンリーダーが読み上げるときに使われます。内容を説明するテキストを必ず書きます。

画像の内容に応じて `alt` の書き方を使い分けます。

```html
<!-- 情報を伝える画像: 内容を説明する -->
<img src="chart.png" alt="2024年の月別売上グラフ。12月が最高値" />

<!-- リンク内の画像: リンク先を説明する -->
<a href="/home">
  <img src="logo.png" alt="ホームに戻る" />
</a>

<!-- 装飾的な画像: alt=""（空）にしてスクリーンリーダーにスキップさせる -->
<img src="divider.png" alt="" />
```

### 2. 図と説明を組み合わせる

`figure` と `figcaption` で画像とキャプションをセットにします。

```html
<figure>
  <img src="photo.jpg" width="400" height="300" alt="富士山の写真" />
  <figcaption>静岡県から見た富士山（2024年1月撮影）</figcaption>
</figure>
```

### 3. 動画を埋め込む

`video` 要素で動画を埋め込みます。`source` 要素でファイルを指定します。

```html
<video width="640" height="360" controls>
  <source src="movie.mp4" type="video/mp4" />
  お使いのブラウザは動画の再生に対応していません。
</video>
```

| 属性 | 役割 |
| --- | --- |
| `controls` | 再生・停止・音量などのコントロールを表示する |
| `autoplay` | ページ読み込み時に自動再生する |
| `muted` | 音声をミュートにする（`autoplay` と組み合わせて使うことが多い） |
| `loop` | 動画を繰り返し再生する |

### 4. 画面サイズに応じた画像を提供する

`picture` 要素と `source` を使うと、画面幅に応じて異なる画像を提供できます。

```html
<picture>
  <source media="(min-width: 800px)" srcset="large.jpg" />
  <source media="(min-width: 400px)" srcset="medium.jpg" />
  <img src="small.jpg" alt="風景写真" />
</picture>
```

ブラウザは条件に合った最初の `source` を使用します。どの条件にも当てはまらない場合は `img` がフォールバックとして使われます。ブラウザの開発者ツールでウィンドウ幅を変えながら、読み込まれる画像が切り替わることを確認します。

## まとめ

- `img` の `alt` 属性は必ず書く。意味のある画像は内容を説明し、装飾的な画像は `alt=""` にする
- `figure`・`figcaption` で画像とキャプションをセットにできる
- `video` の `controls` でコントロールを表示する。`autoplay` には `muted` を組み合わせる
- `picture` 要素で画面サイズに応じた画像を提供できる

**次のステップ:** [08 テーブル](../08-table/README.md) では、データをテーブルで表現する方法を学びます。

## 一次情報・参考資料

- [MDN: \<img\>](https://developer.mozilla.org/ja/docs/Web/HTML/Element/img)
- [MDN: \<video\>](https://developer.mozilla.org/ja/docs/Web/HTML/Element/video)
- [MDN: レスポンシブ画像](https://developer.mozilla.org/ja/docs/Learn_web_development/Core/Structuring_content/Responsive_images)
