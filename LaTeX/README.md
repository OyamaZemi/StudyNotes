# LaTeX
## 日本語化
### TeXShopで日本語を使えるようにする
大学のMacにインストールされているTeXShopは初期状態では日本語を使うとエラーになるので,以下の手順で日本語化します.

1. メニューから環境設定を開き, 画面左下の設定プロファイル( 英語版だとSettings Profile(?) )からpTeX(ptex2pdf)を選択します.

1. OKを押し, 試しにjarticle文書クラスで日本語を入力して, コンパイルできるか確認してみてください.

### 参考
[MacTeX - TeXShop で 日本語を使う方法](http://medemanabu.net/latex/mactex-texshop-ptex-platex/)


## 書式
### 注意点
数学記号などは記号によりローマン体やイタリック体が決まっているので, 以下のurlを参考にしてください.

[由緒正しいTeX入力法 - 東北大学大学院理学研究科数学専攻](https://www.math.tohoku.ac.jp/tmj/oda_tex.pdf)

## コマンド
### コマンド一覧
[LaTeXコマンドシート一覧](http://www002.upp.so-net.ne.jp/latex/kigou_all.html)

## レポート用テンプレート
### 簡易版テンプレ
```
\documentclass[11pt]{jsarticle}

\begin{document}

\begin{center}
{\large \bf 宿題　答案}
\end{center}

\begin{flushright}
名前 : ** **{\footnote{E-mail: ****@*mail.com}}
\end{flushright}

\bigskip

\textbf{問題 1.}
\begin{math}
\end{math}
\begin{eqnarray}
\end{eqnarray}
\bigskip

\textbf{問題 2.}
\begin{math}
\end{math}
\begin{eqnarray*}
\end{eqnarray*}

\end{document}```
