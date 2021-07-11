---
title: Issues
---

設定やら問題とかの備忘録。


# Material theme

Materialテーマ関係。


## 見出しの前に装飾文字を入れられない

ヘッダーが固定されているページでは、ページ内リンクで `id` へ飛ぶとズレる（見出しがヘッダーに隠れる）。

その問題を修正するために、Materialテーマでは擬似要素 `::before` でネガティブマージンを設定してうまいことやっている（この方法は主流な方法）。

ただしこのとき、擬似要素 `::before` を

```css
::before {
  display: block;
}
```

としなければいけない。

しかしそうすると

```css
h1::before {
  content: "装飾";
}
```

のように、見出しを装飾しようとすると、`::before` 直後に改行が入って、そのあとに見出しのテキストが表示される形になってしまう。

そうならないためには

```css
::before {
  display: inline-block;
}
```

としなければならないが、これはページ内リンクのズレ修正と競合してしまう。

Font Awesome で装飾文字を入れたいが、とりあえずは諦めることにする。

### 追記

1文字だけだったら、Materialテーマと競合せず、見出しの先頭に文字を入れることができた。

```css
/* 擬似クラス ::first-letter を使う */
.md-typeset h1::first-letter,
.md-typeset h2::first-letter,
.md-typeset h3::first-letter,
.md-typeset h4::first-letter {
  float: left;
  margin-right: .3em;
}

/* display: block; のまま */
.md-typeset > ::before {
  font-family: "FontAwesome";
  /* margin-right: .3em; */
  /* display:inline-block !important; */
}

/* content のプロパティは1文字だけ */
.md-typeset h1::before {
  content: "\f02d" !important;
}
```

多分うまいこといってる。

