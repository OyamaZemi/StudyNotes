# Jupyter Notebook

## Tips

### Jupyterのフォント・デザインを変えたい.

以下の方法でAtomのようなスタイルに変えることができます.

1. `pip install jupyterthemes`
1. `jt -t onedork`

他に変えられるテーマは`jt -l`で表示できます.

#### 参考

[Jupyter のテーマを変える](http://qiita.com/mkisono/items/b77f8a9502c23a3dc610)
[Google検索](https://www.google.co.jp/search?q=nbviewer+%E3%83%95%E3%82%A9%E3%83%B3%E3%83%88+%E5%A4%89%E6%9B%B4&rlz=1C5CHFA_enJP579JP579&oq=nbviewer+%E3%83%95%E3%82%A9%E3%83%B3%E3%83%88%E3%80%80%E5%A4%89%E6%9B%B4&aqs=chrome..69i57.4511j0j4&sourceid=chrome&ie=UTF-8#q=jupyter+%E3%83%95%E3%82%A9%E3%83%B3%E3%83%88+%E5%A4%89%E6%9B%B4)

## トラブルシューティング

### nbviewerで更新が反映されない.

Githubに新しいコミットをプッシュしても,
[nbviewer](http://nbviewer.jupyter.org/)で更新がすぐに反映されない場合があります.

原因は, 一度nbviewerにurlを渡した際にnbviewer側でキャッシュが作られてしまうことです. 10分ほどで更新が反映されるようですが, すぐに反映したい場合には以下の方法が有効です.

1. nbviewerから出力されたurlをコピー.
1. コピーしたurlの最後に`?flush_cache=true`を追加.

`http://nbviewer.jupyter.org/github/user/repository/blob/master/ipynb.ipynb?flush_cache=true`


#### 参考

[nbviewer faq](http://nbviewer.jupyter.org/faq#i-want-to-removeupdate-a-notebook-from-notebook-viewer)

### nbviewer上でグラフが表示されない

nbviewer上でPlotsライブラリのplotlyjsバックエンドを用いてプロットした図が表示されないことがあります.
(Github上で表示されないのは仕様です.)

<h4 id="cause">原因</h4>

1.
```julia
using Plots
plotlyjs()
```
とした際にplotlyjsのロードに失敗している.

2. plotlyjsを一度ロードした後に, ロードしたセルを消してしまっている.

のどちらか(たぶん後者)だと考えられます.

`plotlyjs()`関数は, plotlyjsのスクリプトをセルに埋め込む関数で, そのセルがないと`plot()`を呼び出したInセルに続くOutセル内のスクリプトが内部でエラーを起こしてしまいます.

また,`plotlyjs()`関数は内部で既に自らが呼ばれているか判断するようです. Runnning中にまた`plotlyjs()`が呼ばれた場合,再びplotlyjsを読み込むことはありません. つまり, Running中にはじめに読み込んだ`plotlyjs()`を含むセルを削除して, また別のセルで`plotlyjs()`と書いて実行しても, 正常にplotlyjsの読み込みができません. セルを削除した直後にプロットをしても表示されますが, Notebookを終了して再び開くとplotlyjsのスクリプトが保存されていないために図が表示されなくなります. また, この状態のNotebookをアップロードしてもnbviewerでは図が表示されません.

<h4 id="solution">解決策</h4>

1. 一度Notebookをシャットダウンしてもう一度開き, どこかのセルで`plotlyjs()`を呼ぶ. (何処かのセルで読み込んでいれば良いようです.)
```julia
using Plots
plotlyjs()
```
これをプッシュすればnbviewerで再び図が表示されるはずです.

2. シャットダウンしたくない場合には, PlotlyJSライブラリの`init_notebook()`関数を呼ぶ.
`init_notebook()`関数はplotlyを読み込む関数で, 引数が強制的にplotlyjsを読み込むかのオプションなので, 以下のようにします.
```julia
using PlotlyJS.init_notebook
init_notebook(true)
```
その後表示したい図を再読込してください.

### ローカルのJupyter Notebook上でグラフが表示されない

Jupyter Notebook上でPlotsライブラリのplotlyjsバックエンドによるプロットが表示されないことがあります.

原因は[上記](#cause)と同じです.

解決策は[上記](#solution)一番目の方法を取ったあとにNotebookをシャットダウンしてもう一度開くことです.
(Jupyter Notebookを終了する必要はありません.)
