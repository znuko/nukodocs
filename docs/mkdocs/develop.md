---
title: Develop
---

# 環境構築

Mkdocsの使い方のメモ。


## Installation

!!! warning
    インストールはHomeBrewではなくpipでインストールすること。

mkdocs のインストール；

```sh
pip install mkdocs
```


## ビルド

`mkdocs.yml` があるディレクトリ移動して、サーバーを起動；

```sh
mkdocs serve
```

ブラウザで http://127.0.0.1:8000 にアクセスすれば、
生成されたページを見ることができる。

サーバーを終了するには `ctrl + C` を入力する。


GitHub Pages を更新するには、以下のコマンドでデプロイする。

```sh
mkdocs gh-deploy
```


## 必要なパッケージ

このサイトをビルドするには、下記のパッケージをインストールする必要がある；

```
pymdown-extensions
mkdocs-material-extensions
fontawesome_markdown
mdx_truly_sane_lists
mkdocs-git-revision-date-localized-plugin
```

パッケージのインストールは `pip install <package>` のようにpipコマンドを実行する。

必要なパッケージは `requirements.txt` に書いておいて、以下のコマンドでまとめてインストールできる；

```sh
pip install -r requirements.txt
```


# ローカル環境のメモ

- `mkdocs` のインストール・管理は、HomeBrew でインストールした `python 3.9` と一緒にインストールされた `pip3` で行っている。
- 管理している pip のパスは `/usr/local/bin/pip3` で、`~/.zshrc` で単に `pip` とエイリアスを設定している。
- mkdocs を直接 HomeBrew でインストール・管理はしていないので注意。
- 故に、mkdocs のアップデートは `pip` コマンドで行う。


# pipコマンド

## pip で管理しているものをリスト表示

```sh
pip list
```

## 新しいバージョンの有無をチェック

```sh
pip list --outdated
```

or

```sh
pip list -o
```

## pip の更新

```sh
pip install --upgrade pip
```

or

```sh
pip install -U pip
```

## mkdocs の更新

```sh
pip install --upgrade mkdocs
```

or

```sh
pip install -U mkdocs
```

なお、pip 自体も自動で更新される。


# Deploy to GitHub Pages

GitHub Pagesにデプロイするときのメモ。

GitHub Actionsを用いて、`push` したときに自動でデプロイするように設定する。

## workflowファイル

Actionsを使うためにworkflowファイルを作成する。

ディレクトリ `.github/workflows` 内に任意の名前で `yml` ファイルを作る。

例えば `github-pages.yml` とかで。内容は以下のものをコピペする；

```yaml
name: Publish docs via GitHub Pages
on:
  push:
    branches:
      - master
jobs:
  build:
    name: Deploy docs
    runs-on: ubuntu-latest
    steps:
      - name: Checkout master
        uses: actions/checkout@v2

      - name: Deploy docs
        uses: mhausenblas/mkdocs-deploy-gh-pages@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

!!! note
    リポジトリの「Settings」>「Actions」の「Workflow permissions」のところで、「Read repository contents permission」にチェックが入っている場合は、Actionsにpush権限がないので、tokenを設定してやらないといけないらしい。
    今のところは「Read and write permissions」にチェックを入れているので、特に気にする必要はないっぽい。

上の設定では、`master`ブランチにpushがあったときに、`gh-deploy`ブランチにビルドしたサイトをpushするようなActionが実行される。

なので、GitHub Pagesで公開するブランチは `gh-deploy` のルート `/` を指定する。

!!! info
    もちろん細かい設定は変更可能。詳細は公式のマニュアルを参照。

ここに書いたworkflowでは、GitHub Actions公式のMkDocsをDeployするActionsを使っている。

- マニュアル： https://github.com/marketplace/actions/deploy-mkdocs