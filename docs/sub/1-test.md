---
title: SUPER TEST
description: Nullam urna elit, malesuada eget finibus ut, ac tortor.
hero: Set heroes with metadata
path: docs/sub/
source: 1-test.md
---


# first

[TOC]

## すること aa

- title以外に、metadata何か使えないか？
- mdの機能一通り確認す[^1]

[^1]: あっっっっっっはああ


!!! info
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

!!! うんこ
    おいしい

!!! warning "うんこ"
    うんこをたべちゃだめ

??? note "open the unko"
    null unko!!


oisikunai.[^2]

[^2]: んんんんんあああああ

にゃおいういいいーーん[^3]。ぴえん

[^3]: ほんんげらああんもええ

## ああああ 

==あああっっっs==

aa^ぴろり^

```tex hl_lines="1 3-5"
\documentclass{jsarticle}
\begin{document}
  \begin{align}
    H \psi = E \psi
  \end{align}
\end{document}
```

- [ ] aa
- [ ] bb
    - [x] unko
    - [x] konu
- [cheat-sheet](https://yakworks.github.io/mkdocs-material-components/cheat-sheet/){:target=_blank}


## tab spaces

=== "md"
    ````
    ``` python linenums="1"
    """ Bubble sort """
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```
    ````
=== "Result"
    ``` python linenums="1"
    """ Bubble sort """
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```

大丈夫

=== "aaa"
    aaaaa
    aaa
    a

=== "bbbbb"
    bbb bbb