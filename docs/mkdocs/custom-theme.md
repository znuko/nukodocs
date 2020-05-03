---
title: Customize Theme
---

# テーマの上書き

- [Styling Your Docs - MkDocs](https://www.mkdocs.org/user-guide/styling-your-docs/#overriding-template-blocks)

既存テーマを上書きしたいときは、それをDLしてきて直接編集するのではなく、 overrides という機能を使うのがよい。

projectディレクトリに `overrides` ディレクトリを作り（ディレクトリ名は任意）、その中に `main.html` を作成する。

```
project/
    mkdocs.yml
    docs/
    overrides/
        main.html
```

`mkdocs.yml` には次のように記述する；

```yaml
theme:
  name: material
  custom_dir: overrides
```

## ページタイトルの変更

各ページのタイトルを変更するには、 `htmltitle` block を上書きする。

`/overrides/main.html` に以下のように記述する；

```jinja
{% extends "base.html" %}

{% block htmltitle %}
  <title>Custom title goes here</title>
{% endblock %}
```

## script の追加

scriptの追加は、 `script` block を `/overrides/main.html` に記述すればいい。

!!! tip
    `<script>` に `type` を指定したいなどの特別な事情がない場合は、 `mkdocs.yml` の `extra_javascript` から簡単にjsを追加できる。

`script` block にはテーマ（`base.html`）で既にいくつか記述がある。

それを無かったことにして上書きするのではなく、単にscriptを追加したいだけであれば、 `super()` を使うことで親（`base.html`）にある記述を呼び出すことができる。

つまり、`/overrides/main.html` には以下のように記述すれば良い；

```jinja
{% extends "base.html" %}

{% block scripts %}
  {{ super() }}

  <script>
    hoge hoge
  </script>
{% endblock %}
```