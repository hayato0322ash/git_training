# git_training

github flowの練習中！！大体考え方がわかってきた！！

git flow実装試験中！！


git_trainingをこれから開始するにあたって
メモを残しておく


現場での手順

イシューに対応する作業ブランチをmaster ブランチから作成する
(チームの方針によってはdevelopブランチから作成する場合もあり)


作業ブランチ名は
「feature/#1_add_name_column」のような感じで
【feature/】というプレフィックス付きで作成する
(feature/の後ろにはその改修の簡単な概要を書く)

鉄則として、ブランチ命名は「Issue番号_動詞_機能」で作成する　

※不具合を改修するブランチの場合は「fix/」というプレフィックスをつけたりする

↓

ローカル環境での作業

↓

作業が終わったら、「git status」で変更したファイルの一覧を見て
「git diff」で差分を見て
「git add -A」して
「git commit -m」して
最後に「git push origin HEAD」コマンドを実行して、GitHubのリモートブランチにpushする。

※「git push origin HEAD」とは、ブランチを指定しなくても、カレントブランチをリモートにpushすることができる。
※コミットメッセージは英語で。グーグル翻訳を使ってかつ、簡潔に

↓

pushしたブランチからプルリクエストを作成して
プルリクエスト用のテンプレが設定されている場合はそれに必要事項を記入。

↓

レビューしていただきたい方達を「Reviewers」の欄で選択する。
※この時、プルリクのコメントに「close #Issue番号(またはIssueのURL)」を入力しておいて、
プルリクがマージされた際にIssueも同時にクローズされるようにしておく。

↓

Slack等に自動でReviewersたちに通知がいく現場が多い

↓

レビューしてもらって、改修依頼があった場合は
ローカル環境で改修を加えて
「git add」
「git commit 」
「git rebase -i」でコミットを一つにまとめた上で
「git push -f origin HEAD」を実行。

※コミットはチームの方針でルールがガラッと変わったりするので、これは飽くまで"KENTAさん流"

↓

GitHub上で「LGTM」をもらったら
"プルリク画面"でマージを実行して完了

※LGTM ＝　「良さそうです」の意味。エンジニア業界の慣習




- 最近はGitHubの「approve機能」を使って
  レビュアーが誰か一人がapproveするまでは
  マージが負荷という設定にしている現場が多い。

- マージの際には大抵の現場では、リポジトリの設定で
  「Automatically delete head branches」が選択してあり、
  GitHub上の作業ブランチは自動的に削除される。

- 最近はGitHubのリポジトリの設定で
  「Allow squash merging」だけが選択されていることも多い。
  その場合マージされる際には、自動的にコミットが一つにまとめられることになっている。

- GitHubでマージが完了した後は、ローカル環境で
  「git checkout master」と
  「git pull origin master」コマンドを実行して
  masterブランチを更新しておいて、次のタスクに備えておく。


- そのブランチで作業中の内容を一旦退避させて、別のブランチで別のタスクに対応しなければならない場合も
  現場では結構よくある。こういう場合は「git stash」を使う

- 「git add」や「git commit」を取り消すための
  「git reset」もよく使う。


- コンフリクトの練習はできればやっておいた方が良い。コンフリクトの発生方法を調べて、練習してみる。