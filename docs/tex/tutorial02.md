---
title: 初級編（後編）
---

# はじめに

## このチュートリアルの内容

この LaTeX チュートリアル 初級編（後編）では、
自分でレポートとかを LaTeX を使って作れるようになるレベルまで、最速で到達してもらいます。

細かい説明はあえて省略していますが、最低限必要であろうコマンドは一通り説明しているつもりです。

!!! info
    前回に引き続き、このページにあるサンプルコードは、
    `platex` + `dvipdfmx` を使ってタイプセットすることを想定して書いています。

## tex用語・文書構成

texファイルからpdfファイルを生成することを「タイプセット」と言います。

ここでは、texファイルの基本的な構成について説明します。

以下のコードは、`Hello, LaTeX!` を出力するだけの最もシンプルなものです；

```tex linenums="1"
\documentclass{jsarticle}
\begin{document}
  Hello, LaTeX!
\end{document}
```

1行目の `\documentclass` は、文書のクラスを指定するコマンドです。

文書のクラスとは、テーマのようなもので、記事や書籍、レポートなどのクラスがあらかじめ用意されています。
上の例では `jsarticle` という和文記事の文書クラスを指定しています。

| クラス名     | 用途     |
| ----------- | ------- |
| `jsarticle` | 和文記事 |
| `jsbook`    | 和文書籍 |
| `jsreport`  | 和文レポート |

`\documentclass` の直後の `{ }` で、コマンドの引数として文書クラスの名前を与えています。

2行目と4行目にあるような `\begin` と `\end` がセットになっているコマンドは一般に「環境」と呼ばれます。

上の例にある `\begin{document}` ~ `\end{document}` は `document` 環境と呼ばれ、
この環境の中に書いた文章が、pdfの内容として出力されます。

つまり、上の例では、3行目に書いた `Hello, LaTeX!` がpdfに出力されるわけです。


# 基本的な LaTeX コマンド

## コメント文

コメント文とは、タイプセットの際に無視される文のことです。

コード中に `%` を書くと、以降の文が（改行されるまで）無視されます（コメントアウト）。

```tex linenums="1"
\documentclass{jsarticle} % class を指定
% メモなどを書いておけます
\begin{document}
  % \LaTeX <- 無視
  Hello, LaTeX! % %以降は無視
\end{document}
```

## クラスのオプション

クラスにはいくつかのオプションが用意されています。

!!! note
    オプション引数とは、省略可能な引数のことです。
    省略した場合は、標準で設定されている値が適用されます。

    普通の引数は `{ }` で与えますが、オプション引数は `[ ]` で与えます。

例えば、フォントサイズを 12pt にするには、
以下のようにして `\documentclass` コマンドにオプションを与えます；

```tex
\documentclass[12pt]{jsarticle}
```

!!! tip
    標準（デフォルト）のフォントサイズは 10pt です。
    何も指定しなければ、このサイズになります。

さらに、用紙サイズ（標準ではA4）を B5 に変更するには、
`b5paper` と `papersize` を書き加えます；

```tex
\documentclass[12pt,b5paper,papersize]{jsarticle}
```

!!! info
    このチュートリアルでは platex でのタイプセットしか説明しませんが、
    platex をユニコード文字が使えるように拡張した uplatex というものもあります。

    uplatex を使ってタイプセットするには、クラスのオプションに `uplatex` を指定する必要があります；

    ```tex
    \documentclass[uplatex]{jsarticle}
    ```

## タイトルなどの出力

文書のタイトルや著者名、日付などを出力するには `\maketitle` というコマンドを使います；

```tex linenums="1"
\documentclass{jsarticle}

\title{LaTeX チュートリアル} % タイトル
\author{物理太郎} % 著者
\date{2020年8月24日} % 日付

\begin{document}
  \maketitle % これで出力
  Hello, LaTeX!
\end{document}
```

3行目の `\title{}` コマンドに、引数として文書のタイトルを指定します。
4行目の `\author{}` には著者名を、5行目の `\date{}` には日付を指定します。

上の例では、日付を直接指定していますが `\date{\today}` と書けば、
タイプセットしたときの日付を自動で指定することができます。

あとは、document環境中に `\maketitle` と書けば、そこにタイトルなどが出力されます。

出力されるタイトルなどのスタイルは、`\documentclass{}` で指定した文書のクラスに依存します。

## 段落

段落を作るには、`\par` コマンドを使います；

```tex linenums="1" hl_lines="4 7"
\documentclass{jsarticle}
\begin{document}
  吾輩は猫である。名前はまだ無い。
  \par
  どこで生れたかとんと見当けんとうがつかぬ。
  何でも薄暗いじめじめした所でニャーニャー泣いていた事だけは記憶している。
  \par
  続きはWebで。
\end{document}
```

