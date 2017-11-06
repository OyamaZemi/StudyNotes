# Julia

## Tutorials

* [Julia高速チュートリアル](https://github.com/bicycle1885/Julia-Tutorial)
* [最新Juliaチュートリアル](http://nbviewer.jupyter.org/github/bicycle1885/JuliaTokyo7/blob/master/最新Juliaチュートリアル.ipynb)


## Style Guidelines

* [QuantEcon.jl](https://github.com/QuantEcon/QuantEcon.jl/blob/sl/styleguide/docs/style_guide.md)
* [johnmyleswhite/Style.jl](https://github.com/johnmyleswhite/Style.jl)


## Performance Tips

* [Performance Tips](http://docs.julialang.org/en/stable/manual/performance-tips/)
* [The Need for Speed](https://lectures.quantecon.org/jl/need_for_speed.html)
* [Juliaチューニングハンズオン](https://gist.github.com/bicycle1885/626f59ff9e0375573470)
* [コードの高速化](http://nbviewer.jupyter.org/github/IoriS/MyMatching.jl/blob/master/課題5.ipynb) (@IoriS)


## Package Management
### 開発版パッケージのインストール
Quant Econ等ではpublishされていないパッケージを用いている場合があります。その際には`Pkg.add("パッケージ名")`ではなく`Pkg.clone("パッケージが置いてあるgithubのURL")`を使ってパッケージをインストールしましょう。


## トラブルシューティング

Ijulia インストール時の失敗談
Pkg.add("IJulia")でIjuliaをインストールしようとしたところ、以下のエラーがでました。

```julia
julia> Pkg.add("IJulia")
INFO: Initializing package repository /home/9720514486/.julia/v0.4
INFO: Cloning METADATA from git://github.com/JuliaLang/METADATA.jl
ERROR: ArgumentError: '/home/9720514486/.julia/v0.4/REQUIRE' exists. remove_destination=true is required to remove 
'/home/9720514486/.julia/v0.4/REQUIRE' before moving.
in checkfor_mv_cp_cptree at file.jl:90
in init at pkg/dir.jl:63
in cd at pkg/dir.jl:28
in add at pkg.jl:23
```

これに対する対処法は、 '/home/9720514486/.julia/v0.4/REQUIRE' を消せということだったので、
ホームデュレクトリ直下にあった.juliaをターミナルで、　rm -rf .julia　と打ち込んで消して
再度、juliaを起動しjuliaのコマンドライン（ターミナルみたいなもの）から
Pkg.rm("Julia")と打ち込み
再度　Pkg.add("IJulia")と打ち込んだらうまくいきました。


そもそもエラーがでてしまった原因はPkg.add("IJulia")と打ち込んでパソコンが動作している途中に、その動作を強制終了させてしまったことです。
学校のパソコンは動作が遅いですが、しっかり待つ必要がありました。
