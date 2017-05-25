---
author: azu
---

# 文と式

本格的に基本文法について学ぶ前に、JavaScriptというプログラミング言語がどのような要素からできているかを見ていきましょう。

JavaScriptは、**文**（Statement）と**式**（Expression）から構成されています。

## 式

**式**（Expression）を簡潔に述べると、値を生成し、変数に代入できるものを言います。

`42`のようなリテラルや`foo`といった変数、関数呼び出しが式です。
また、`1 + 1`のような式と演算子の組み合わせも式と呼びます。

式の特徴として、式を評価すると結果の値を得ることができます。
この結果の値を**評価値**と呼びます。

評価した結果を変数に代入できるものは**式**であるという理解で問題ありません。

{{book.console}}
```js
// 1という式の評価値を表示
console.log(1); // => 1
// 1 + 1という式の評価値を表示
console.log(1 + 1); // => 2
// 式の評価値を変数に代入
var total = 1 + 1;
// 関数式の評価値(関数オブジェクト)を変数に代入
var fn = function() {
    return 1;
};
// fn() という式の評価値を表示
console.log(fn()); // => 1
```

## 文

**文**（Statement）を簡潔に述べると、処理を実行する1ステップが1つの文といえます。
JavaScriptでは、文の末尾にセミコロン(`;`)を置くことで文と文に区切りを付けます。

ソースコードとして書かれた文を上から処理していくことで、プログラムが実行されます。

```js
処理する文;
処理する文;
処理する文;
```

たとえば、if文やfor文などが**文**と呼ばれるものです。
次のように、文の処理の一部として式を含むことがあります。

```js
var isTrue = true;
// isTrueという式がif文の中に出てくる
if (isTrue) {
}
```

一方、if文などは文であり式になることはできません。

**式**ではないため、if文の評価結果をfor文に代入するといったことはできません。
そのため、次のようなコードは`SyntaxError`となります。

[import, statement-not-expression-invalid.js](src/statement-not-expression-invalid.js)

### 式文

一方、**式**（Expression）は**文**（Statement）になることができます。
文となった式のことを**式文**と呼び、基本的に文が書ける場所には式を書くことができます。

その際に、**式文**（Expression statement）は文の一種であるため、セミコロンで文を区切っています。

```js
// 式文であるためセミコロンをつけている
式;
```

式は文となることができますが、先ほどのfor文のように文は式となることができません。

### ブロック文

次のような、文を`{`と`}`で囲んだ部分を**ブロック**と言います。
ブロックには、複数の**文**を書くことができます。

```js
{
    文;
    文;
}
```

if文など文の中には、ブロックで終わるものがあります。

文の末尾にはセミコロンを付けるとしていましたが、
例外として**ブロックで終わる文**の末尾には、セミコロンが不要となっています。

```js
// ブロックで終わらない文なので、セミコロンが必要
if (true) console.log(true);
// ブロックで終わる文なので、セミコロンが不要
if (true) {
    console.log(true);
}
```

## function宣言（文）とfunction式

[関数と宣言][]の章において、関数を定義する方法を学びました。
functionキーワードから文を開始する**関数宣言**と、変数へ**関数式**を代入する方法があります。

関数宣言（文）と関数式は、どちらも`function`というキーワードを利用しています。

```js
// learn関数を宣言する関数宣言文
function learn() {
}
// 関数式をread変数へ代入
var read = function() {
};
```

この文と式の違いを見ると、関数宣言文にはセミコロンがなく、関数式にはセミコロンがあります。
このような、違いがなぜ生まれるのかは、ここまでの内容を適用することで説明できます。

関数宣言文で定義した`learn`関数には、セミコロンがありません。
これは、**ブロックで終わる文**にはセミコロンが不要であるためです。

一方、関数式を`read`変数へ代入したものには、セミコロンがあります。

<!-- textlint-disable preset-ja-technical-writing/ja-no-weak-phrase -->

「ブロックで終わる関数であるためセミコロンが不要なのでは？」と思うかもしれません。

<!-- textlint-enable preset-ja-technical-writing/ja-no-weak-phrase -->

しかし、この匿名関数は**式**であり、この処理は変数を宣言する文の一部であることが分かります。
つまり、次のように置き換えても同じといえるため、末尾にセミコロンが必要となります。

```js
function fn() {}
// fn(式)の評価値を代入する変数宣言の文
var read = fn;
```

## まとめ

この章では次のことについて学びました。

- JavaScriptは**文**（Statement）と**式**（Expression）から構成される
- 文は式になることができない
- 式は文になることができる（**式文**）
- 文の末尾にはセミコロンを付ける
- ブロックで終わる文は例外的にセミコロンを付けなくてよい

JavaScriptには、特殊なルールにもとづき、セミコロンがない文も行末に自動でセミコロンが挿入されるという仕組みがあります。
しかし、この仕組みは構文を正しく解析できない場合に、セミコロンを足すという挙動を含みます。
これにより、意図しない挙動を生むことがあります。そのため、必ず**文**の末尾にはセミコロンを書くようにします。

エディタやIDEの中にはセミコロンの入力の補助をしてくれるものや、[ESLint][]などのLintツールを使うことで、
セミコロンが必要なのかをチェックできます。

セミコロンが必要か見分けるにはある程度慣れが必要ですが、ツールを使い静的にチェックすることもできます。
そのため、ツールなどの支援を受けて経験的に慣れていくこともよい方法といえます。

[関数と宣言]: ../function-method/README.md
[ESLint]: http://eslint.org/  "ESLint - Pluggable JavaScript linter"