あるいは、文中に空行を入れることでも、段落が作られます；

```tex linenums="1" hl_lines="4 7"
\documentclass{jsarticle}
\begin{document}
  吾輩は猫である。名前はまだ無い。

  どこで生れたかとんと見当けんとうがつかぬ。
  何でも薄暗いじめじめした所でニャーニャー泣いていた事だけは記憶している。

  続きはWebで。
\end{document}
```

!!! attention
    文章の区切りには、段落コマンド `\par` を使いましょう。

    くれぐれも、ただの改行でしかない `\\` コマンドを使わないように。


## 見出し

見出しは `\section{}` というコマンドで出力することができます。

```tex linenums="1"
\documentclass{jsarticle}

\begin{document}
  \section*{はじめに} % 章番号なし
  Hello, LaTeX!

  \section{テーラー展開} % 節
  \subsection{三角関数} % 小節
  サイン、コサイン、タンジェント。

  \subsection{指数関数} % 小節
  指数関数は、、、
\end{document}
```

章番号は、順に自動で出力されます。
章番号を出力したくない場合は、代わりに `\section*{}`というコマンドを使います。

小節の出力には `\subsection{}`、さらには `\subsubsection{}` が用意されています。

章立ても文書クラスに依存します。

| コマンド | 説明 | 備考 |
| ------ | --- | --- |
| `\part{}` | 部 | |
| `\chapter{}` | 章 | `jsarticle` クラスでは使用不可 |
| `\section{}` | 節 | |
| `\subsection{}` | 小節 | |
| `\subsubsection{}` | 小々節 | `jsbook`, `jsreport` クラスでは番号なし |
| `\paragraph{}` | 段落 | 番号なし |
| `\subparagraph{}` | 小段落 | 番号なし |

!!! tip
    余程大規模な文書でない限りは、`\section` から始めれば十分です。
    book クラスの場合は `\chapter` から始めましょう。

## 目次

目次を作成するには、`\tableofcontents` コマンドを使用します；

```tex linenums="1" hl_lines="3"
\documentclass{jsarticle}
\begin{document}
  \tableofcontents % 目次出力
  \section*{はじめに}
  \section{てすてす}
    \subsection{てすー}
      \subsubsection{テスっと}
    \subsection{テスト}
  \section{てすてす}
    \subsection{てすー}
\end{document}
```

`\setcounter{tocdepth}{深さ}` で、目次に表示する見出しの深さを指定できます；

```tex linenums="1" hl_lines="3"
\documentclass{jsarticle}
\begin{document}
  \setcounter{tocdepth}{3} % 深さ指定
  \tableofcontents % 目次出力
  \section{はじめに}
  ...
\end{document}
```

| 深さ | 表示される見出し |
| --- | -------------- |
| `-1` | 部 `\part` のみ |
| `0` | 章 `\chapter` まで |
| `1` | 節 `\section` まで |
| `2` | 小節 `\subsection` まで（デフォルト） |
| `3` | 小々節 `\subsubsection` まで |

## 脚注

脚注を出力するには、次のように書きます；

```tex linenums="1"
\documentclass{jsarticle}
\begin{document}
  吾輩は猫\footnote{食肉目ネコ科ネコ属}である。
  名前はまだ無い\footnote{ちなみに、著者の名前は夏目漱石である。}。
\end{document}
```

!!! tip
    文末に脚注を付ける際は、`\footnote` コマンドは句点の前に入れるのが常識。

## 箇条書き

箇条書きをするには、`itemize` 環境を使用します；

```tex
\begin{itemize}
  \item りんご
  \item ぶどう
  \item メロン
\end{itemize}
```

`enumerate` 環境を使えば、リストに番号を付けられます；

```tex
\begin{enumerate}
  \item とまと
  \item キャベツ
  \item じゃがいも
\end{enumerate}
```

入れ子にもできます；

```tex
\begin{enumerate}
  \item くだもの
  \begin{enumerate}
    \item りんご
    \item ぶどう
    \item メロン
  \end{enumerate}
  \item やさい
  \begin{enumerate}
    \item とまと
    \item キャベツ
    \item じゃがいも
  \end{enumerate}
\end{enumerate}
```

番号の書式は、ローマ数字やアルファベットにも変更できます；

