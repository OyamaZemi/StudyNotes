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

### Jupyter Notebook上でグラフが表示されない

Jupyter Notebook上で以下のようなコードを実行してもグラフが表示されないことがあります。
```
using Plots

plotlyjs()

plot(collect(1:10))
```	

これに対する対処法として, 
1. 一旦Jupyterを終了.
1. Macの場合 `~/.julia/使用しているJuliaのバージョン/IJulia`を削除.
`rm ~/.julia/v0.5/IJulia`
念のため `rm ~/.julia/v0.5/Plots` もしておくと良いかもしれません.
1. Juliaを開き先程削除したIJulia, PlotsをPkg.add()によりインストールします.

この後再びJupyterを起動して試してみると治っている場合があります.

