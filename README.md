# SFC卒業論文用LaTeXテンプレート

## 概要

こちらの[テンプレート](https://github.com/sasn0/thesis-overleaf-template)をベースに作った、SFC卒業論文用LaTeXテンプレートです。大元のフォーク元テンプレートは、「関連リンク」に記載しています。

主に以下のような変更を加えています。

- PDF目次に対応（`hyperref`を使用）
- 元号を令和に変更（元号を変数として任意に定義可能なよう変更）
- commit hashをフッターに追加（`gitinfo2`を使用）
- 行間をダブルスペースに変更
- 参考文献スタイルをjunsrtに変更
- 数式フォントをLatin Modernに変更

## 使い方

### テンプレートをダウンロードする
- [Releases](https://github.com/mu373/sfc-thesis-template/releases/)からダウンロードできます
- `main.pdf`はこのテンプレートをビルドしたPDFです


### PDFを書き出す
- `latexmk`で一発でPDFを作成できます。
- LaTeX Workshopを入れたVSCodeで執筆すると便利です。ファイルを保存するたびに自動でビルドしてくれて、PDFを見ながら執筆ができます。（環境構築については下に簡単に記載してあります）

### PDFのフッターにcommit hashを入れる

ページのフッターにcommitハッシュとcommit日時を入れておくと、PDF（あるいはそれを印刷したもの）を見るときに、どの時点でのコミットに対応しているものかを確認できて便利です。`gitinfo2`というLaTexパッケージを使います。

- `post-commit`というファイルを`.git/hooks/`内に置かないと、LaTeXの`gitinfo2`がコミット情報を認識してくれません
- 以下のスクリプトでセットアップが必要です。（中身をもらえればわかりますが、単純に`post-commit`を`.git/hooks/`内にコピーしているだけです）

```sh
sh ./scripts/setup.sh
```

- 提出用のPDFを生成するときには`main.tex`で以下をコメントアウトします（フッターからコミット情報が入らなくなる）

```tex
\usepackage[mark]{gitinfo2}
\renewcommand{\gitMark}{commit \gitAbbrevHash\space(\gitAuthorDate)}
```

### Overleafで使う場合
1. 自分のレポジトリに `git clone` する
2. overleafのアカウントで、`import from github` を選ぶ
3. `Menu` から、コンパイル => `LaTeX` を選ぶ
4. `Menu` から、Main Document => `main.tex` を選ぶ


### コメントを定義する
thesis.sty内で、コメントを定義することができます。

コメントを消したかったら、trueをコメントアウトして、falseのコメントアウトを外せばOKです。
```
\notestrue          %コメントoff時コメントアウト
%\notesfalse        %コメントon時コメントアウト
```

下記のようにすれば、コメントの色と名称の指定ができます。
```
\newcommand{\sassan}[1]{\colornote{red}{#1}{sassan}}
\newcommand{\harusame}[1]{\colornote{blue}{#1}{harusame}}
```


## 参考：環境構築
Mac上で、VS CodeのLaTeX Workshopを使って執筆するワークフローを想定しています。

- MacTeXのGUIなしバージョンをインストールする
```sh
brew install mactex-no-gui
sudo tlmgr update --self --all
```

- VS Codeに[LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)をインストールする
- VS Codeの設定（JSONファイル）に以下を追加する
```json
    "latex-workshop.latex.recipes": [
        {
            "name": "latexmk",
            "tools": [
                "latexmk"
            ]
        },
    ],
    "latex-workshop.latex.tools": [
        {
            "name": "latexmk",
            "command": "latexmk",
        },
    ],
    "latex-workshop.latex.clean.enabled": true,
    "latex-workshop.latex.clean.fileTypes": [
        "*.aux",
        "*.bbl",
        "*.blg",
        "*.idx",
        "*.ind",
        "*.lof",
        "*.lot",
        "*.out",
        "*.toc",
        "*.acn",
        "*.acr",
        "*.alg",
        "*.glg",
        "*.glo",
        "*.gls",
        "*.ist",
        "*.fls",
        "*.log",
        "*.fdb_latexmk",
        "*.synctex.gz",
        "_minted*",
        "*.nav",
        "*.snm",
        "*.vrb",
        "*.run.xml",
        "*.dvi",
        "*.bcf"
    ],
    "latex-workshop.view.pdf.viewer": "tab",
    "latex-workshop.latex.autoClean.run": "onBuilt",
    "workbench.activityBar.visible": false,
```

- VS Code上で`command + shift + P`して、`Build LaTeX project` `View LaTeX PDF file`するとPDFが表示されるはずです。


## ライセンス
元テンプレと同様に、私が改造した部分についてもすべての権利を放棄します。

## 関連リンク
- [@kurokobo 卒業論文用テンプレート](https://wiki.kurokobo.com/index.php?LaTeX)
- [ymrl/thesis-template](https://github.com/ymrl/thesis-template)
- [sasn0/thesis-overleaf-template](https://github.com/sasn0/thesis-overleaf-template)
- [LaTeX with VSCodeな環境を整える（Mac）](https://m12watanabe1a.hatenablog.com/entry/2019/09/30/020036)