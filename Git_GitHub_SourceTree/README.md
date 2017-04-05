# GitHub
## Personalアカウント
Personalアカウントではプライベートレポジトリを作成できます.
本来月7$かかるPersonalアカウントが学生なら実質無料で使えます. 2016年5月以降プライベートレポジトリが無制限に作成できるようになったのでお得です.

### 作成方法
1. [GitHub Education](https://education.github.com/)にアクセスして, Request a discountをクリックし,必要な情報を入力します.　メールアドレス入力フォームには`~.ac.jp`で終わる大学のメールアドレスを入力するようにしてください. (メールアドレスを忘れた人は[MailSuite](https://ms.ecc.u-tokyo.ac.jp/cgi-bin/index.cgi)にログインすることで確認することができます)

1. 数日後にメールが届きます. acceptされた場合すでにPersonalアカウントが使用可能になっているはずです.

### 参考
* [無料でGitHubのプライベートリポジトリを使う方法（$7 Microプラン）【学生限定】](http://www.mocchiblog.com/?p=10516)

* [GitHub、有料プランの料金体系を変更、個人は月額7ドルプランのみ、組織利用はユーザー単位での課金に変更](https://codezine.jp/article/detail/9434)

## 共同開発のモデル

### 概論
* [A quick note on collaborative development models](https://help.github.com/articles/using-pull-requests#a-quick-note-on-collaborative-development-models)

### Fork&Pull Model
* [GitHub のリポジトリをForkする ①追跡編](http://lab.planetleaf.com/git/fork-repository-github-01-tracking.html)

* [GitHub のリポジトリをForkする ② Pull Request 編](http://lab.planetleaf.com/git/send-a-pull-request-from-the-repository-you-foke.html)

### Shared Repository Model
* [GitHub初心者はForkしない方のPull Requestから入門しよう](http://blog.qnyp.com/2013/05/28/pull-request-for-github-beginners/)

### 運用例
1. 共同開発するレポジトリをSourceTreeにクローンする。
1. SourceTreeの上にある「ブランチ」アイコンをクリックする。新規ブランチにブランチ名（自分の名前とか）を入力して新しいブランチを作成する。
1. 更新をコミットしてプッシュする際にプッシュするブランチを選べるので、自分が新しく作ったブランチにチェックを残し、masterブランチのチェックを外してプッシュする。
1. Githubにて「branch:master▼」というプルダウンメニューから自分が新しく作成したブランチを選択し、正しくプッシュされていることを確認する。
1. Githubのmasterブランチからプルリクエストを行い、新しく作ったブランチにて更新したことを伝える。そのプルリクエストをもとに尾山先生にmasterブランチへ自分の更新を反映してもらう。
1. masterブランチに更新が反映されれば、自分で作ったブランチは削除してもOK。

## サブモジュール

### 参考
* [サブモジュール - SourceTreeから始めるGit](http://qiita.com/icoxfog417/items/a650768dfc91b0f0df05#3-6)

## トラブルシューティング

### Git Hub からレポジトリをZipでダウンロードする際の注意点ー文字コードについて
Git Hub からレポジトリをZipでダウンロードする際にSafari等のブラウザが勝手に文字コードを変えてダウンロードしてしまい、エラーが出てしまう事があります。
（例 `UnicodeEncodeError:'utf8' codec can't decode byte 0x8d`　）
これに対する対処法の一つとして、ダウンロードしたいレポジトリをクローンする方法があります。これは、ターミナルで

git clone URL で実行されます。 URLはダウンロードしたいレポジトリのあるページのURLです。
例えば、`git clone https://github.com/oTree-org/oTree` のような感じです。
windowsの場合はgitをインストールした上で、同様にコマンドプロンプトで　`git clone URL` で実行です。

もう一つの対処法にブラウザの設定を変える方法があるのですが、まだ試していないので、どなたか試したら加筆をお願いします。
(トラブルが出たらここに書いてみんなと共有する．)

### 参考
* [SourceTree 初心者が、初心者すぎてハマったポイント](http://blog.livedoor.jp/noanoa07/archives/1981463.html)

# Source Tree
## リベースの仕方
### リベースとは
>rebase コマンドを使用すると、一方のブランチにコミットされたすべての変更をもう一方のブランチで再現することができます。
>[引用元: 3.6 Git のブランチ機能 - リベース](https://git-scm.com/book/ja/v1/Git-%E3%81%AE%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E6%A9%9F%E8%83%BD-%E3%83%AA%E3%83%99%E3%83%BC%E3%82%B9)

つまり,２つのブランチがあり片方のブランチが変更されていく時に, もう片方のブランチにその変更を取り込む事ができます.
>まずふたつのブランチ (現在いるブランチとリベース先のブランチ) の共通の先祖に移動し、現在のブランチ上の各コミットの diff を取得して一時ファイルに保存し、現在のブランチの指す先をリベース先のブランチと同じコミットに移動させ、そして先ほどの変更を順に適用していきます。

>![Qiita](https://git-scm.com/figures/18333fig0329-tn.png)
>[引用元: 3.6 Git のブランチ機能 - リベース](https://git-scm.com/book/ja/v1/Git-%E3%81%AE%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E6%A9%9F%E8%83%BD-%E3%83%AA%E3%83%99%E3%83%BC%E3%82%B9)

### 問題
QuantEcon.applicationsレポジトリをフォークしてその内容を変更しpull requestを出したものの, それが承認されるまでの間にフォーク元のレポジトリの対応する部分が新たに変更されたので, 競合が発生してpull requestが承認されなくなりました.
### 目的
自らの変更をリベースすることで競合を解決します.

### 解決手順
1. はじめにフォークしたレポジトリをフェッチして最新の状態にしておいてください.

1. まずリベースしたいブランチにダブルクリックなどでチェックアウトします.

1. リベースしたいコミット上で右クリックし```リベース```を選択します.
ここで競合が存在する等のメッセージが表示される場合,競合の解決を行います.

1. メッセージを閉じるとリベースするファイルの一覧が表示されるのですが, その一覧のうち```？```アイコンが表示されているものが既存の変更と競合しているので解決しなければなりません. 競合ファイルをクリックしてどの部分が競合しているのかも確認しておきます.

1. 今回は別の人に変更された方を残したいので```'自分の変更'を使って解決```をクリックします.
※ここで```'相手の変更'を使って解決```をクリックすると相手に変更された方が残らなくなるので注意してください.

1. メニューから```操作```をクリックし, ```リベースを続ける```をクリックします.

1. 何もなければ競合が解決した旨を報告するなどして終了です.

1. ここでエラーが発生した場合,強制プッシュを行います. プッシュボタンを押して出てくるウィンドウに強制プッシュのチェックボックスがない場合は,Source Treeの環境設定にある全般タブの下の方の```強制プッシュを許可する```にチェックを入れてください.
※強制プッシュは危険なので,問題がないことを確認したうえで行ってください.

### 参考
1. [すぐ忘れる！SourceTreeを使ったリベースとスカッシュの手順](http://qiita.com/ryounagaoka/items/7c129e98a7f81c507a61)

1. [Git のブランチ機能 - リベース](https://git-scm.com/book/ja/v1/Git-%E3%81%AE%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E6%A9%9F%E8%83%BD-%E3%83%AA%E3%83%99%E3%83%BC%E3%82%B9)

1. [[Git] 分かりやすく！mergeは「合流」、rebaseは「付け替え」!](http://nullnote.com/web/git/merge_rebase/)
