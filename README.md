# Github Tutorial

## 目次
- [はじめに](#はじめに)
- [gitの環境構築](#gitの環境構築)
- [リモートリポジトリの作成](#リモートリポジトリの作成)
- [ローカルリポジトリを構築](#ローカルリポジトリを構築)
- [ブランチの作成](#ブランチの作成)
- [ファイルの中身を変更](#ファイルの中身を変更)
- [リモートリポジトリに送信](#リモートリポジトリに送信)
- [リモートリポジトリをローカルリポジトリに反映](#リモートリポジトリをローカルリポジトリに反映)
- [補足](#補足)

---
## はじめに
このチュートリアルは[超ざっくりとgitについて学ぶ](https://www.slideshare.net/mnemonic1/git-156355957)の実践編となるため、まずは資料を一読しておくことを推奨します。
また、このチュートリアルはGithubのアカウントが作成してあることが前提となっております。まだアカウントを作成していない場合は[このサイト](https://qiita.com/okumurakengo/items/848f7177765cf25fcde0)を参考にアカウントを作成してください。

---
## gitの環境構築
まずはローカルPCでgitを使える状態にします。


```
# gitがインストールされているか確認

$ git version
git version <gitのバージョン>
```
gitのバージョンが表示されればすでにgitがインストールされています。
gitがインストールされていなければ[ここ](https://git-scm.com/downloads)からインストールしましょう。
インストールが完了したらgitの設定をします。下記のコマンドでgitの自分のユーザを登録しましょう。
```
$ git config --global user.name "<自分のユーザ名>"
```

```
$ git config --global user.email "<自分のメールアドレス>"
```

これでgitが使える状態になりました。

次に、githubにリモート環境からssh接続できるようにします。[ここ](https://qiita.com/shizuma/items/2b2f873a0034839e47ce)を参照してsshの設定を行ってください。

---
## リモートリポジトリの作成
まず初めに、自分のGithubアカウントで使うリモートリポジトリを作成します。
このチュートリアルでは、[このリポジトリ](https://github.com/collabodesignlab/GithubTutorial/)を自分用に複製して使います。

Gitでは、他人のリポジトリを複製することを fork(フォーク) と言います。では、さっそくforkしましょう。
ページの右上部にあるforkというボタンをクリックします。
すると自分のGithubアカウントのページに行くと、GithubTutorialというリポジトリが作成されているはずです。
これで、自分用のリモートリポジトリが作成できました。
(この説明ページは自分のリモートリポジトリからでも見ることができます)

---
## ローカルリポジトリを構築

先ほど作成したリモートリポジトリをダウンロードしてきて、ローカルリポジトリを構築します。
ローカルPCにリポジトリをダウンロードする操作を clone(クローン) と言います。では、さっそくクローンしましょう。
```
# リポジトリのクローン

$ git clone git@github.com:<自分のGithubアカウントのユーザID>/GithubTutorial.git
```

もし指定した場所にクローンしたい場合は、下記のコマンドでクローン先のディレクトリを指定してください。

```
$ git clone git@github.com:<自分のGithubアカウントのユーザID>/GithubTutorial.git <クローン先のディレクトリ>
```

クローンしたらちゃんとリポジトリがあるか確認し、リポジトリ(ディレクトリ)に移動しましょう。

```
# リポジトリの中身を確認

$ ls
GithubTutorial

$ cd GithubTutorial
$ ls
README.md               src
```
これでリポジトリの準備ができました。

---
## ブランチの作成

まず、ローカルリポジトリの状態を確認します

```
# リポジトリの状態を確認

$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
``` 

「ファイルの変更が直接 Master に反映する」ということが書かれています。複数人で作業している場合、masterを直接変更すると競合してしまうので、変更作業を行うブランチを作成して、そこで変更を行いましょう。

まず、現在のブランチを確認します。
```
# ブランチの確認

$ git branch 
* master
```
*マークがついてるブランチが現在いるブランチです。この結果から、今はmasterブランチにいることがわかります。
では、新しくブランチを作成しましょう。

```
# ブランチの作成

$ git branch <ブランチ名>
```

```
# ブランチの確認

$ git branch
* master
  <作成したブランチ>
```

新しく作成したブランチに移動します

```
# ブランチの移動
$ git checkout <作成したブランチ>
```

```
# 現在のブランチを確認

$ git branch
master
* <作成したブランチ>
```

これで、新しく作成したブランチに移動することができました。

---
## ファイルの変更を記録

では早速ファイルの中身を変更してみましょう。

このチュートリアルでは 
[src/main.py](src/main.py) 
または 
[src/main.c](src/main.c)
を変更していきます。

このチュートリアルでは[src/main.py](src/main.py)を変更した際の記述をしていますが、
[src/main.c](src/main.c)でも操作は変わりません。
ファイルを変更したら、その変更をローカルリポジトリに記録します。
まずは変更したファイルを下記のコマンドで指定します。

```
# ファイルの追加

$ git add -p src/main.py
```

次に変更内容をローカルリポジトリに反映します。
```
# 変更の記録

$ git commit -m "<ここに変更した内容を書く>"
```
これで、ローカルリポジトリに変更を反映することができました。

1. ファイルの中身を変更
2. git addで変更を記録するファイルを指定
3. git commitでローカルリポジトリに反映

この操作を繰り返すことで自分の行った変更を記録していきます。

---
## リモートリポジトリに送信

では、最後に自分の行った変更をmasterに反映します。つまり、他の人が自分の変更したファイルを使えるようにします。

まず最初に下記コマンドでローカルリポジトリの内容をリモートリポジトリに送信します。
```
# リモートリポジトリに送信

git push -u origin <作成したブランチ>
```
これで、リモートリポジトリの<作成したブランチ>に変更が反映されました。

---
## 作成したブランチをmasterにマージ

上記で行なった変更を、リモートのmasterブランチに反映します。
まず自分のリポジトリのページをブラウザから開きます(このページの上部に行けばOK)
すると、Compare & pull requestというボタンが出現してるのでクリックします。
すると、open pull requestというページに行くので、masterにマージする準備をします。ここで「Able to merge」と表示されていれば、マージすることができます。Create pull requestからpull requestを作成します。次のページでmergeをクリックするとマージ完了です。マージが完了したらDelete branchをクリックして作成したブランチを削除しましょう。

---
## リモートリポジトリをローカルリポジトリに反映
上記の操作でリモートリポジトリのmasterを更新することができました。しかし、ローカルリポジトリのmasterは最初の状態のままです。最後にリモートリポジトリの内容をローカルリポジトリに反映します。
まず、現在のブランチをmasterに変更しましょう。
現在いるブランチを確認します。
```
# ブランチの確認

$ git branch
  master
* <作成したブランチ>

# ブランチの移動

$ git checkout master
Swittched to branch 'master'

# ブランチの確認

$ git branch
* master
  <作成したブランチ>
```

この状態で[src/main.py](src/main.py)の中身をみてみると、最初の状態(変更前)に戻っているはずです。
では、リモートリポジトリのmasterをローカルリポジトリに反映しましょう。
```
# ローカルリポジトリを最新の状態にする

$ git pull origin master
```
これで再度src/main.pyを見てみると中身が変更されているはずです。ローカルも無事更新したので、不必要なブランチは削除しておきましょう。
```
# ブランチの削除

$ git branch -D <作成したブランチ> 
```
以上がgithubを使ったバージョン管理の流れになります。

---
## 補足
他人に見られたくないファイルは[.gitignore](.gitignore)に記載してaddできないようにする必要があります。
```
# .gitignore

.DS_Store
.vscode
```

### 使わない方がいいコマンド
```
# 全ファイルの追加

git add .
git add --all
```
共有してはいけないファイルを共有するリスクがあるため(パスワードなど)

---
## 参考サイト
- [GitHubアカウント作成方法](https://qiita.com/okumurakengo/items/848f7177765cf25fcde0)
- [GitHubでssh接続する手順 公開鍵・秘密鍵の生成から ](https://qiita.com/shizuma/items/2b2f873a0034839e47ce)
- [サルでもわかるGit入門](https://backlog.com/ja/git-tutorial/)
- [Gitはじめの一歩](https://www.slideshare.net/ihcomega/git-57454868)
