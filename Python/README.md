# Python
プログラミング言語Pythonの使い方について解説します. Python3.x系がメインです.

[日本語版公式サイト](http://www.python.jp/)

**目次**

1. [はじめに](#はじめに)
1. [Pythonのインストール方法](#Pythonのインストール方法)
1. [Pythonコードの実行方法](#Pythonコードの実行方法)
1. [ライブラリをインストールする](#ライブラリをインストールする(pip))
1. [コーディング規約](#コーディング規約)
1. [ローカル開発環境venvの使い方](#ローカル開発環境venvの使い方)


## はじめに

Pythonはフリー・マルチプラットフォーム・オープンソースな動的な型付けの汎用プログラミング言語です. シンプルでわかりやすい文法を持ち, Webサーバから統計処理まで様々な用途に使用することが出来ます. 非常にメジャーな言語で, [Tiobe Index](http://www.tiobe.com/tiobe_index)というプログラミング言語の人気調査を見ると, JavaやC系の言語に次ぐ人気を獲得しています. GoogleやFacebookといった企業が採用していることもあり, 近年日本でも利用者が増えています.

* [Tiobe Index](http://www.tiobe.com/tiobe_index)
* [Python - Wikipedia](https://ja.wikipedia.org/wiki/Python)

Pythonは「ニシキヘビ」の意味ですが, 名前の由来は[空飛ぶモンティ・パイソン](https://ja.wikipedia.org/wiki/%E7%A9%BA%E9%A3%9B%E3%81%B6%E3%83%A2%E3%83%B3%E3%83%86%E3%82%A3%E3%83%BB%E3%83%91%E3%82%A4%E3%82%BD%E3%83%B3)だそうです.

## Pythonのインストール方法

Pythonにはたくさんのディストリビューション（方言のようなもの）が存在し, 様々なダウンロード/インストール方法があります.

また **Python2**, **Python3** という大きなバージョンの違いがあり, この2つの間には互換性がありません. **Python3の方が新しく, ゼミでは主に3系を使います**が, 未だPython3に対応していないライブラリもあるので注意が必要です.

[公式サイト](http://www.python.jp/)からもダウンロードできますが, ここでは[Anaconda](https://www.continuum.io/why-anaconda)という, 科学計算用のライブラリが最初から入っているディストリビューションを紹介します.

#### Windows OSの場合

[Anacondaのインストーラ](https://www.continuum.io/downloads)をダウンロードして使うのが良いと思います. Python3.5系を選択してください.


#### Mac OS XまたはLinuxの場合

上記のインストーラを使っても良いですが, pyenvというバージョン管理ツールが便利です. 経済学部のPCにもこれがインストールされています.

[pyenvの使い方](blob/master/Python/pyenv.md)

## Pythonコードの実行方法

Pythonで書かれたコードを実行する方法はいくつもありますが, ここでは3つを紹介します. いずれも, サンプルとして`Hello World!`と出力させてみます.

#### 1. インタラクティブモードでPythonを動かす

ターミナル（windowsならコマンドプロンプト）を起動し, 

```
python
```

と入力します. すると

```
Python 3.4.3 |Anaconda 2.3.0 (x86_64)| (default, Mar  6 2015, 12:07:41) 
[GCC 4.2.1 (Apple Inc. build 5577)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

というように, 入力待ちの状態になります. ここで`print("Hello Wold!")`とタイプして実行すると, 

```
>>> print("Hello World!")
Hello World!
>>> 
```

と出力を返し, 再び入力待ちの状態になります. Pythonを終了したい場合は

```
exit()
```

を実行します.

#### 2. Pythonファイル(.py)をターミナルで実行する

インタラクティブモードは手軽にPythonが実行できますが, ある程度長いコードを書くには不便です. そこでエディタ（メモ帳でもOK）で

```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

print("Hello World!")
```

と書いて`test.py`という名前で保存し, 

```
cd [該当のファイルのパス]
```

として, 

```
python test.py
```

を実行すれば, 

```
Hello World!
```

とターミナルが返してくれます.

#### 3. IPython Notebook(Jupyter Notebook)上でPythonを動かす

(Jupyter)[http://jupyter.org/]

Jupyter Notebook（旧名IPython Notebook）は, PythonやR, Julia, Scalaなどのプログラミング言語に対応した, 文章や図, 数式とコードを1つのNotebookにまとめることのできるツールです.

百聞は一見にしかず: [KMRのシミュレーション](http://nbviewer.jupyter.org/github/myuuuuun/KMR/blob/master/KMR.ipynb)

Anaconda環境には最初から入っています. その他の環境の場合は

```
pip install jupyter
```

でインストールできます. 起動する場合は

```
jupyter notebook
```

を実行すると, ブラウザが開き, ドキュメントが作成できるようになります.

## ライブラリをインストールする(pip)

```
pip install [ライブラリ名]
pip install --upgrade [ライブラリ名]
pip uninstall [ライブラリ名]
```

## コーディング規約
Pythonを使ってコードを書く際には、「こういう風に書きましょう」というマナー（ルール）があります。はじめのうちはそれらを守る余裕はないかもしれませんが、慣れてきたらPython のコーディング規約に従って書くようにしましょう。

代表的なコーディング規約はPEP8というものです.

たとえば

* インデントはスペース4つ
* 等号記号 = の両側にはスペースを1つずつ入れる
* ただし，関数のキーワード引数の = にはスペースを入れない (例：f(x, t=1))

などがあります。詳しくは下記のリンクから確認してください。

[PEP8](http://legacy.python.org/dev/peps/pep-0008/)
[PEP8 オンラインチェッカー](http://pep8online.com/)

幸いなことに, 多くのエディタには自動でPEP8に従うようコードを整形してくれるアドインがあります. flake8といった, コーディング規約に従っているかをチェックするPythonのライブラリも存在します.

PEP8に加えて, [Google Python スタイルガイド](http://works.surgo.jp/translation/pyguide.html) などがコーディング規約として定められる場合もあります.

## ローカル開発環境venvの使い方

```
python3 -m venv [任意の環境名]  #環境作成
source [任意の環境名]/bin/activate  #仮想環境起動

deactivate  #終了
```