---
title: Development
---

# Git

## git-flow

理想：

- master
  - 直pullはしない
- gh-deploy
  - `mkdocs gh-deploy` コマンドで自動にpullされる
  - github pages の公開ブランチ
- article
  - 記事の追加・更新
- mkdocs
  - `nav` 以外で`mkdocs.yml` の編集だったり、拡張機能の追加、サイト全体の設定の変更とか。
  - mkdocsの記事編集はここでもいい