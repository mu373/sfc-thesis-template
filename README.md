# SFC卒業論文用LaTeXテンプレート

こちらの[テンプレート](https://github.com/sasn0/thesis-overleaf-template)をベースに作った、SFC卒業論文用LaTeXテンプレートです。元となっているテンプレートは、関連リンクに記載しています。

以下のような変更を加えています。

- PDF目次に対応（`hyperref`を使用）
- 元号を令和に変更（変数として任意に定義可能なよう変更）
- commit hashをフッターに追加（`gitinfo2`を使用）
- 行間をダブルスペースに変更
- 参考文献スタイルをjunsrtに変更
- 数式フォントをLatin Modernに変更

## 使い方

### PDFのフッターにcommit hashを入れる

ページのフッターにcommitハッシュとcommit日時を入れておくと、PDF（あるいはそれを印刷したもの）を見るときに、どの時点でのコミットに対応しているものかを確認できて便利。`gitinfo2`というLaTexパッケージを使うことで、これを実現できる。

- `post-commit`というファイルを`.git/hooks/`内に置かないと、LaTeXの`gitinfo2`がコミット情報を認識してくれない
- 以下のスクリプトでセットアップができる

```sh
sh ./scripts/setup.sh
```

- 提出用のPDFを生成するときには`main.tex`で以下をコメントアウトする（フッターからコミット情報が入らなくなる）

```tex
\usepackage[mark]{gitinfo2}
\renewcommand{\gitMark}{commit \gitAbbrevHash\space(\gitAuthorDate)}
```

### Overleafで使う場合
1. 自分のレポジトリに `git clone` する
2. overleafのアカウントで、`import from github` を選ぶ
3. `Menu` から、コンパイル => `LaTeX` を選ぶ
4. `Menu` から、Main Document => `main.tex` を選ぶ


### コメントを定義
thesis.styをちょっといじったりすると、コメント定義ができる。

コメントを消したかったら、trueをコメントアウトして、falseのコメントアウトを外せばok。
```
\notestrue          %コメントoff時コメントアウト
%\notesfalse        %コメントon時コメントアウト
```

下記のようにすれば、コメントの色と名称の指定ができる。
```
\newcommand{\sassan}[1]{\colornote{red}{#1}{sassan}}
\newcommand{\harusame}[1]{\colornote{blue}{#1}{harusame}}
```

## ライセンス
>オリジナルのテンプレートについては（おそらく） @kurokobo に著作権があります。
>私が改造した部分についてはすべての権利を放棄いたします。

元テンプレにこうありますが、私が手を入れた箇所についても、すべての権利を放棄致します。

## 関連リンク
- [@kurokobo 卒業論文用テンプレート](https://wiki.kurokobo.com/index.php?LaTeX)
- [ymrl/thesis-template](https://github.com/ymrl/thesis-template)
- [sasn0/thesis-overleaf-template](https://github.com/sasn0/thesis-overleaf-template)