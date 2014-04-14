# CSS Styleguide
見た目に関する CSS の決まり事。

## 目次
1. [メタルール](#meta-rule)
    1. [エンコード](#meta-rule-encode)
    2. [コメント](#meta-rule-comment)
    3. [TODO コメント](#meta-rule-comment-todo)
2. [書式ルール](#format-rule)
    1. [一般的な書式](#format-rule-general)
    2. [階層にインデントをつけない](#format-rule-indent)
    3. [大文字/小文字](#format-rule-charactor)
    4. [「0」のときの単位の省略](#format-rule-omission-of-unit)
    5. [小数点の頭の「0」の省略](#format-rule-omission-of-decimal-point)
    6. [URI 値の引用符の省略](#format-rule-quotation-of-uri)
3. [コーディングルール](#coding-rule)
    1. [リセット CSS は使わない](#coding-rule-unuse-reset-css)
    2. [ディレクトリ構成](#coding-rule-directory-structure)
    3. [プロパティの列挙順](#coding-rule-property-order)
    4. [ベンダープレフィックス](#coding-rule-vendor-prefix)
    5. [カラーコード](#coding-rule-color-code)
    6. [カラーコードの短縮](#coding-rule-color-code-shortening)
    7. [px か em か](#coding-rule-px-vs-em)
    8. [セレクタ](#coding-rule-selector)
    9. [@import での読み込みはダメ](#coding-rule-import-loading)
    10. [ショートハンドプロパティ](#coding-rule-shorthand)
    11. [CSS ハック](#coding-rule-css-hack)
    12. [余計なモジュールの構造化は避ける](#coding-rule-appropriate-structuring)
    13. [CSS のバリデート](#coding-rule-validation)
4. [スタイルのプレビュー](#style-preview)
5. [[ オプション ] プリプロセッサ](#use-preprocessor)
6. [参考文献](#reference)

<a name="meta-rule"></a>
## 1. メタルール

<a name="meta-rule-encode"></a>
### エンコード
UTF-8 を使う。

```css
@charset "utf-8";
```

<a name="meta-rule-comment"></a>
### コメント
普通のコメントは普通に、 `/* */` 形式で書こう。  
`/* start - { name } */` でコメント開始箇所、 `/* end - { name } */` で終了箇所を書く。コメントを書く場合は必ず両方書こうね。

```css
/* start - layout */
.header {
  ...
}

.main {
  ...
}

.footer {
  ...
}
/* end - layout */

/* start - module */
.module {
  ...
}

.module-bordered {
  ...
}

.module-full-width {
  ...
}
/* end - module */
```

コメントはできるだけ一行で収まるように、コメントを入れ過ぎないようにしよう（コメントがないとモジュールの意味がわからないとかはモジュールの作り自体がよくない）。

<a name="meta-rule-comment-todo"></a>
### TODO: コメント
こんな感じ:

```css
.module {
  backround-image: url(//lorempixel.com/200/200/); /* TODO: change dummy image */
}
```

<a name="format-rule"></a>
## 2. 書式ルール

<a name="format-rule-general"></a>
### 一般的な書式
- プロパティの前には半角スペース2つでインデント
- シングルクォーテーション ( `'` ) ではなくダブルクォーテーション ( `"` ) を使います
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

<a name="format-rule-indent"></a>
### 階層にインデントをつけない
CSS では階層に対してのインデントをしない。  
セレクタの指定で十分わかると思うからね。

```css
/* NG */
.list {
  ...
}

  .list li {
    ...
  }

    .list li .list-note {
      ...
    }

/* OK */
.list {
  ...
}

.list li {
  ...
}

.list li .list-note {
  ...
}
```

<a name="format-rule-charactor"></a>
### 大文字/小文字
CSS のプロパティ、ID やクラス名は小文字のみで行おう。  
コメントには大文字を使ってもいいよ。

```html
/* NG */
.LAYOUT {
  background-color: #fff;
}

.module {
  MARGIN: 0 AUTO;
}

/* OK */
.layout {
  background-color: #fff;
}

.module {
  margin: 0 auto;
}
/* end - Module */

/* start - RSS Feed */
.rss-feed {
  margin: 0 auto;
}
/* end - RSS Feed */
```

<a name="format-rule-omission-of-unit"></a>
### 「0」のときの単位の省略
「0」のときは単位を省略して書こう:

```css
/* OK */
.format {
  margin: 0;
  padding: 0;
}
```

<a name="format-rule-omission-of-decimal-point"></a>
### 小数点の頭の「0」の省略
小数点の頭の「0」は省略して書こう:

```css
/* OK */
.format {
  margin: .5em;
  text-shadow: 0 1px 0 rgba(0,0,0,.4);
}
```

<a name="format-rule-quotation-of-uri"></a>
### URI 値の引用符の省略
URI 値の引用符は省略して書こう:

```css
/* NG */
.format {
  background-image: url("//lorempixel.com/200/200/");
}

/* OK */
.format {
  background-image: url(//lorempixel.com/200/200/);
}
```

<a name="coding-rule"></a>
## 3. コーディングルール

<a name="coding-rule-unuse-reset-css"></a>
### リセット CSS は使わない
必要以上にスタイルシートを上書きしてしまう。そして、それがどこに、どのように上書きされたか把握しにくい。リセット CSS は使わないことにしておこう。

その代わりに以下の手段を使ってブラウザのスタイルシートに上書きする:

- ブラウザ間の誤差をなくして補正する [necolas/normalize.css](https://github.com/necolas/normalize.css/) を使う ( Sass を使ってる環境では [hail2u/normalize.scss](https://github.com/hail2u/normalize.scss) )
- 自分で user agent stylesheets に上書きするスタイルを書く

あと、自分で書くときは user agent stylesheets に上書きするようなスタイル**のみ**書くように心がけよう。

```css
/* NG */
p {
  margin: 0;
}

/* OK */
p {
  margin-top: 0;
  margin-bottom: 0;
}
```

<a name="coding-rule-directory-structure"></a>
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

<a name="coding-rule-property-order"></a>
### プロパティの列挙順
このようなグループで分けて書こう:

1. ボックス（表示とポジション）
2. ボーダー
3. バックグラウンド
4. テキスト
5. その他

ボックスには `margin` や `position` の指定、ボーダーには `border` 、バックグラウンドには `background` 、テキストには `font` や `color` や `lin-height` や `text-align` 、その他には `clear` や `cursor` の指定を書く。グループ内でのプロパティの列挙順はできるだけ統一するように（できるだけ合わせる. レベルでいいけど）。  

プロジェクトごとにプロパティの列挙順一覧を作成しておこう。

<a name="coding-rule-vendor-prefix"></a>
### ベンダープレフィックス
以下の順序で書こう:

1. -webkit-
2. -moz-
3. -ms-
4. -o-
5. none

ブラウザのアップデートにより、ベンダープレフィックスのサポートが不要になったものは順次消していこう。

<a name="coding-rule-color-code"></a>
### カラーコード
透過以外は HEX 形式で、透過が伴うものは RGBA 形式で指定する。  

```css
.module {
  color: #000;
  background-color: #fff;
  text-shadow: 0 1px 0 rgba(0,0,0,.4);
}
```

これは余計な話かもしれないけど、IE8 以下の対応を考えてるなら CSS3 から追加された RGBA, HSLA 形式は使わないほうがいい。サポートされてないからね。  
Sass なんかを使ってる場合はコンパイル時に HEX 形式に変換するといいよ。

<a name="coding-rule-color-code-shortening"></a>
### カラーコードの短縮
カラーコードが 3文字で短縮して表記できるものは 3文字で指定しよう。
`#XXYYZZ` ( 例: `#2200aa` ) 形式のものは短縮して表記できるよ。

```css
/* NG */
.module {
  color: #110011;
  background-color: #eeeeee;
}

/* OK */
.module {
  color: #101;
  background-color: #eee;
}
```

一応 Web にあったリストのリンクも載せておくね。

- [#RGB スタイルシート専用 3桁カラーコード](http://www.ne.jp/asahi/mitoro/page/color_code.htm)

<a name="coding-rule-px-vs-em"></a>
### px か em か
本当は `em` 使ったほうがいいかもしれないけど、今はまだ `px` 使おう。  
僕にはまだ `em` を使ってちゃんとプロダクトを組み上げる自身がないんだ。

`rem` という手段も検討してみよう。

<a name="coding-rule-selector"></a>
### セレクタ
ユニバーサルセレクタ ( `*` ) は使ってはいけない。適用範囲が把握しにくいことや全てを走査して適用していくのでパフォーマンスが落ちるから。

```css
/* NG */
* {
  margin: 0;
  padding: 0;
}
```

最優先セレクタ ( `!important` )は使ってはいけない。強制的に優先度を決めると他のものとの優先度の比較が難しくなるから。

```css
/* NG */
.message {
  margin-bottom: 20px !important;
}
```

タイプセレクタは使ってはいけない。パフォーマンスの低下につながるし、不要に要素とクラスの結びつきを強めるから。

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

<a name="coding-rule-import-loading"></a>
### @import での読み込みはダメ
CSS の `@import` は使用してはいけない。ブラウザのパラレルロード（並行してコンテンツを読み込む仕組み）を無視して順番にファイルを読み込むため、パフォーマンスの低下につながるから。

```css
/* NG */
@import url('list.css');  
@import url('button.css');
```

<a name="coding-rule-shorthand"></a>
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

<a name="coding-rule"></a>
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

<a name="coding-rule-css-hack"></a>
### CSS ハック
使ってはいけない。

<a name="coding-rule-appropriate-structuring"></a>
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

<a name="coding-rule-validation"></a>
### CSS のバリデート
すべてが終わった時ではなくて、一部が完成したタイミング、もしくはあなたが書いているコードを常に監視して CSS コードの検証を行おう。コードが書き終わってから「found 27 errors and 217 warnings.」とか出るのが恐いからね。

Web での検証ツールは以下のものを使おう。

- [CSS LINT](http://csslint.net/)

Error は基本的に 0 に、warnings は.. まぁできるだけ減そう。

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
Sass(SCSS) を使うよ。  
`Mixin` や `Partial` といった便利な機能があるからね。

- [Sass](http://sass-lang.com/)

<a name="reference"></a>
## 6. 参考文献
- [CSS Style Rules](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml#CSS_Style_Rules)
- [CSS Formatting Rules](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml#CSS_Formatting_Rules)
- [CSS Meta Rules](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml#CSS_Meta_Rules)
- [「Google HTML/CSS Style Guide」を適当に和訳してみた](http://re-dzine.net/2012/05/google-htmlcss-style-guide/)
- [CSS Styleguide](https://github.com/styleguide/css)
- [GitHubのHTML/CSS Styleguideを適当に和訳してみた](http://re-dzine.net/2012/09/github-htmlcss-styleguide/)
