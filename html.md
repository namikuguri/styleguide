# HTML Styleguide
文書構造に関する HTML の決まり事。

## 目次
1. [メタルール](#meta-rule)
    1. [エンコード](#meta-rule-encode)
    2. [コメント](#meta-rule-comment)
    3. [TODO コメント](#meta-rule-comment-todo)
2. [書式ルール](#format-rule)
    1. [一般的な書式](#format-rule-general)
    2. [インデントや改行箇所](#format-rule-indent)
    3. [大文字/小文字](#format-rule-charactor)
3. [コーディングルール](#coding-rule)
    1. [ドキュメントタイプ](#coding-rule-doctype)
    2. [基本的な構造](#coding-rule-base-structure)
    3. [ルート要素](#coding-rule-root-element)
    4. [外部リソースを読み込む際の type 属性](#coding-rule-type-attribute)
    5. [role 属性](#coding-rule-role-attribute)
    6. [セマンティックに書く](#coding-rule-semantic)
    7. [インラインスタイル](#coding-rule-inline-styling)
    8. [HTML 要素によるスタイリング](#coding-rule-element-styling)
    9. [マルチメディアの代替コンテンツ](#coding-rule-alternate-content)
    10. [タグの省略をしない](#coding-rule-omission-of-tag)
    11. [フォームの cols , rows 属性](#coding-rule-form)
    12. [アウトライン](#coding-rule-outline)
    13. [HTML のバリデート](#coding-rule-validation)
4. [[ オプション ] プリプロセッサ](#use-preprocessor)
5. [参考文献](#reference)

<a name="meta-rule"></a>
## 1. メタルール

<a name="meta-rule-encode"></a>
### エンコード
UTF-8 を使う。

```html
<meta charset="utf-8">
```

<a name="meta-rule-comment"></a>
### コメント
`<!-- start / { name } -->` でコメント開始箇所、 `<!-- end / { name } -->` で終了箇所を書く。コメントを書く場合は必ず両方書こうね。  
コメントの下はインデントをいれる必要はないよ。

```html
<!-- start / header -->
<header>
  ...
</header>
<!-- end / header -->
```

他でコンポーネント化されているものなど、HTML だけではわかりにくいものにはコメントを書こう。必ず書けというわけではないよ。

```html
<!-- start / header -->
{{include file="header.tpl"}}
<!-- end / header -->

<!-- start / estimate form -->
<%= form_for(@estimate, :html => {:class => 'basic-form', :multipart => true}) do |f| %>
  ...
<% end / %>
<!-- end / estimate form -->
```

<a name="meta-rule-comment-todo"></a>
### TODO コメント
こんな感じ:

```html
<!-- TODO: remove -->
```

<a name="format-rule"></a>
## 2. 書式ルール

<a name="format-rule-general"></a>
### 一般的な書式
- インデントは半角スペース2つで行います
- シングルクォーテーション ( `'` ) ではなくダブルクォーテーション ( `"` ) を使います

<a name="format-rule-indent"></a>
### インデントや改行箇所
ブロック要素・リスト要素・テーブル要素は改行してから記述し、これらの子要素にはインデントを入れる。

```html
<div class="module">
  <p>paragraph</p>
</div>

<ul>
  <li>list item</li>
  <li>list item</li>
</ul>

<table>
  <tr>
    <th>table header</th>
    <td>table data</td>
  </tr>
</table>
```

インライン要素や `<br>` タグでは改行を挟まない。

```html
<!-- NG -->
<p>てきすとてきすと
  <a href="">リンク</a>
  <br>
  てきすとてきすと</p>

<!-- OK -->
<p>てきすとてきすと<a href="">リンク</a>てきすとてきすと</p>
```

<a name="format-rule-charactor"></a>
### 大文字/小文字
HTML の要素、ID やクラス名は小文字のみで行おう。  
コメントには大文字を使ってもいいよ。

```html
/* NG */
<div class="LAYOUT"> ... </div>
<DIV CLASS="module"> ... </DIV>

/* OK */
<div class="layout"> ... </div>
<div class="module"> ... </div>

<!-- start / RSS Feed -->
<div class="rss-feed"> ... </div>
<!-- end / RSS Feed -->
```

<a name="coding-rule"></a>
## 3. コーディングルール

<a name="coding-rule-doctype"></a>
### ドキュメントタイプ
HTML5 でいこう。

```html
<!DOCTYPE html>
```

<a name="coding-rule-base-structure"></a>
### 基本的な構造
`html` 以下の `head` , `body` にもインデントを取ろう。  
`main` 要素さん、こんにちは。

```html
<!DOCTYPE html>
<html lang="ja">
 <head>
   <title> ... </title>
 </head>
 <body>
   <!-- start / header -->
   <header>
     ...
   </header>
   <!-- end / header -->
   
   <!-- start / main -->
   <main role="main">
     ...
   </main>
   <!-- end / main -->
   
   <!-- start / footer -->
   <footer>
     ...
   </footer>
   <!-- end / footer -->

   <!-- start / scripts -->
   <div class="scripts">
     ...
   </div>
   <!-- end / scripts -->

   <!-- start / analysis-code -->
   <div class="analysis-code">
     ...
   </div>
   <!-- end / analysis-code -->
 </body>
</html>
```

<a name="coding-rule-root-element"></a>
### ルート要素
HTML ページではルート要素は `<html>` だよね。
このルート要素には言語コードを指定しておこう。

日本語の指定だとこうだ:

```html
<html lang="ja">
  ...
</html>
```

<a name="coding-rule-type-attribute"></a>
### 外部リソースを読み込む際の type 属性
CSS と JavaScript の `type` 属性は省略する。HTML5 ではデフォルトの言語として解釈されるからね。

```html
<!-- NG -->
<link rel="stylesheet" href="stylesheets/base/base.css" type="text/css">
<script src="javascripts/jquery.min.js" type="text/javascript"></script>

<!-- OK -->
<link rel="stylesheet" href="stylesheets/base/base.css">
<script src="javascripts/jquery.min.js"></script>
```

<a name="coding-rule-role-attribute"></a>
### role 属性
HTML5 のセマンティクスを補うために `role` 属性を使ってそれぞれに役割を明確にしよう。

特に `main` 要素を使う場合は、ユーザーエージェントが要件とされる role マッピングを実装するまで `role="main"` を指定しよう。

```html
<main role="main">
  ...
</main>
```

<a name="coding-rule-semantic"></a>
### セマンティックに書く
見出しは `<h1>` ~ `<h6>` 要素、段落なら `<p>` 要素、順序付きリストなら `<ol>` 要素、コンテンツの意味に適した要素を使うようにしよう。

また、 `<dl>` で使う `<dt>` と `<dd>` のように要素同士が関係を持っているものがあるけど、これらの関係性を見えにくくするような HTML を組んではいけないよ。（バリデーションをかけたらすぐにエラーが返ってくると思うけど）

```html
<!-- NG -->
<dl>
  <dt>Definition Term</dt>
  <span class="separation"></span>
  <dd>Definition Description</dd>
</dl>

<!-- OK -->
<dl>
  <dt>Definition Term</dt>
  <dd>Definition Description</dd>
</dl>
```

`div` や `span` を使う前に他に適した要素が本当に無いのか、以下のサイトなどで一度確認してみて。HTML5 になってから意味付けをする要素も増えたしね。

- [HTML5](http://www.w3.org/html/wg/drafts/html/CR/)
- [HTML5 タグリファレンス](http://reference.hyper-text.org/html5/)
- [HTML5.jp](http://html5.jp/)

<a name="coding-rule-inline-styling"></a>
### インラインスタイル
要素に当てる `style` 属性は使ってはいけない。
理由はスタイルの適用箇所が CSS ファイルと HTML ファイルにあったらどちらにあるか分かり難くなるから.. とか、まぁいろいろね:

```html
<!-- NG -->
<p style="color: red">赤い文字</p>
```

<a name="coding-rule-element-styling"></a>
### HTML 要素によるスタイリング
スタイリング目的で要素を決めるのはもういい加減やめよう。

`<center>` といった書式方向を決める要素や、`<font>` といった見た目を変更するだけの要素は使ってはいけない。HTML5 では廃止予定になっていることが 1番の理由だけど、そもそも見た目を変更するために要素を選択するのは良くないからね。

それと `<br>` タグもスタイリング目的で使ってはいけないよ。以下のような使い方はよくないね。

- 連続した `<br>`
- スタイルを整えるための `<br>`

<a name="coding-rule-alternate-content"></a>
### マルチメディアの代替コンテンツ
画像が表示されない場合、音声で読み上げられる場合を考えて `<img>` には `alt` 属性を指定しておこう。  
`alt` に画像内の文章をすべて書けというわけではないけれど、「何の画像か？」というのが分かる程度には書こう。  
写真やイラストだけの画像に `alt` をつける必要はないけどね。

```html
<!-- NG -->
<img src="figure-tax-increase.png" alt="">

<!-- OK -->
<img src="figure-tax-increase.png" alt="2015年10月に消費税率を10%に引き上げる政府の大増税計画の推移">
<img src="picture-mainview.png" alt="">
```

<a name="coding-rule-omission-of-tag"></a>
### タグの省略をしない
`li`, `dt`, `dd`, `p`, `tr`, `th`, `td`, `rt`, `rp`, `optgroup`, `option`, `thread`, `tfoot` で終了タグの省略は行わない。

<a name="coding-rule-form"></a>
### フォームの cols , rows 属性
`input` 要素、 `textarea` 要素の幅・高さの指定を `cols` 属性や `rows` 属性では行わない。それぞれにクラスを振って `width` や `hight` プロパティの指定で行おう。

```html
<!-- NG -->
<input type="text" colos="50" rows="10">
<textarea id="" name="" cols="30" rows="10"></textarea>

<!-- OK -->
<input type="text" class="input-kana">
<textarea id="" name="" class="textarea-note"></textarea>
```

<a name="coding-rule-outline"></a>
### アウトライン
アウトラインを綺麗に保って機械（検索エンジン）にページを正しく解釈してもらおう。  
そのためにはアウトライン形成に関係する `section` 要素や `h1` ~ `h6` 要素などを理解して適切に使うことが必要だね。  
また、こういった要素には見た目に関する強いプロパティ（ 余白や色 ）を割り当ててしまうと "見た目上の問題" からアウトラインが崩れてしまうことがあるので気をつけよう。

「完璧！」と思っても上手くできていないことがあるよね。大枠のアウトラインができた時とコーディングの最後は必ずツールを使ってアウトラインを確認しよう。

- [HTML5 Outliner](http://gsnedders.html5.org/outliner/)
- [HTML5 Outliner ( Chrome  extension )](https://chrome.google.com/webstore/detail/html5-outliner/afoibpobokebhgfnknfndkgemglggomo)
- [HTML5 Outliner ( Firefox add-on )](https://addons.mozilla.org/en-US/firefox/addon/html5_outliner/)

<a name="coding-rule-validation"></a>
### HTML のバリデート
すべてが終わった時ではなくて、一部が完成したタイミング、もしくはあなたが書いているコードを常に監視して HTML コードの検証を行おう。コードが書き終わってから「Result: 27 Errors, 25 warning(s)」とか出るのが恐いからね。

Web での検証ツールは以下のものを使おう。

- [Markup Validation Service](http://validator.w3.org/)

Error は基本的に 0 に、warnings は.. まぁできるだけ減そう。

<a name="use-preprocessor"></a>
## 4. [ オプション ] プリプロセッサ
Slim を使うよ。  
面倒な山カッコ（ `<` , `>` ）を書かなくて済むからね。

- [Slim](http://slim-lang.com/)

<a name="reference"></a>
## 5. 参考文献
- [HTML Style Rules](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml#HTML_Style_Rules)
- [HTML Formatting Rules](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml#HTML_Formatting_Rules)
- [「Google HTML/CSS Style Guide」を適当に和訳してみた](http://re-dzine.net/2012/05/google-htmlcss-style-guide/)
- [Markup & Templates Styleguide](https://github.com/styleguide/templates)
- [GitHubのHTML/CSS Styleguideを適当に和訳してみた](http://re-dzine.net/2012/09/github-htmlcss-styleguide/)
- [結局どうすればいいの？](http://hail2u.net/documents/diveintohtml5-semantics.html)
- [HTML5 ドキュメントのセクションとアウトライン](https://developer.mozilla.org/ja/docs/Web/HTML/Sections_and_Outlines_of_an_HTML5_document)
- [HTMLのアウトライン意識してますか？ - QiitaのSEO事情（前編）](http://qiita.com/yuku_t/items/726a67d8ae74eea2540a)
- [role属性を実装しよう](https://w3g.jp/blog/studies/lets_role_fit)
- [HTMLに提案中のmain要素](http://myakura.hatenablog.com/entry/2012/12/01/025158)
