---
title: "沖縄高専ICT委員会技術継承　Git/GitHub編　#02-基礎編"
emoji: "🔥"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["git", "github"]
published: true
---
# はじめに
Hey Guys!
この度、委員長の指示で沖縄高専ICT委員会技術継承としてGit/GitHubを教えるアヤノです。
この記事は、副委員長の@IshizuShim0126と執筆しました！

第2章では、Gitの理解を目的として、最低限知っていたほうが良い操作を説明します。
演習もあるので、頑張りましょう！

@[speakerdeck](5209bc1ff932437f9076aeafeced9f64)

# バージョン管理の重要性
## 普通にバージョン管理をすると 
例えば、学校のレポートを書いているとき、以下のようにファイル名を変えて保存したことはありませんか？

```sh
例：
report.docx
report_final.docx
report_final2.docx
report_final_最新版.docx
```

この方法では、どれが本当に最新のファイルなのか分かりづらくなります。また、どこをどのように変更したのかを確認するのも大変です。さらに、友達と一緒に作業していると、「どのファイルが最新なの？」と混乱することもあります。

これがチーム開発で起こると最悪で、誰が何のファイルを追加し、どれが最新ファイルで、新しいファイルはどんな名前を付ければいいのかが分からなくなり、作業効率がかなり落ちます。

## Gitでバージョン管理をすると
Gitは、こうしたファイル管理の悩みを解決してくれる便利なツールです。Gitを使うと、次のようなことが簡単にできます。
- **変更履歴の管理**：いつ、誰が、どこを変更したのかを自動で記録できます。
- **バージョンの切り替え**：過去のバージョンに簡単に戻ることができます。間違えてもすぐに元に戻せるので安心です。
- **複数人での共同作業**：友達やチームメンバーと一緒に作業するときも、誰がどこを直したのかが一目でわかり、作業がスムーズに進みます。

このようにGitを使うと、ファイル管理のストレスから解放され、作業がもっとスムーズで安心なものになります。

# この記事で使用するGit特有の単語
この記事では、以下のgit特有の単語をいくつか使用します。

- **リポジトリ**
    - Gitでバージョン管理する「プロジェクト全体」を指します。フォルダやプロジェクトをGitで管理するための箱のようなものです。`git init` で作成できます。
- **コミット** 
    - ファイルの変更内容を「メモ書き」として記録することです。コミットを繰り返すことで、いつでも過去の状態に戻れるようになります。
- **ステージングエリア** 
    - 変更したファイルを「次のコミットに含めるかどうか」を一時的に選ぶ場所です。`git add` でステージングエリアにファイルを追加します。
- **ブランチ**
    - 作業の「分岐点」です。新しい機能を追加したり、実験的な変更をする際に使います。`git switch` でブランチの切り替えができます。
        :::message alert
        ブランチについては、今理解しなくても問題ありません。
        :::
- **HEAD**
    - 現在作業中の最新のコミットやブランチを指すポインタです。`git log` で確認できるコミットの一番上がHEADにあたります。

# Gitで主に使うコマンドの流れ
それでは、Gitでよく使うコマンドとそのイメージを説明します。

## 紹介するコマンドのイメージ
![](/images/articles/ict-git-fundamentals/nagare.png)

gitでは、基本的にはこの6つのコマンド（init, switch, status, add, commit, log）を使って、バージョン管理をします。個人的には、この6つのコマンドを理解・使用ができれば、後は調べながらでもgitを使えると考えています。

## コマンドの紹介
ここでは、先程のイラストに登場した6つのコマンド（init, switch, status, add, commit, log）の説明と例を説明します。

### git init
`git init` は、**新しいGitリポジトリを作成するコマンド**です。プロジェクトのフォルダでこのコマンドを実行すると、そのフォルダがGitでバージョン管理できるようになります。

**例：**
```bash
mkdir my_project
cd my_project
git init
```
これで `my_project` フォルダがGitの管理下に入りました。フォルダ内に `.git` という隠しフォルダが作成され、ここにすべてのバージョン管理情報が保存されます。

### git switch
`git switch` は、**作業中のブランチを切り替えるコマンド**です。ブランチとは、異なる作業内容を分けて管理するための機能です。

**例：**
```bash
git switch -c new-feature
```
`-c` オプションを使うことで、新しいブランチ new-feature を作成し、同時にそのブランチへ切り替えます。

既存のブランチに切り替える場合は：
```bash
git switch main
```
これで `main` ブランチに戻ることができます。

### git status
`git status` は、**現在のリポジトリの状態を確認するコマンド**です。ステージングされているファイル、まだステージングされていない変更、コミットされていない変更などを確認することができます。

**例：**
```bash
git status
```
これを実行すると、次のような情報が表示されます。

- 現在作業しているブランチ名
- ステージングされているファイル
- まだステージングされていない変更
- Gitで追跡されていない新しいファイル（Untracked files）

このコマンドを使うことで、どのファイルを add すべきかを確認する際に役立ちます。


### git add
`git add` は、**ファイルの変更をステージングエリアに追加するコマンド**です。ステージングエリアとは、コミットする変更を一時的に保存する場所です。

**例：**
```bash
echo "Hello World" > hello.txt
git add hello.txt
```
これで `hello.txt` の変更がステージングエリアに追加され、次のコミットで記録される準備が整いました。

