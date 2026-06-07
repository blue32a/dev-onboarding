# テーブル

## このステップのゴール

- データをテーブルで表現できます
- ヘッダーと本体を構造化して、関連するデータをわかりやすく整理できます

## 前提知識・環境

- 07-media を完了していること

## 実践

`index.html` にコードを書きながら進めます。変更はLive Serverで確認します。

### 1. テーブルの基本構造を作る

`table`・`tr`・`td` でシンプルなテーブルを作ります。

```html
<table>
  <tr>
    <td>Alice</td>
    <td>エンジニア</td>
    <td>東京</td>
  </tr>
  <tr>
    <td>Bob</td>
    <td>デザイナー</td>
    <td>大阪</td>
  </tr>
</table>
```

表示はできますが、どの列が何を示しているかわかりません。

### 2. ヘッダーと本体を分ける

`thead`・`tbody`・`th` を追加して構造を明確にします。

```html
<table>
  <caption>メンバー一覧</caption>
  <thead>
    <tr>
      <th scope="col">名前</th>
      <th scope="col">役職</th>
      <th scope="col">勤務地</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>エンジニア</td>
      <td>東京</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td>デザイナー</td>
      <td>大阪</td>
    </tr>
  </tbody>
</table>
```

| 要素・属性 | 役割 |
| --- | --- |
| `caption` | テーブルのタイトル |
| `thead` | ヘッダー行をまとめる |
| `tbody` | データ行をまとめる |
| `th` | ヘッダーセル。`td` より強調して表示される |
| `scope="col"` | このヘッダーが列のヘッダーであることをスクリーンリーダーに伝える |

### 3. セルを結合する

`colspan`（横方向）・`rowspan`（縦方向）でセルを結合できます。

```html
<table>
  <caption>連絡先一覧</caption>
  <thead>
    <tr>
      <th scope="col" rowspan="2">名前</th>
      <th scope="col" colspan="2">連絡先</th>
    </tr>
    <tr>
      <th scope="col">メール</th>
      <th scope="col">電話</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>alice@example.com</td>
      <td>090-1111-2222</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td>bob@example.com</td>
      <td>090-3333-4444</td>
    </tr>
  </tbody>
</table>
```

## まとめ

- `table > thead + tbody` の構造でテーブルをヘッダーと本体に分ける
- `th` はヘッダーセル。`scope` 属性でヘッダーの対応方向（`col`/`row`）を指定する
- `caption` でテーブルのタイトルを付ける
- `colspan`・`rowspan` でセルを結合できる

**次のステップ:** [09 アクセシビリティ](../09-accessibility/README.md) では、すべてのユーザーが使えるHTMLの書き方を学びます。

## 一次情報・参考資料

- [MDN: \<table\>](https://developer.mozilla.org/ja/docs/Web/HTML/Element/table)
- [MDN: HTMLテーブルの高度な機能とアクセシビリティ](https://developer.mozilla.org/ja/docs/Learn_web_development/Core/Structuring_content/Table_accessibility)
