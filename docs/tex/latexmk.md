---
title: latexmk について
---

`.latexmkrc` より `latexmkrc` の方が後に読まれる（優先される）。

----
以下、とりまメモ
----

## latexmk

### latexmk options

`latexmk -help` でoption一覧表示。

| option            | description                                                  |
| ----------------- | ------------------------------------------------------------ |
| `-cd`             | サブディレクトリ以下のtexファイルをタイプセット するときに使用。<br>これを付けないと、texファイルで読み込む相対パスで書かれた画像やスタイルファイルを見つけられない。<br>例： `latexmk -cd tex/member01/member01.tex` |
| `-latex='platex'` | `platex` でタイプセット （`.latexmkrc` で`$latex = uplatex` としているとき） |
| `-e`              | perl commandが使える。<br>例： `latexmk -e $latex='platex' test.tex` |
| `-pvc`            |                                                              |
|                   |                                                              |

### latex options

`latexmk` にも渡すことができる（多分）。

| options                    | discription                                   |
| -------------------------- | --------------------------------------------- |
| `-synctex=1`               | synctex を有効にする（`*.synctex.gz` を生成） |
| `-interaction=nonstopmode` | エラーが出てもタイプセットを途中で止めない    |
| `-halt-on-error`           |                                               |
| `-file-line-error`         |                                               |
| `-shell-escape`            | shell script を有効にする                     |
|                            |                                               |



### .latexmkrc

`latexmk` の設定ファイル。perlで書かれている。

#### path

スタイルファイル（.sty）を探索する場所（パス）を追加
```perl
$ENV{'TEXINPUTS'} = './sty//;' . '../sty//;' . '../../sty//;';
```

フォントを探索する場所（パス）を追加
```perl
$ENV{'OPENTYPEFONTS'} = './fonts//;' . '../fonts//;' . '../../fonts//;';
```



### typeset

- エディタ（texshop, vscode, etc）で、サブディレクトリにあるtexファイルをlatexmkを用いてタイプセットするとき、親ディレクトリにある `.latexmkrc` は読み込まない。
  -  `.latexmkrc` はホームディレクトリ `~` に置いておくか、texファイルと同じディレクトリに置いておかなければならない。
  - latexmkのoptionで設定を与える方が楽？
- コマンドラインから `latexmk` を実行する場合は、カレントディレクトリに `.latexmkrc` があればよい。



## vscode

- カレントディレクトリ直下、サブディレクトリに関わらず、タイプセット するtexファイルと同じディレクトリにある `.latexmkrc` しか読み込まない。
  - ホームディレクトリにある `.latexmkrc` は読み込む。
- vscodeを使う場合、 `.latexmkrc` と同じ内容を `settings.json` に書いてしまった方が楽。



### .vscode/settings.json

`.vscode/settings.json` のテンプレート

```json
{
  "latex-workshop.latex.tools": [
    // for kaishi
    {
      "name": "latexmk(uplatex) for kaishi",
      "command": "latexmk",
      "args": [
        "-e", "$latex                = 'uplatex %O -synctex=1 -interaction=nonstopmode %S'",
        "-e", "$bibtex               = 'upbibtex %O %B'",
        "-e", "$biber                = 'biber %O --bblencoding=utf8 -u -U --output_safechars %B'",
        "-e", "$makeindex            = 'upmendex %O -o %D %S'",
        "-e", "$dvipdf               = 'dvipdfmx %O -o %D %S';",
        "-e", "$ENV{'TEXINPUTS'}     = './sty//;' . '../sty//;' . '../../sty//;' . './tex//;' . '../../tex//;'",
        "-e", "$ENV{'OPENTYPEFONTS'} = './fonts//;' . '../fonts//;' . '../../fonts//;'",
        "-pdfdvi",
        "%DOC%"
      ]
    },
    // ...
  ],
  "latex-workshop.latex.recipes": [
    // For kaishi (uplatex)
    {
      "name": "kaishi",
      "tools": [
        "latexmk(uplatex) for kaishi"
      ]
    },
    // ...
  ],
  "latex-workshop.latex.recipe.default": "lastUsed",
  "latex-workshop.latex.autoBuild.run": "never",
  "latex-workshop.latex.autoClean.run": "onBuilt",
  "latex-workshop.latex.clean.fileTypes": [
    "*.aux", "*.toc", "*.log", "*.dvi", "*.out.ps",
    "*.fdb_latexmk", "*.fls", // latexmk
    "*.nav", "*.snm", "*.out" // beamer
  ],
  "latex-workshop.message.update.show": false,
  "latex-workshop.message.badbox.show": false,
  "latex-workshop.message.warning.show": false,
  "latex-workshop.view.pdf.viewer": "tab",
  "latex-workshop.intellisense.package.enabled": true,
  // syntax coloring
  "files.associations": {
    "*.sty": "latex",
    ".latexmkrc": "perl"
  },
}
```

