---
title: Develop
---

# 開発

Mkdocsの使い方のメモ。


## Installation

- HomeBrew ではインストールしない！
- pip でインストールする。

mkdocs のインストール

```sh
pip install mkdocs
```

## 使い方

ディレクトリ移動して

```sh
mkdocs serve
```

でサーバーを起動。

ブラウザで http://127.0.0.1:8000 にアクセスすれば、
生成されたページを見ることができる。

サーバーを終了するには `ctrl + C` を入力する。


GitHub Pages を更新するには、以下のコマンドでデプロイする。

```sh
mkdocs gh-deploy
```

## pip installations

とりま現状で必要なやつら；

```sh
pip install pymdown-extensions
pip install mkdocs-material-extensions
pip install fontawesome_markdown
pip install mdx_truly_sane_lists
pip install mkdocs-git-revision-date-localized-plugin
```

## ローカル環境のメモ

- `mkdocs` のインストール・管理は、HomeBrew でインストールした `python 3.9` と一緒にインストールされた `pip3` で行っている。
- 管理している pip のパスは `/usr/local/bin/pip3` で、`~/.zshrc` で単に `pip` とエイリアスを設定している。
- mkdocs を直接 HomeBrew でインストール・管理はしていないので注意。
- 故に、mkdocs のアップデートは `pip` コマンドで行う。

## pip コマンド

### pip で管理しているものをリスト表示

```sh
pip list
```

### 新しいバージョンの有無をチェック

```sh
pip list --outdated
```

or

```sh
pip list -o
```

### pip の更新

```sh
pip install --upgrade pip
```

or

```sh
pip install -U pip
```

### mkdocs の更新

```sh
pip install --upgrade mkdocs
```

or

```sh
pip install -U mkdocs
```

なお、pip 自体も自動で更新される。
