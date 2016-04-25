# pyenv

Pythonのバージョン管理ツール, pyenvの説明.

公式Github: [yyuu/pyenv](https://github.com/yyuu/pyenv)

**目次**

1. [pyenvとは](#pyenvとは)
1. [pyenvの導入](#pyenvの導入)
1. [pyenvの使い方](#pyenvの使い方)
1. [pyenv環境でのライブラリのインストール](#pyenv環境でのライブラリのインストール)
1. [(補足)PATHとは](#（補足）PATHとは)

## pyenvとは
1台のPCの中で, 異なるバージョンのPythonを使い分けるためのツールです.

一口にPythonと言っても様々なディストリビューションがあり, Python2/Python3という大きなバージョンの違いだけでなく, 科学計算用の様々なモジュールが最初から揃っているAnacondaやWinPythonといったものもあります. またそれぞれに

```
2.7.3/2.7.4/3.4.3/3.4.4/anaconda3-2.3.0/anaconda3-2.4.0
```

というような複数のマイナーバージョンが存在し, 異なるPythonを使い分けたくなることがしばしばあります. そのような場面で複数のPythonを簡単に切り替えられるようにするツールがpyenvです.

#### (余談)どのpythonが実行されるか

Macには最初からPythonがインストールされており（system python）, 実行ファイルは `/usr/bin/` にあります. 他にもhomebrewでPythonをインストールしたことがあれば `/usr/local/bin/`などにも入っているはずです.

1台のPCに複数のPythonがインストールされている場合, どれが使われるかはコマンドサーチパス（以下パス, PATHと書く）の記述順序によります -> [PATHとは](#path)

現在使われているPythonの実行ファイルがどこにあるかを確認するには, ターミナルを開き

```
which python
```

というコマンドを実行します. すると 

```
/usr/bin/python
```

というように, 実行ファイルの場所を返してくれます（PATHに追加されているディレクトリの中に実行可能なpythonが存在しない場合は, 何も返ってきません）

結局, どのPythonが実行されるかを制御するためにはパスを書き換えることが必要になります. しかしそれを毎度毎度やるのはめんどうくさい. そこでパスの書き換えをコマンド一つで実行してくれるのがpyenvです.

## pyenvの導入

経済学部のPCには, 既にインストールされています.

他のPCにインストールしたい場合は

* Github: [yyuu/pyenv](https://github.com/yyuu/pyenv)

に全てが書いてあります. なおMacでHomebrewがインストールされていれば

```
brew update
brew install pyenv
```

で直ちにインストールできます（参考: [MacにHomebrewをインストールする](http://qiita.com/_daisuke/items/d3b2477d15ed2611a058)）.

```
pyenv
```

というコマンドを実行し, 

```
pyenv 20150326
Usage: pyenv <command> [<args>]

Some useful pyenv commands are:
   commands    List all available pyenv commands
   local       Set or show the local application-specific Python version
   global      Set or show the global Python version
   shell       Set or show the shell-specific Python version
   install     Install a Python version using python-build
   uninstall   Uninstall a specific Python version
   rehash      Rehash pyenv shims (run this after installing executables)
   version     Show the current Python version and its origin
   versions    List all Python versions available to pyenv
   which       Display the full path to an executable
   whence      List all Python versions that contain the given executable

See 'pyenv help <command>' for information on a specific command.
For full documentation, see: https://github.com/yyuu/pyenv#readme
```

というようなヘルプが表示されれば, インストール成功です. もし

```
pyenv: command not found
```

と表示された場合は, パスの設定が上手く出来ていません. シェルにbashを使っている場合（特に設定を変えていなければこれです）, ターミナルで

```
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
exec $SHELL
```

を順に実行してください. `pyenv`を実行し, 先ほどのようなヘルプが表示されればインストール成功です. これでも失敗した場合は, 直接`~/.bash_profile`（通常隠しファイルになっている）を編集してみてください.

## pyenvの使い方

代表的なコマンド

* ヘルプ

```
pyenv  #ヘルプを表示
```

* バージョンをインストール

```
pyenv install --list          #現在pyenvでインストール可能な全てのバージョンを表示
pyenv install [バージョン名]     #該当のバージョンをインストール
pyenv uninstall [バージョン名]   #該当のバージョンをアンインストール
```

* バージョンを確認

```
pyenv versions   #現在pyenv環境にインストールされている全てのバージョンを表示
pyenv version    #現在シェルで実行されているpythonのバージョンを表示
pyenv local      #現在のディレクトリに設定されているpythonのバージョンを表示
pyenv global     #PC全体で標準に設定されているpythonのバージョンを表示
```

* バージョンを設定

```
pyenv shell [バージョン名]    #現在シェルで実行されているpythonのバージョンを設定
pyenv local [バージョン名]    #現在のディレクトリに設定されているpythonのバージョンを設定
pyenv global [バージョン名]   #PC全体で標準のpythonのバージョンを設定
```

とりあえずanaconda3の最新バージョン（2016/4/24現在: `anaconda3-2.4.0`）をインストールするのが良いと思います. そのためには, 

```
pyenv install --list  #インストール可能なバージョンを確認
pyenv install anaconda3-2.4.0  #最新バージョンのanacondaをインストール
pyenv global anaconda3-2.4.0  #anacondaを標準のpythonに設定
```

とすればよいです. なお, 大学のPCには既にanaconda3がインストールされています.

```
which python
```

というコマンドを実行し, 

```
/Users/[username]/.pyenv/shims/python
```

などと表示されれば, 正常にpyenvのpythonが優先して使用できるようになっています.

## pyenv環境でのライブラリのインストール

pipが既にインストールされているので, 通常通り

```
pip install quantecon
```

などと実行すれば, それぞれのディストリビューション毎にライブラリがインストールされます.

pipについての詳細は: ライブラリのインストール

経済学部のPCに最初から入っているsystem pythonやanacondaでは, パーミッションの都合で新しいライブラリがインストール出来ない可能性があります. そのようなエラーが出た場合は, 別にディストリビューションをインストールし, その環境で再度インストールしてみてください.

## （補足）PATHとは

パスとは, 一般には

```
/Users/myuuuuun/Documents/hoge.txt
```

のような, フォルダやファイルの場所を示すための表記です.

しかし「パスを通す」といった時のパスは, 正確にはコマンドサーチパスのことで, 「シェルがコマンド実行ファイルを探しに行くディレクトリ」のことです. ターミナルを開き

```
echo $PATH
```

とすると, 

```
/usr/local/bin:/usr/bin:/bin:/usr/sbin
```

などと表示され, これがコマンドサーチパスになります. パスの細かい話は, 下のリンクを参照してください.

PATHの詳細:

* [UNIX入門 - Mac Wiki](http://macwiki.osdn.jp/wiki/index.php/UNIX%E5%85%A5%E9%96%80)
* [PATHを通すとは？(Mac OS X)](http://qiita.com/soarflat/items/09be6ab9cd91d366bf71)
* [PATHを通すために環境変数の設定を理解する(Mac OS X)](http://qiita.com/soarflat/items/d5015bec37f8a8254380)

使用しているシェルがbashの場合（何も設定を変えていなければこれです. 使用中のシェルは`echo $SHELL`で確認できます）, ユーザー用のPATHは

```
.bash_profile
```

に記述します. 通常隠しファイルになっているので, ターミナル上で編集するか, 

* [Macの隠しファイルや隠しフォルダを表示する裏技](http://inforati.jp/apple/mac-tips-techniques/system-hints/how-to-show-hidden-file-or-folder-of-macos.html)

を参考に, 隠しファイルを表示してエディタなどで編集してください.