すべての変更を一度に追加する場合は：
```bash
git add .
```
これでカレントディレクトリ以下のすべての変更がステージングされます。
`git add .` は便利ですが、意図しないファイルも追加されることがあるので、慣れるまでは個別にファイルを指定する方法も試してみましょう。

### git commit
`git commit` は、**ステージングエリアにある変更をリポジトリに記録するコマンド**です。コミットメッセージを付けて、どんな変更をしたのか説明します。

**例：**
```bash
git commit -m "Add hello.txt with greeting message"
```
これで `hello.txt` の変更が履歴として保存され、過去のバージョンに戻すことができるようになります。

### git log
`git log` は、**これまでのコミット履歴を確認するコマンド**です。どのような変更が、いつ、誰によって行われたかを確認できます。

**例：**
```bash
git log
```
これでコミット履歴が表示されます。見やすくするために、以下のオプションを使うこともできます。

```bash
git log --oneline
```
`--oneline` は、各コミットを1行で表示するオプションで、履歴を素早く確認したいときに便利です。

# 実際にやってみた（演習）
それでは、実際にGitのコマンドを使って基本的な操作を体験してみましょう。

## 1. Git 初期化とファイル作成
まず、簡単なメモファイルを作成し、Gitで管理を開始します。

```bash
echo "hello git" > memo.txt
git init
git add .
git commit -m "初めてのgit"  # master ブランチにコミット
```

これで `memo.txt` の内容が `master` ブランチにコミットされました。

## 2. 新しいブランチ "test" を作成して切り替え
次に、新しいブランチ `test` を作成して切り替えます。

```bash
git switch -c test
```

これで `test` ブランチに切り替わり、新しい作業を開始できます。

## 3. "test" ブランチで修正
`memo.txt` の内容を修正し、再度コミットします。

```bash
echo "hello git!!!" > memo.txt
git add .
git commit -m "!!!を追加"  # test ブランチにコミット
```

これで `test` ブランチに新しいコミットが追加されました。

## 4. 各ブランチの内容確認
実際に、各ブランチでファイルの内容がどう変わるか確認してみましょう。

```bash
# main ブランチに切り替えて確認
git switch main
type memo.txt  # 使用しているOSがwindows以外はcatに読み替える
# 期待される出力: "hello git"

# test ブランチに切り替えて確認
git switch test
type memo.txt  # 使用しているOSがwindows以外はcatに読み替える
# 期待される出力: "hello git!!!"
```

このように、ブランチごとにファイルの内容が異なることを確認でき、gitでバージョン管理が出来ました。

# その他のコマンド
他にも知っていた方が良いコマンド（stash, reset, diff, revert）を4つ紹介します。
これらのコマンドは知っていたら便利ですが、使えなくても何とかなるので、紹介だけに留めます。

## git stash
`git stash` は、**作業中の変更を一時的に退避させ、ワーキングディレクトリをクリーンな状態に戻すコマンド**です。例えば、別のブランチで作業する必要があるけど、今の変更をコミットしたくない場合に便利です。

**例：**
```bash
git stash
```
これで現在の変更が一時保存され、作業ディレクトリが元の状態に戻ります。

退避した変更を元に戻す場合：
```bash
git stash apply
```
また、退避した内容を削除する場合は：
```bash
git stash drop
```

## git reset
`git reset` は、**コミットやステージングエリアの変更を取り消すコマンド**です。誤ってコミットした内容や、ステージングした変更を戻したいときに使います。

**例：**
```bash
git reset HEAD~1
```
これは直前のコミットを取り消し、変更内容はステージングされたままになります。

ステージングエリアだけをリセットする場合：
```bash
git reset
```
これでステージングされた変更が解除されます。

## git diff
`git diff` は、**ファイルの変更内容を確認するコマンド**です。どの部分がどのように変更されたかを具体的に表示してくれます。

**例：**
```bash
git diff
```
これは、ワーキングディレクトリとステージングエリアの違いを表示します。

ステージングされた変更と最新のコミットとの差分を見る場合：
```bash
git diff --staged
```

## git revert
`git revert` は、**指定したコミットを取り消す「新しいコミット」を作成するコマンド**です。履歴を保持したまま変更を取り消せるので、安全な方法です。

**例：**
```bash
git revert <コミットID>
```
これで指定したコミットの内容を打ち消す新しいコミットが作成されます。
誤ったコミットを取り消す必要があるけど、履歴を残したいときに便利です。

# おわりに
Gitの演習、お疲れさまでした。
今回は、Gitの基礎的な操作を紹介しました。
沖縄高専ICT委員会技術継承Git/GitHub編は次章で最終回です。
今回の内容が分かっているつもりで行うので、軽い復習をお願いします。

# おまけ（Gitのコマンド、Git/GitHubのロードマップの紹介）
Gitは今回紹介したもの以外にも沢山コマンドがあるので、以下のサイトを見ながらどんなコマンドがあるのかを確認することをおすすめします。
- [Gitコマンド一覧](https://zenn.dev/zmb/articles/054ba4189244a5)
- [Git - Reference](https://git-scm.com/docs)

また、Git/GitHubを使いこなすためのロードマップもあるので、極めたい方はこちらを見てください。
- [Learn Git and GitHub](https://roadmap.sh/git-github)
