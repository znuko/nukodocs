---
title: Extensions
---

extensions 導入の備忘録。


# Material Extensions

materialテーマ標準のextensions。

## Admonition

`mkdocs.yml` :

``` yaml
markdown_extensions:
  - admonition
```

Types:

!!! note
    Qualifiers: `note` , `seealso`

!!! abstract
    Qualifiers: `abstract`, `summary`, `tldr`

!!! info
    Qualifiers: `info`, `todo`

!!! tip
    Qualifiers: `tip`, `hint`, `important`

!!! success
    Qualifiers: `success`, `check`, `done`

!!! question
    Qualifiers: `question`, `help`, `faq`

!!! warning
    Qualifiers: `warning`, `caution`, `attention`

!!! failure
    Qualifiers: `failure`, `fail`, `missing`

!!! danger 
    Qualifiers: `danger`, `error`

!!! bug
    Qualifiers: `bug`

!!! example
    Qualifiers: `example`

!!! quote
    Qualifiers: `quote`, `cite`

Changing the title:

=== "Result"
    !!! note "おすきなタイトル"
        に変更できます。
=== "md"
    ```
    !!! note "おすきなタイトル"
        に変更できます。
    ```

Removing the title:

=== "Result"
    !!! note ""
        たいとるなし
=== "md"
    ```
    !!! note ""
        たいとるなし
    ```

Collapsible blocks：

=== "Result"
    ??? note "Click me!!"
        本文を収納・展開できます
=== "md"
    ```
    ??? note "Click me!!"
        本文を収納・展開できます
    ```


## CodeHilite