```tex hl_lines="2-3"
\begin{enumerate}
  \renewcommand{\labelenumi}{(\roman{enumi})} % 1段目の書式
  \renewcommand{\labelenumii}{\Alph{enumii}.} % 2段目の書式
  \item くだもの
  \begin{enumerate}
    \item りんご
    \item ぶどう
    \item メロン
  \end{enumerate}
  \item やさい
  \begin{enumerate}
    \item とまと
    \item キャベツ
    \item じゃがいも
  \end{enumerate}
\end{enumerate}
```

| コマンド | 書式 | 例 |
| --- | --- | --- |
| `\arabic` | アラビア数字 | 1, 2, 3, ... |
| `\roma` | 小文字のローマ数字 | i, ii, iii, ... |
| `\Roma` | 大文字のローマ数字 | I, II, III, ... |
| `\ahph` | 小文字のアルファベット | a, b, c, ... |
| `\Alph` | 大文字のアルファベット | A, B, C, ... |

!!! note
    番号の書式を文書全体に適用したいなら、
    `\renewcommand{\labelenumi}{(\roman{enumi})}` プリアンブルに書けばよい。

!!! tip
    `\renewcommand{\AAA}{BBB}` は、`\AAA` というコマンドを `BBB` という内容で再定義する、というコマンド。

## 数式環境

### テキストスタイル

文中で数式を使うときはドル記号 `$` で囲みます；

```tex
これは運動方程式 $F = ma$ です。
```

### ディスプレイスタイル

中央にデカデカと出力するときは、ドル記号2つ `$$` で囲みます；

```tex
$$
F = m \frac{dv}{dt}
$$
```

!!! tip
    `\frac{分子}{分母}` は、数式環境中で分数を出力するコマンドです。

### 複数行（align 環境）

ディスプレイスタイルの数式環境中で、数式を途中で改行するには、
`amsmath.sty` というスタイルファイルで定義された `align` 環境を使います。

!!! info
    標準の LaTeX で用意されている数式環境（`eqnarray` 環境とか）もありますが、
    このチュートリアルでは amsmath の align 環境に統一して使っていくことにします。

`align` 環境は、標準のLaTeXでは定義されていないので、
数学用のマクロ集である `amsmath` パッケージをロードする必要があります。

スタイルファイルのロードは、tex 文書中の「プリアンブル」と呼ばれる領域
（`\documentclass{}` と `\begin{document}` の間）に、
`\usepackage{}` というコマンドを書くことで行うことができます；

```tex linenums="1" hl_lines="4"
\documentclass{jsarticle}

% ここがプリアンブル
\usepackage{amsmath}

\begin{document}
  amsmath.sty で定義されている align 環境が使えます。
  \begin{align}
    z &= x + iy\\
      &= r (\cos \theta + i\sin \theta)
  \end{align}
\end{document}
```

`align` 環境の中で `\\` を書くと、そこで数式が改行されます。

改行した数式の位置を揃えるには、揃えたい場所に `&` を書きます。
上の例では、イコール `=` の位置で揃えるようにしています。

`align` 環境は自動で式番号を出力しますが、
式番号を出力したくない場合は、代わりに `align*` 環境を使うか、
`\notag` というコマンドを使います；

```tex linenums="1"
\documentclass{jsarticle}
\usepackage{amsmath}
\begin{document}
  align 環境では各行の式番号を出力。
  \begin{align}
    z &= x + iy\\
      &= r (\cos \theta + i\sin \theta)
  \end{align}

  align* 環境では式番号を出力しない。
  \begin{align*}
    z &= x + iy\\
      &= r (\cos \theta + i\sin \theta)
  \end{align*}

  notag コマンドを使えば、行単位で非表示にできる。
  \begin{align}
    z &= x + iy \notag \\
      &= r (\cos \theta + i\sin \theta)
  \end{align}
\end{document}
```

## 図の挿入

まずは、挿入したい図や画像を用意し、texファイルのあるディレクトリに配置します。

```
test.tex
fig01.png
```

画像を挿入するには、`graphicx` パッケージを使用します。

`\includegraphics` コマンドで `fig01.png` を読み込みます；

```tex linenums="1"
\documentclass{jsarticle}
\usepackage[dvipdfmx]{graphicx}
\begin{document}
  \includegraphics[width=5cm]{fig01.png}
\end{document}
```

`graphicx` パッケージを読み込む際、`dvipdfmx` オプションを与えます。

!!! info
    ドライバの指定は、グローバルオプションで与えることもできます。

    ```tex linenums="1" hl_lines="1"
    \documentclass[dvipdfmx]{jsarticle}
    \usepackage{graphicx}
    \begin{document}
      \includegraphics[width=5cm]{fig01.png}
    \end{document}
    ```

挿入する画像の出力サイズは、`\includegraphics` のオプション引数で与えます。
上の例では、横幅（`width`）が `5cm` となるように画像を挿入しています。

