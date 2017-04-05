# Quantitative Economics

## 回答のダウンロード
Quantitative Economics で本文／練習問題に登場する Python コードのファイルを一括してダウンロードする方法を記述しておきます。なお、このプロセスは飛ばしてもかまいません（必要に応じて、Quantitative Economics のコード部分をコピペすればよい）。
※Windows の場合、一括ダウンロードには「Source Tree」のインストールが必要となります。

### Windows用
先日やったのと同じように、"cd ***"のコマンドを使って、ファイルをダウンロードするフォルダまで移動し、"git clone https://github.com/jstac/quant-econ"と打てばよいはずなのですが、Windowsではなぜかgitをコマンドとして認識してくれません。"Quantitative Economics"に助けを求めたいところなのですが、 http://quant-econ.net/py/getting_started.html を見ても助けてくれるどころか
"Did you get an error message? Are you using Windows?"
などと煽り出す始末です。

そのため、コマンドプロンプトあるいはPowershellからcloneを作るのは諦めてSourceTreeを用いましょう。SourceTreeを起動すると左上に「新規/クローンを作成する」とあるのでそこをクリックし、「元のパス/URL」にhttps://github.com/jstac/quant-econ を、「保存先のパス」に適当なフォルダを入力(ただし、フォルダの中身は空でないといけないようです)して「クローン」を押しましょう。しばらくすると指定されたフォルダにファイルが集まっています。

### Mac用
1. ターミナルを開き「cd フォルダ名」のコマンドを使って、ファイルを保存したいフォルダまで移動
1. 「git clone https://github.com/jstac/quant-econ」をうちこむと、そのフォルダの中に quant-econ のフォルダがつくられます

## Python Part(Basic)
[An Introductory Example](AnIntroductoryExample.md)
[Python Essentials](PythonEssentials.md)
[OOP](OOP.md)
[NumPy](NumPy.md)
[MatPlotLib](MatPlotLib.md)

## Economics Part(Advanced)
[Finite Markov Chains](FiniteMarkovChains.md)
[Schelling’s Segregation Model](SchellingsSegregationModel.md)