- [CodeHilite - Material for MkDocs](https://squidfunk.github.io/mkdocs-material/extensions/codehilite/)

`mkdocs.yml`:

```yaml
markdown_extensions:
  - codehilite
```

行番号表示：

=== "Result"
    ``` python linenums="1"
    """ Bubble sort """
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```
=== "md"
    ```` md
    ``` python linenums="1"
    """ Bubble sort """
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```
    ````

特定の行をハイライトする；

=== "Result"
    ```tex hl_lines="1-2 6"
    \documentclass{jsarticle}
    \begin{document}
      \begin{align}
        H \psi = E \psi
      \end{align}
    \end{document}
    ```
=== "md"
    ````
    ```tex hl_lines="1-2 6"
    \documentclass{jsarticle}
    \begin{document}
      \begin{align}
        H \psi = E \psi
      \end{align}
    \end{document}
    ```
    ````

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# PyMdown Extensions

## 絵文字 Emoji

- [Emoji cheat sheet](https://www.webfx.com/tools/emoji-cheat-sheet/)

installation:

```
pip install pymdown-extensions
pip install mkdocs-material-extensions
```

`mkdocs.yml`:

```yaml
markdown_extensions:
  - pymdownx.emoji:
      emoji_index: !!python/name:materialx.emoji.twemoji
      emoji_generator: !!python/name:materialx.emoji.to_svg
```

examples:

- `:smile:` :smile:
- `:hankey: :poop: :shit:` :hankey: :poop: :shit:
- `:+1:` :+1:


## SmartSymbols

- [SmartSymbols - PyMdown Extensions Documentation](https://facelessuser.github.io/pymdown-extensions/extensions/smartsymbols/)

`mkdocs.yml` :

```yaml
markdown_extensions:
  - pymdownx.smartsymbols:
      fractions: false #? does not work
      ordinal_numbers: false
```

Markdown | Result
:------: | :----:
`(tm)` | ™
`(c)` | ©
`(r)` | ®
`c/o` | ℅
`+/-` | ±
`-->` | →
`<--` | ←
`<-->` | ↔
`=/=` | ≠
`1/4, etc.` | ¼, etc.
`1st 2nd etc.` | 1st 2nd etc.


## Keys

- [Keys - PyMdown Extensions Documentation](https://facelessuser.github.io/pymdown-extensions/extensions/keys/)


`mkdocs.yml` :

```yaml
markdown_extensions:
  - pymdownx.keys
```

| Markdown | Result |
| :------: | :----: |
| `++cmd+comma++` | ++cmd+comma++ |
| `++a+b+c+space++` | ++a+b+c+space++ |


## InlineHilite

- [InlineHilite - PyMdown Extensions Documentation](https://facelessuser.github.io/pymdown-extensions/extensions/inlinehilite/)

```yaml
markdown_extensions:
  - pymdownx.inlinehilite
```

| Markdown | Result |
| :------: | :----: |
| `` `\usepackage{amsmath}` `` | `\usepackage{amsmath}` |
| `` `:::tex \usepackage{amsmath}` `` | `:::tex \usepackage{amsmath}` |
| `` `#!tex \usepackage{amsmath}` `` | `#!tex \usepackage{amsmath}` |


## tabbed

=== "Result"
    === "tab 1"
      tab 1
    === "tab 2"
      tab 2
    === "tab 3"
      tab 3
    === "tab 4"
      tab 4
=== "md"
    ```md
    === "tab 1"
      tab 1
    === "tab 2"
      tab 2
    === "tab 3"
      tab 3
    === "tab 4"
      tab 4
    ```

続けて書くけど区切りたいときは `===` のあとに `!` を入れる；

=== "Result"
    === "Bash"
        ``` bash
        #!/bin/bash

        echo "Hello world!"
        ```

    === "C"
        ``` c
        #include <stdio.h>

        int main(void) {
          printf("Hello world!\n");
          return 0;
        }
        ```

    ===! "C++"
        ``` c++
        #include <iostream>

        int main(void) {
          std::cout << "Hello world!" << std::endl;
          return 0;
        }
        ```

    === "C#"
        ``` c#
        using System;

        class Program {
          static void Main(string[] args) {
            Console.WriteLine("Hello world!");
          }
        }
        ```

=== "md"
    ```hl_lines="18"
    === "Bash"
        ``` bash
        #!/bin/bash

        echo "Hello world!"
        ```

    === "C"
        ``` c
        #include <stdio.h>

        int main(void) {
          printf("Hello world!\n");
          return 0;
        }
        ```

    ===! "C++"
        ``` c++
        #include <iostream>

        int main(void) {
          std::cout << "Hello world!" << std::endl;
          return 0;
        }
        ```

    === "C#"
        ``` c#
        using System;

        class Program {
          static void Main(string[] args) {
            Console.WriteLine("Hello world!");
          }
        }
        ```
    ```












- - - - - - - - - - - - - - - - - - - - - - - - -

# MkDocs+

## Font Awesome

- [Font Awesome - MkDocs+](https://bwmarrin.github.io/MkDocsPlus/fontawesome/)

```
pip install fontawesome_markdown
```

`mkdocs.yml` :

```yaml
markdown_extensions:
  - fontawesome_markdown

extra_css:
  - "https://maxcdn.bootstrapcdn.com/font-awesome/4.6.1/css/font-awesome.min.css"
```
examples:

- `:fa-external-link:` :fa-external-link:
- `:fa-coffee:` :fa-coffee:
- `:fa-twitter:` :fa-twitter:
- `:fa-github:` :fa-github:


- - - - - - - - - - - - - - - - - - - - - - - - -

# Others

## indent spaces

- [Incorrect rendering of nested lists · Issue #545 · mkdocs/mkdocs](https://github.com/mkdocs/mkdocs/issues/545)
- [MkDocs でスペース2個のインデントをリストのネストとして認識させたい場合 - stamemo](https://stakiran.hatenablog.com/entry/2018/08/02/202816)

indentに必要はスペースはデフォルトでは `4` つになっている。
不便なので、`2` つに変更する。

```sh
pip install mdx_truly_sane_lists
```

`mkdocs.yml` :

```yaml
markdown_extensions:
  - mdx_truly_sane_lists
```

これで、スペース2つでもタブとして認識する。

!!! question
    それでも、一部機能はスペース4つじゃないと効かない？


## 定義リスト

`mkdocs.yml` :

``` yaml
markdown_extensions:
  - def_list
```

=== "Result"
    たーむ
    :  にゃおああああああああああああああああああああああああああああうぎゃあああああああああああああああああああああああああああああああああああああああああなんでえええええええええええええええ
=== "md"
    ```md
    たーむ
    :  にゃおああああああああああああああああああああああああああああうぎゃあああああああああああああああああああああああああああああああああああああああああなんでえええええええええええええええ
    ```


## リンクを新規タブで開く

``` yaml
markdown_extensions:
  - attr_list
```

kmarkdown と同じようにしてリンクを書く；

```md
[リンク名](URL){target=_blank}
```