画像サイズの指定は、横幅 `width` の代わりに、高さ `height` で指定することもできます。
大きさの単位は `cm`, `mm`, `pt` など、いろいろ使えます。

画像を中央寄せするには `center` 環境を使用します；

```tex
\begin{center}
  \includegraphics[width=5cm]{fig01.png}
\end{center}
```

キャプションを付けるには、`figure` 環境を使用します；

```tex
\begin{figure}[htbp]
  \centering
  \includegraphics[width=5cm]{fig01.png}
  \caption{素晴らしい図}
\end{figure}
```

`htbp` というオプションは、図を挿入する位置を指定しています。
左に書いたもの程、優先度が高いです。

| オプション | 位置 |
| -------- | --- |
| `h` | ソースコード通りの位置 (here) |
| `t` | ページの上部 (top) |
| `b` | ページの下部 (bottom) |
| `p` | 別ページに単独で (page) |

## 表の作成

表を作成するには、`tabular` 環境を使用します；

```tex linenums="1"
\documentclass{jsarticle}
\begin{document}
  \begin{tabular}{rcl}
    \hline\hline
    野菜 & 色 & 味\\
    \hline
    トマト & 赤 & 酸っぱい\\
    キャベツ & 緑 & 無味\\
    じゃがいも & 茶色 & 美味しい\\
    \hline\hline
  \end{tabular}
\end{document}
```

上の例では、4行3列の表を出力しています。

列は `&` で区切り、`\\` で行を改めます。

`\hline` は、行方向に線を引くコマンドです。
2つ重ねると、2本の線を引きます。

`\begin{tabular}` の直後にある引数には、各列の位置を指定します。
3列の表を作るなら、3文字を指定します。

| 引数 | 位置 |
| --- | --- |
| `l` | 左寄せ |
| `c` | 中央寄せ |
| `r` | 右寄せ |

キャプションを付けるには、`table` 環境を使用します；

```tex
\begin{table}
  \centering
  \caption{野菜リスト}
  \begin{tabular}{rcl}
    \hline\hline
    野菜 & 色 & 味\\
    \hline
    トマト & 赤 & 酸っぱい\\
    キャベツ & 緑 & 無味\\
    じゃがいも & 茶色 & 美味しい\\
    \hline\hline
  \end{tabular}
\end{table}
```
!!! tip
    図のキャプションは図の下に付け、
    表のキャプションは表の上に付けるのが常識です。

## 相互参照

数式や図表にラベルを付け、式番号や図・表番号を参照することができます。

`\label{}` でラベルを付け、`\ref{}` で参照します；

```tex linenums="1" hl_lines="9 12 18"
\documentclass[dvipdfmx]{jsarticle}

\usepackage{amsmath}
\usepackage{graphicx}

\begin{document}
  \begin{align}
    f(x) = \sin x
    \label{eq:sin}
  \end{align}

  (\ref{eq:sin})式をプロットすると、図\ref{fig:sin}のようになります。

  \begin{figure}[htbp]
    \centering
    \includegraphics[width=5cm]{fig01.png}
    \caption{素晴らしい図}
    \label{fig:sin}
  \end{figure}

  さいごに、野菜のリストを表\ref{tab:vegetable}に示します。

  \begin{table}[htbp]
    \centering
    \caption{野菜リスト}
    \label{tab:vegetable}
    \begin{tabular}{rcl}
      \hline\hline
      野菜 & 色 & 味\\
      \hline
      トマト & 赤 & 酸っぱい\\
      キャベツ & 緑 & 無味\\
      じゃがいも & 茶色 & 美味しい\\
      \hline\hline
    \end{tabular}
  \end{table}
\end{document}
```

!!! note
    目次の作成や相互参照を利用するには `platex` コマンドを2回実行する必要があります。
    1回目のタイプセットで参照情報を記した `aux` ファイルを生成し、2回目にそれが読み込まれます。

    `latexmk` を使用すれば、1回のコマンド実行で、必要な数だけ自動で `platex` が実行されるので、
    ユーザがタイプセット改数を気にする必要はありません。

## 参考文献

参考文献は、`thebibliography` 環境で出力します；

```tex
参考文献\cite{test2020}より、、、

\begin{thebibliography}{99}
  \bibitem{test2020} 著者名、『書籍名』、出版社、出版年。
  \bibitem{simizu2004} 清水明，『新版 量子論の基礎』，サイエンス社，2004．
\end{thebibliography}
```

`\bibitem{}` の引数で、文献のラベルを指定します。

本文中で参照するには `\cite{}` を使います。