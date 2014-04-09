# Front-end Styleguide
HTML と CSS 、Javascript に共通する決まり事。

## 目次
1. [無駄なスペースは削除](#delete-space)
2. [URI 値のプロトコルの省略](#omission-of-protocol)
3. [ID かクラスか](#id-vs-class)
4. [ID やクラスの命名](#naming)
    1. 意味のわかる名前をつける
    2. ID とクラスの命名スタイル
    3. 単語の省略
5. [[ オプション ] Grunt 、タスクの簡略化](#simplification-of-task)
6. [参考文献](#reference)

<a name="delete-space"></a>
## 1. 無駄なスペースは削除
行末など残ったスペースは削除しておこう。

（ `_` をスペースとみたてて）:

```css
/* NG */
.module {
  color: red;_
}
```

<a name="omission-of-protocol"></a>
## 2. URI 値のプロトコルの省略
URI 値のプロトコル ( http:, https: )は省略する。

HTML の場合:

```html
/* NG */
<img src="http://www.google.com/" alt="">

/* OK */
<img src="//www.google.com/" alt="">
```

CSS の場合:

```css
/* NG */
.format {
  background-image: url(http://www.google.com/);
}

/* OK */
.format {
  background-image: url(//www.google.com/);
}
```

<a name="#id-vs-class"></a>
## 3. ID かクラスか
ページ内に 1度だけ出現するものには id を使い、そうでない場合は class を使う。どちらか迷ったら class を使おう。  
さらに言うなら、基本的には一部のコンテンツを指定したい場合や SMACSS のレイアウトカテゴリー以外で id を使うべきではなく、他では class を使うべき。

- 良い id の例: header, main, footer
- 悪い id の例: navigation, list, contents name

<a name="naming"></a>
## 4. ID やクラスの命名
### 意味のわかる名前をつける
コンポーネントの意味がわかる名前で書く。  
連番や見た目を表した名前は使用してはいけない。

```css
/* NG: 連番（意味がわからん） */
.message-1 {
  ...
}

.message-2 {
  ...
}

/* NG: 見た目を表してる */
.button-red {
  ...
}

.clear {
  ...
}

/* OK: 役割を表してる */
.message-user {
  ...
}

.message-shop-owner {
  ...
}

.list {
  ...
}
```

### ID とクラスの命名スタイル
単語が複数ある場合はアンダースコア ( `_` ) で単語をつないで書こう。  
単語が複数ある場合は必ず切り離して。例外は HTML の要素名になってるものとか、それが一般的な場合かな。

```css
/* NG */
.headeritem {
}

/* OK */
.header_item {
  ...
}

/* Exception */
.figcaption {
  ...
}
```

プロジェクトによっては BEM を使うのもいいね。  
その時はハイフン ( `-` ) とアンダースコア ( `_` ) を使って BEM のルールに従おう。  
BEM ( Block, Element, Modifier ) のルール:

- Block .. **アプリケーションの構成要素** に当たるもの。単体の Block もあれば複数の Block を含む複合物のものもある。
- Element .. **Block の構成要素** （検索 Block 内の入力欄とボタンとか）。
- Modifier .. 元となる **Block や Element で一部スタイルの変更が必要な時にに使うもの** 。

BEM について詳細が知りたい場合は公式サイトを読むのが一番いいけど、「英語プギャー」ってなったら自分で書いたブログとか他の人が上手くまとめてるやつ見て。

- [BEM](http://bem.info/)
- [BEM とは](http://chroma.hatenablog.com/entry/2013/12/12/200817)
- [Japanese Translations of BEM-Methodology](https://github.com/juno/bem-methodology-ja)
- [BEMという命名規則とSass 3.3の新しい記法](http://blog.ruedap.com/2013/10/29/block-element-modifier)

### 単語の省略
複数単語が連なる際、それらを省略しようとしてはいけないよ。

```css
/* NG */
.fnav {
  ...
}

/* OK */
.footer-navigation {
  ...
}
```

また、いつでも省略可能なものとしては以下を上げている。  
これら以外に省略して記述したい単語がある場合は検討の末、プロジェクトのドキュメントに残すこと。

一般的なものとして省略を許している単語:

- navigation => nav
- previous => prev - thumbnail => thumb
- picture => pic
- background => bg
- banner => bnr
- image => img

接頭辞としての省略:

- button => btn ( `class="button btn-primarily"` のようなマルチクラスの指定で、モジュールに接頭辞を付ける場合に限る )
- icon => ico ( `class="icon ico-message"` のようなマルチクラスの指定で、モジュールに接頭辞を付ける場合に限る )
- layout => l ( SMACSS のレイアウトカテゴリー内で使う場合に限る )
- grid => g ( SMACSS のレイアウトカテゴリー内で使う場合に限る )
- javascript => js ( Javascript で使うクラスとスタイルのクラスを分ける場合に限る )

<a name="simplification-of-task"></a>
# 5. [ オプション ] Grunt 、タスクの簡略化
これはやらなくてもいいけど、やったほうがいいこと。

タスクを登録しておけばコマンドを叩くことでコンパイル処理などが簡単に行えるようになるよ。  
ドキュメントの豊富さから、今のところは Grunt を使おう。

- [GRUNT](http://gruntjs.com/)

Grunt がやってくれること:

- Sass => CSS, HTML => Slim といったコンパイル処理の自動化
- ファイルの結合化
- ファイルサイズの縮小化（難読化）
- HTML, CSS, JS のバリデーション
- スタイルガイドの追加・更新
- CSS のプロパティ列挙順の統一化
- ライブリロード
- CSS ベンダープレフィックスの付与

<a name="reference"></a>
## 6. 参考文献
- [「Google HTML/CSS Style Guide」を適当に和訳してみた](http://re-dzine.net/2012/05/google-htmlcss-style-guide/)
- [GitHubのHTML/CSS Styleguideを適当に和訳してみた](http://re-dzine.net/2012/09/github-htmlcss-styleguide/)
