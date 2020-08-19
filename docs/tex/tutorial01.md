---
title: 初級編（前編）
---

LaTeX 入門チュートリアルです。精進してください。

# はじめに

## このチュートリアルの内容

この LaTeX チュートリアル 初級編（前編）では、LaTeX とはなんぞやというところから、
超基本的な LaTeX 文書のタイプセット、最低限の環境構築を終えるところまで最速で行ってもらいます。

コピペばかりで理解の方は全くできないと思いますが、そこは次回以降のチュートリアルに任せることにします。

ここでは、とにかく、とりあえず LaTeX が使えるようになるのが目的です。

## LaTeX とは？

LaTeX は「ラテフ」とか「ラテックス」と読みます。

LaTeX は文書を作成するソフトです。
Microsoft Office の Word みたいなものです。

LaTeX は、（本当は正しくないですが）単に tex と略されます。

## とりま使ってみる

自分のPCにインストールする前に、とりあえずどんなもんか試してみましょう。

まずは [奥村さんの「TeXを使ってみよう」](https://oku.edu.mie-u.ac.jp/~okumura/texonweb/) にアクセスします。

入力ボックスに以下の内容を貼り付けます（コピペ）。

```tex
\documentclass{jsarticle}
\title{\LaTeX 入門}
\author{あなたの名前}
\begin{document}
\maketitle
\section{テスト}
私は$E = mc^2$を発見しました。
\end{document}
```

「PDF生成」ボタンをクリックすると、処理結果が表示されます。

一番下のPDFファイルを開くと、完成した文書が見れます。


# 自分のPC（ローカル）で使えるようにする

それでは、自分のPCにLaTeXをインストールして、tex ファイルから PDF の文書を生成するところまでいきましょう。

## TeX Live のインストール

LaTeX を使えるようにするには、LaTeX 本体とその他もろもろがセットになった [TeX Live](http://www.tug.org/texlive/) をインストールするのが手っ取り早いです。

詳しくは以下の記事を参考にしてください。

- [TeX Live - TeX Wiki](https://texwiki.texjp.org/?TeX%20Live#w628bee6)


### MacOS の場合

TeX Live を Mac 用にカスタマイズした [MacTeX](http://tug.org/mactex/) をインストールします。

下記リンクからDLページにアクセスします。

- [Downloading MacTeX 2020](http://tug.org/mactex/mactex-download.html)

「`MacTeX.pkg`」のリンクをクリックして、インストーラをDLします。

DLが完了したら、そのパッケージを開いて、インストーラを起動します。

あとはGUIウィンドウでポチポチやってれば、TeX Live のインストールができるはずです。

- 参考
  - [MacTeX - TeX Wiki](https://texwiki.texjp.org/?MacTeX)


### Windows の場合

下記リンクからDLページにアクセスします。

- [Installing TeX Live over the Internet](https://www.tug.org/texlive/acquire-netinstall.html)

文中にあるリンクの「`install-tl-windows.exe`」をクリックして、インストーラをDLします。

DLが完了したら、そのインストーラを起動します。

あとはGUIウィンドウでポチポチやってれば、TeX Live のインストールができるはずです。

- 参考
  - [TeX Live/Windows - TeX Wiki](https://texwiki.texjp.org/?TeX%20Live%2FWindows)


## タイプセット

「タイプセット」とは、他のプログラミング言語で言うところのコンパイルのようなものです。

メモ帳などのエディタで作成した tex ファイルをタイプセットすることで、目的の PDF ファイルが生成されます。

まずは、最も基本的な方法である、CUI（コマンドライン）でのタイプセットの方法をみていきます。

### `platex` + `dvipdfmx` を使う

LaTeX にもいろいろ種類があるのですが、ここでは LaTeX を日本語が使えるように拡張した pLaTeX を使った例をみることにします。

まず、エディタ（メモ帳とか何でもいい）を起動し、新規ファイルを作成します。

そこに以下のコードをコピペして、`test01.tex` という名前（と拡張子）で保存します。

```tex
\documentclass{jsarticle}
\title{\LaTeX 入門}
\author{あなたの名前}
\begin{document}
\maketitle
\section{テスト}
私は$E = mc^2$を発見しました。
\end{document}
```

上記の内容の tex ファイルを作成したら、ターミナル（端末、コマンドプロンプト）を起動します。
黒い画面のやつです。

ターミナル上で `cd` コマンドを使って、先ほど作成した tex ファイルがあるディレクトリ（フォルダ）まで移動します。

移動できたら、ターミナルで次のコマンドを入力し、実行（Enter キーを入力）します；

```sh
platex test01.tex
```

すると、いくつかのファイルとともに `test01.dvi` というファイルが生成されます。

次に、この dvi ファイルから pdf ファイルを生成するために、次のコマンドを実行します；

```sh
dvipdfmx test.dvi
```

すると、目的の pdf ファイル `test01.pdf` が生成されます。


### `latexmk` を使う

先に見た方法では、tex ファイルから pdf ファイルを生成するのに、2回もコマンドを打たなくてないけなくて面倒です。

さらに、目次や図・数式番号などの相互参照のある文書を作ろうと思うと、複数回 `platex` コマンドを実行する必要があります。

また、 `platex` コマンドにはいろいろ便利なオプション引数（後述）を与えることもできますが、それらを毎回打つのは面倒です。

以上のことから、より簡単にタイプセットするために `latexmk` というコマンドを紹介しておきます。

`latexmk` コマンドで tex 文書をタイプセットするには、あらかじめ設定ファイファイルを配置しておく必要があります。

まず、エディタを開いて、新規ファイルをホームディレクトリ（`cd ~` で行ける場所）、あるいは tex ファイルと同じディレクトリに作成します。

それに、以下の内容をコピペして、`latexmkrc` という名前（拡張子は無し）で保存します；

```perl
#!/usr/bin/env perl
$latex    = "platex %O -synctex=1 %S";
$dvipdf   = "dvipdfmx %O -o %D %S";
$pdf_mode = 3;
```

設定ファイルの準備ができたら、あとは以下のコマンドを打つだけで、一気に pdf ファイルまで生成できます；

```sh
latexmk test01.tex
```

また、 `-c` オプションを付けると、`.aux` や `.log` などの中間ファイルを自動で消去してくれます；

```
latexmk -c test01.tex
```

# 開発環境（エディタ）

今までの話では、ターミナルからコマンド操作で tex のタイプセットを行う方法を述べました。

TeX Live には、わざわざコマンドを打たなくても、ボタン一つでタイプセットを行ってくれる便利なソフトが付属しています。

OS別にそれぞれ次のようなソフトが既にインストール済みのはずです；

- Windows の場合は「[TeXworks](http://www.tug.org/texworks/)」
- Mac の場合は「[TeXShop](https://pages.uoregon.edu/koch/texshop/)」

それぞれの環境設定の方法を簡単に見ておきましょう。

## TeXworks (Windows)

保留中。ggrks

- 参考
  - [TeXworks - TeX Wiki](https://texwiki.texjp.org/?TeXworks)

## TeXShop (Mac)

多分、デフォルトの設定ではうまくタイプセットできません。

TeXShop を起動したら、`cmd + ,` で環境設定を開きます。

表示された「TeXShop 環境設定」ウインドウの「書類」タブの左下にある「設定プロファイル」から「pTeX (latexmk)」を選択します。

「OK」を押すと設定完了です。

あとは、メインウィンドウの左上にある「タイプセット」のボタンを押せば、開いているtex文書をタイプセットし、生成されたpdfを自動で開いてくれます。

- 参考
  - [TeXShop - TeX Wiki](https://texwiki.texjp.org/?TeXShop)

## VSCode（おすすめ）

TeXworks や TeXShop でも十分かもしれませんが、Microsoft 製のフリーソフト「[Visual Studio Code](https://code.visualstudio.com)（略して vscode）」を使えば、もっと快適な LaTeX 環境を構築することができます。

ここでは、とりあえず vscode で LaTeX のタイプセットができるようになるまでの手順を簡単に述べます。

まずは、下記リンクから vscode をDLして、インストールします。

- [Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/download)

インストールができたら、vscode を起動します。

`cmd + shift + X` （Windowsの場合は  `ctrl + shift + X` ）を押すか、左のサイドバーにある四角が4つあるアイコンをクリックすると、拡張機能の検索窓が開くので、「latex」と入力すれば表示される「[LaTeX Workshop](https://github.com/James-Yu/LaTeX-Workshop)」という拡張機能をインストールします。

拡張機能のインストールが完了したら、一旦 vscode を再起動します。

次に、 `cmd + ,` （Windowsの場合は `ctrl + ,` ）を押して設定タブを開いて、
右上にあるアイコン（カーソルをホバーすると「設定(UI)を開く」と表示される）をクリックして `settings.json` を開きます。

vscode の環境設定ファイル `settings.json` に、以下のコードをコピペして `cmd + S` で（Windowsの場合は `ctrl + S` ）で保存します；

```json
{
  "latex-workshop.latex.tools": [
    {
      "name": "Latexmk (pLaTeX)",
      "command": "latexmk",
      "args": [
        "-latex='platex'",
        "%DOC%"
      ]
    },
  ],
  "latex-workshop.latex.recipes": [
    {
      "name": "pLaTeX",
      "tools": [
        "Latexmk (pLaTeX)"
      ]
    }
  ],
  "latex-workshop.latex.autoClean.run": "onBuilt",
  "latex-workshop.latex.clean.fileTypes": [
    "*.aux", "*.toc", "*.log", "*.dvi", "*.fdb_latexmk", "*.fls"
  ]
}
```

!!! note
    `settings.json` の `{ }` の中に既に何か書かれている場合は、その最後の行をカンマ `,` で区切った後、上記コードの `{ }` の中身を、後ろに追加する形でコピペしてください。

以上で準備は完了です。
あとは、texファイルを vscode で開いて、`cmd + opt + B`（Windowsの場合は `ctrl + alt + B`）を押せば、タイプセットできます。

生成された pdf を確認するには、`cmd + opt + V`（Windowsの場合は `ctrl + alt + V`）を押すと、pdf がタブ表示でプレビューされます。

!!! attention
    ここでの話は、 `latexmkrc` の存在を前提とした設定方法です。
    上で説明した `latexmk` コマンドのための設定ファイル `latexmkrc` をホームディレクトリか、texファイルと同じディレクトリに配置しておいてください。


# PDF ビューア

最後に、おすすめのPDFビューアを紹介しておきます。

フリーソフトかつ軽快で、後に説明する synctex に対応したものとしては、次の2つがあげられます；

- [sumatraPDF](https://www.sumatrapdfreader.org/free-pdf-reader.html) (Windows)
- [Skim](https://skim-app.sourceforge.io) (Mac)

どちらも一方のOSにしか対応していませんが、普段使いのPDFビューアとしても利用できるので、この機会にインストールしておくとよいでしょう。

## smatraPDF (Windows)

[公式のDLページ](https://www.sumatrapdfreader.org/download-free-pdf-viewer.html)からDLしてください。

## Skim (Mac)

[公式ページ](https://skim-app.sourceforge.io)の左のサイドバーにある「Download」リンクをクリックしてDLしてください。