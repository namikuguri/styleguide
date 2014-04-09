# CSS Styleguide
見た目に関する CSS の決まり事。

## 目次
1. [メタルール](#meta-rule)
    1. エンコード
    2. コメント
    3. TODO コメント
2. [書式ルール](#format-rule)
    1. 一般的な書式
    2. 大文字/小文字
    3. 「0」のときの単位の省略
    4. 小数点の頭の「0」の省略
    5. URI 値の引用符の省略
3. [コーディングルール](#coding-rule)
    1. ディレクトリ構成
    2. プロパティの列挙順
    3. ベンダープレフィックス
    4. カラーコード
    5. px か em か
    6. セレクタ
    7. ショートハンドプロパティ
    8. CSS ハック
    9. 余計なモジュールの構造化は避ける
    10. CSS のバリデート
4. [スタイルのプレビュー](#style-preview)
5. [[ オプション ] プリプロセッサ](#use-preprocessor)
6. [参考文献](#reference)

<a name="meta-rule"></a>
## 1. メタルール
### エンコード
UTF-8 を使う。

```css
@charset "utf-8";
```

### コメント
普通のコメントは普通に、 `/* */` 形式で書こう。  
`/* start - { name } */` でコメント開始箇所、 `/* end - { name } */` で終了箇所を書く。コメントを書く場合は必ず両方書こうね。

```css
/* start - layout */
.layout {
  ...
}
/* end - layout */

/* start - module */
.module {
  ...
}
/* end - module */
```

コメントはできるだけ一行で収まるように、コメントを入れ過ぎないようにしよう（コメントがないとモジュールの意味がわからないとかはモジュールの作り自体がよくない）。

### TODO: コメント
こんな感じ:

```css
.module {
  backround-image: url(//lorempixel.com/200/200/); /* TODO: change dummy image */
}
```

<a name="format-rule"></a>
## 2. 書式ルール
### 一般的な書式
- プロパティの前にはスペース2つでインデント
- `:` の前にはスペースを1つ
- `{` の前にはスペースを1つ
- `{` の後は改行
- セレクタ内最後のプロパティの後は改行
- `}` の後は改行し、 1行空ける

これら満たした CSS の構文:

```css
/* General Format */
.module {
  display: block;
  background-color: #fff;
}

.module-bordered {
  border: 1px solid #ccc;
}
```

## 大文字/小文字
CSS のプロパティ、ID やクラス名は小文字のみで行おう。  
コメントには大文字を使ってもいいけど、使うなら頭文字だけ大文字にするとか、とにかく一貫させて使うことが大事。

```html
/* NG */
/* start - Layout */
.LAYOUT {
  background-color: #fff;
}
/* end - Layout */

/* start - module */
.module {
  MARGIN: 0 AUTO;
}
/* end - module */

/* OK */
/* start - Layout */
.layout {
  background-color: #fff;
}
/* end - Layout */

/* start - Module */
.module {
  margin: 0 auto;
}
/* end - Module */
```

### 「0」のときの単位の省略
「0」のときは単位を省略して書こう:

```css
/* OK */
.format {
  margin: 0;
  padding: 0;
}
```

### 小数点の頭の「0」の省略
小数点の頭の「0」は省略して書こう:

```css
/* OK */
.format {
  margin: .5em;
  text-shadow: 0 1px 0 rgba(0,0,0,.4);
}
```

### URI 値の引用符の省略
URI 値の引用符は省略していいよ:

```css
/* OK */
.format {
  background-image: url(...);
}
```

<a name="coding-rule"></a>
## 3. コーディングルール
### ディレクトリ構成
SMACSS カテゴリーで分けてつくろう。

このようにディレクトリを分けるよ:

- ベース
- レイアウト
- モジュール
- ステート（状態）
- テーマ

ディレクトリ構成の例:

```sh
stylesheets/
 |
 |-- base/
 | |
 | |__ base.css
 |
 |-- layout/
 | |
 | |-- laytout.css
 | |
 | |__ grid.css
 |
 |-- module/
 | |
 | |-- button.css
 | |
 | |-- form.css
 | |
 | |__ table.css
 |
 |-- state/
 | |
 | |__ state.css
 |
 |__ theme/
   |
   |-- valentine.css
   |
   |__ xmas.css
```

Sass で Partial ファイルを取り扱う場合はカテゴリーディレクトリと同じ階層に置こう。

```sh
stylesheets/
 |
 |-- .../
 |
 |-- theme/
 |
 |__ partial/
   |
   |__ colors.css
```

SMACSS について詳細が知りたい場合は本が出てるからそれ見て。「100ページ読むのはだりぃ〜 」って気持ちのときは.. 自分で書いた本の要約でも見て。

- [SMACSS 読んだ](http://chroma.hatenablog.com/entry/2013/07/22/120818)

### プロパティの列挙順
このようなグループで分けて書こう:

1. ボックス（表示とポジション）
2. ボーダー
3. バックグラウンド
4. テキスト
5. その他

ボックスには `margin` や `position` の指定、ボーダーには `border` 、バックグラウンドには `background` 、テキストには `font` や `color` や `lin-height` や `text-align` 、その他には `clear` や `cursor` の指定を書く。グループ内でのプロパティの列挙順はできるだけ統一するように（できるだけ合わせる. レベルでいいけど）。  

プロジェクトごとにプロパティの列挙順一覧を作成しておこう。

### ベンダープレフィックス
以下の順序で書こう:

1. -webkit-
2. -moz-
3. -ms-
4. -o-
5. none

ブラウザのアップデートにより、ベンダープレフィックスのサポートが不要になったものは順次消していこう。

### カラーコード
透過以外は HEX 形式で、透過が伴うものはは RGBA 形式で指定する。  
カラーコードが3文字で表記できるものは 3文字で指定しよう。

```
/* NG */
.module {
  color: #000000;
  background-color: #ffffff;
}

/* OK */
.module {
  color: #000;
  background-color: #fff;
  text-shadow: 0 1px 0 rgba(0,0,0,.4);
}
```

これは備考だけど、IE8 以下の対応を考えてるなら CSS3 から追加された RGBA, HSLA 形式は使わないほうがいい。サポートされてないからね。  
Sass なんかを使ってる場合はコンパイル時に HEX 形式に変換するといいよ。

### px か em か
本当は `em` 使ったほうがいいかもしれないけど、今はまだ `px` 使おう。  
僕にはまだ `em` を使ってちゃんとプロダクトを組み上げる自身がないんだ。

`rem` という手段も検討してみよう。

### セレクタ
ユニバーサルセレクタ ( `*` ) は使用してはいけない。適用範囲が把握しにくいことや全てを走査して適用していくのでパフォーマンスが落ちるからね:

```css
/* NG */
* {
  margin: 0;
  padding: 0;
}
```

最優先セレクタ ( `!important` )は使用してはいけない。強制的に優先度を決めると他のものとの優先度の比較が難しくなるからね:

```css
/* NG */
.message {
  margin-bottom: 20px !important;
}
```

タイプセレクタは使用してはいけない。パフォーマンスの低下につながるから:

```css
/* NG */
p.message {
  margin-bottom: 20px;
}

/* OK */
.message {
  margin-bottom: 20px;
}
```

### ショートハンドプロパティ
あまり使わないようにしよう。指定が読み取りにくいことや余計な打ち消しをすることがあるからね。  
例外は `margin` や `padding` などで複数箇所の指定をするとき、`border` の指定をするときくらいかな。

```css
/* NG */
.body {
  margin: 0 20px 0 0;
  padding: 0 0 20px;
  background: red url(...) repeat-x 0 0;
  font: italic lighter 14px/1.4 Georgia, serif;
}

/* OK */
.body {
  margin-right: 20px;
  padding-bottom: 20px;
  background-color: red;
  background-image: url(...);
  background-repeat: repeat-x;
  background-position: 0 0;
  font-familiy: Georgia, serif;
  font-style: italic;
  font-weight: bold;
  font-size: 14px;
  line-height: 1.4;
}

/* Exception */
.module-bordered {
  margin: 0 auto;
  padding: 20px 0;
  border: 1px solid #ccc;
}
```

### ネストの上限
ネストは3階層以下に収めるようにする。

```css
/* OK: 最大深度 */
.outer {
  background-color: red;
}

.outer .inner {
  position: relative;
  margin: 0 auto;
  width: 300px;
}

.outer .inner:before {
  content: "ribbon";
  position: absolute;
  top: 10px;
  left: -10px;
}

.outer .inner .box-left {
  float: left;
  width: 100px;
}

.outer .inner .box-right {
  float: right;
  width: 100px;
}
```

### CSS ハック
使ってはいけない。

### 余計なモジュールの構造化は避ける
余計なモジュール化は避けよう。
親要素に子要素が紐付いているリストやテーブルには、子要素に対してモジュール構造を持たせる必要はない。

```html
<!-- NG -->
<style>
.list {
  ...
}

.list-item {
  ...
}
</style>

<ul class="list">
  <li class="list-item"> ... </li>
  <li class="list-item"> ... </li>
  <li class="list-item"> ... </li>
</ul>

<style>
.table {
  ...
}

.table-row {
  ...
}

.table-header {
  ...
}

.table-data {
  ...
}
</style>

<table class="table">
  <tr class="table-row">
    <th class="table-header"> ... </th>
    <td class="table-data"> ... </td>
  </tr>
</table>

<!-- OK -->
<style>
.list {
  ...
}

.list li {
  ...
}
</style>

<ul class="list">
  <li> ... </li>
  <li> ... </li>
  <li> ... </li>
</ul>

<style>
.table {
  ...
}

.table tr {
  ...
}

.table th {
  ...
}

.table td {
  ...
}
</style>

<table class="table">
  <tr>
    <th> ... </th>
    <td> ... </td>
  </tr>
</table>
```

### CSS のバリデート
すべてが終わった時ではなくて、一部が完成したタイミング、もしくはあなたが書いているコードを常に監視して CSS コードの検証を行おう。コードが書き終わってから「found 27 errors and 217 warnings.」とか出るのが恐いからね。

Web での検証ツールは以下のものを使おう。

- [CSS LINT](http://csslint.net/)

Error は基本的に 0 に、warnings は.. まぁできるだけ減そう。

- [Sass](http://sass-lang.com/)

<a name="style-preview"></a>
## 4. スタイルのプレビュー
StyleDocco ( node 環境 ) か KSS ( rails 環境 ) 、または Kalei ( node, rails が入っていない環境 ) を使おう。  
これらを使うことでこんなメリットがある。

- ID やクラスに振られるスタイルのプレビュー
- ファイル内に含めるモジュールの定義 ( ファイルの先頭に記載 )

SCSS で書いてて、スタイルのプレビューに StyleDocco を使ってる場合はこんなふうに書くよ。  
（ SCSS では `// ` 形式のコメントはコンパイル後の CSS ファイルに書き出されない）

テンプレート:

```scss
// # { ファイル名 }
// { モジュールに関する注意事項、このファイルで取り扱うモジュールの役割など }

...

// # { モジュール名 }
// ```
// { スタイルが割り当てられる HTML コード }
// ```

.module {
}
```

実際の例:

```scss
// # Base
// ここではできるだけ User Agent Style に上書きするようなスタイルのみ書くように心がけましょう

...

// # Heading
// ```
// <h1>Heading Level 1</h1>
// <h2>Heading Level 2</h2>
// <h3>Heading Level 3</h3>
// <h4>Heading Level 4</h4>
// ```

h1 {
  font-size: 24px;
  line-height: 1.35;
}

h2 {
  font-size: 18px;
  line-height: 1.35;
}

h3 {
  font-size: 16px;
  line-height: 1.35;
}

h4 {
  font-size: 14px;
  line-height: 1.35;
}
```

<a name="use-preprocessor"></a>
## 5. [ オプション ] プリプロセッサ
これはやらなくてもいいけど、やったほうがいいこと。

Sass(SCSS) を使うよ。  
`Mixin` や `Partial` といった便利な機能があるからね。

<a name="reference"></a>
## 6. 参考文献
- [CSS Style Rules](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml#CSS_Style_Rules)
- [CSS Formatting Rules](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml#CSS_Formatting_Rules)
- [CSS Meta Rules](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml#CSS_Meta_Rules)
- [「Google HTML/CSS Style Guide」を適当に和訳してみた](http://re-dzine.net/2012/05/google-htmlcss-style-guide/)
- [CSS Styleguide](https://github.com/styleguide/css)
- [GitHubのHTML/CSS Styleguideを適当に和訳してみた](http://re-dzine.net/2012/09/github-htmlcss-styleguide/)
