---
title: Custome CSS
---

## 一般論

自分でスタイルシートをカスタムするには、 `docs/` 以下にcssファイルを配置する；

```
my-project/
  docs/
    css/style.css
    index.md
    ...
  mkdocs.yml

```

`mkdocs.yml` には次のように記述する；

```yaml
extra_css:
  - css/style.css
```

## header awesome

下記サイトのautherのGitHubから、 `docs/css/custome.css` をダウンロードしてきて配置。

- [MkDocs の見出しを Font Awesome で装飾する | kurokobo.com](https://blog.kurokobo.com/archives/2952)
  - [リポジトリ](https://github.com/kurokobo/mkdocs-header-awesome/)
  - [デモページ](https://kurokobo.github.io/mkdocs-header-awesome/)

!!! note
    ブログ記事内の css サンプルコードのコピペだけじゃ無理だったので注意。