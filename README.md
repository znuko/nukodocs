# README

## 使い方

ディレクトリ移動して

```sh
mkdocs serve
```

でサーバーを起動。

ブラウザで http://127.0.0.1:8000 にアクセスすれば、
生成されたページを見ることができる。


GitHub Pages を更新するには、以下のコマンドでデプロイする。

```sh
mkdocs gh-deploy
```

URLはこれ：nukoyama.github.io/mkdocs-test/

## pip installations

とりま現状で必要なやつら；

```sh
pip install pymdown-extensions
pip install mkdocs-material-extensions
pip install fontawesome_markdown
pip install mdx_truly_sane_lists
pip install mkdocs-git-revision-date-localized-plugin
```
