---
marp: true
paginate: true
theme: git
# header: 'Git勉強会 - 基本コマンド ＆ ハンズオン'
# footer: '![width:100](../../marp-themes/logo.png)'
---

# Git 勉強会 2 日目

〜基本コマンド ＆ ハンズオン ①〜
2022/03/25

---

## 2 日目アジェンダ（今日はこっち）

- Git 基本コマンド ① 〜個人開発編〜
  - init
  - clone
  - switch (checkout)
  - remote
  - branch
  - mv
  - rm
  - status
  - add
  - commit
  - push
  - log
  - diff
  - config

---

## 3 日目アジェンダ

- Git 基本コマンド ② 〜チーム開発編〜
  - fetch
  - merge
  - rebase
  - pull
  - stash
  - restore (checkout)
  - reset
  - revert
  - cherry-pick
  - blame
  - tag
  - reflog

---

## スライドの基本構成

### Git サブコマンド名（ex. clone）

#### 機能

- コマンドの役割・機能の説明

#### ユースケース

- どんなときに使うか（逆引き用）

#### コマンド例

- よく使うコマンドの例

#### イメージ

- 内部構造を理解するため図で説明

#### 参考

- 公式リファレンス + 分かりやすい記事

---

### init

#### 機能

- Git ローカルリポジトリを作成する
  - `.git` ディレクトリ（フォルダ）が作成される

#### ユースケース

- Git でバージョン管理を始めたい

#### コマンド例

```bash
$ git init
```

---

#### イメージ

#### 参考

- [git-init – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-init/)

---

### clone

#### 機能

- リポジトリのクローンを作成する

#### ユースケース

- 既に存在するリモートリポジトリ（GitHub/GitLab）のソースコードをローカルに複製したい

#### 主なオプション

- `-b | --branch`: 複製したいブランチを指定する

#### コマンド例

```bash
$ git clone <リモートリポジトリの URL>
$ git clone <リモートリポジトリの URL> -b <ブランチ>
```

---

#### イメージ

#### 参考

- [git-clone – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-clone/)

---

### switch (checkout) # TODO: branch の前後に移動する？

#### 機能

- 作業ツリーを異なるブランチに切り替える

#### ユースケース

- 既に存在するブランチに移動したい
- 新しいブランチを作成したい

#### 主なオプション

- `-c | --create`: ブランチを新規作成して切り替え

#### コマンド例

```bash
$ git switch <ブランチ>  # git checkout <ブランチ> と同じ
$ git switch -c <ブランチ>  # git checkout -b <ブランチ> と同じ
```

#### 備考

- switch は Git バージョン 2.23.0 でリリース (2019/08/16)
- checkout は複数の役割を兼ね備えてしまっているため、こちらの方が理解しやすい

---

#### イメージ

#### 参考

- [git-switch – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-switch/)
- [git checkout の代替としてリリースされた git switch と git restore](https://kakakakakku.hatenablog.com/entry/2020/04/08/151627)

---

### remote

#### 機能

- リモートリポジトリを関連付けする

#### ユースケース

- リモートリポジトリ（GitHub / GitLab）を登録（削除）したい
- リモートリポジトリの名前と場所（URL）を確認したい
  - Fork したリポジトリなど、リモートリポジトリが複数ある場合に便利

#### 主なオプション

- `-v | --verbose`: 詳細を表示

#### コマンド例

```bash
$ git remote add origin <リモートリポジトリのURL>
$ git remote -v
$ git remote remove <リモートリポジトリのURL>
```

---

#### イメージ

#### 参考

- [git-remote Documentation](https://git-scm.com/docs/git-remote)
- [【 git remote 】コマンド（基礎編）――リモートリポジトリを追加、削除する](https://atmarkit.itmedia.co.jp/ait/articles/2005/08/news017.html)

---

### branch

#### 機能

- ブランチを作成、削除、一覧表示する

#### ユースケース

- ローカルリポジトリにあるブランチを確認したい
- ローカルリポジトリにあるブランチの名前を変えたい
- ローカルリポジトリにあるブランチを削除したい

#### 主なオプション

- `-a | --all`: リモートブランチを含んだブランチの一覧を表示
- `-m | --move`: 現在チェックアウトしているブランチ名を指定したブランチ名で変更
- `-d | --delete`: 指定したブランチを削除（`-D で強制削除）

#### コマンド例

```bash
$ git branch -a # ローカルとリモートにあるブランチ一覧を表示
$ git branch <ブランチ名> # ブランチを作成
$ git switch <ブランチ名>
$ git branch -m <変更後のブランチ名>  # 今いるブランチ名を変更
$ git branch -d <ブランチ名>  # 指定したブランチを削除。-D で強制削除
```

---

#### イメージ

#### 参考

- [git-branch – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-branch/)
- [git branch コマンド - Qiita](https://qiita.com/chihiro/items/e178e45a7fd5a2fb4599)

---

### mv

#### 機能

- ファイルやディレクトリの名前を変更し、インデックスに反映する

#### ユースケース

- Git 管理しているファイルの名前を変更したい

#### コマンド例

```bash
$ git mv <変更前のファイル名> <変更後のファイル名>  # ファイル名を変更し、git にも変更を反映
```

#### 備考

- mv コマンドでファイル名を変更しても、その後 git add, git rm をすれば同じ挙動になる

```bash
$ mv <変更前のファイル名> <変更後のファイル名>
$ git add <変更後のファイル名>
$ git rm <変更前のファイル名>
```

---

#### イメージ

#### 参考

- [git-mv – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-mv/)
- [Git で管理しているファイルのリネームを git mv でなく mv してしまったときにどうなるのか調べてみた - Qiita](https://qiita.com/zonkyy/items/7705844c5e255b8fa3ae)

---

### rm

#### 機能

- ファイルを削除し、インデックスに反映する

#### ユースケース

- Git 管理しているファイルを削除したい
- `.gitignore` ファイルを編集したけど反映されない

#### よくあるオプション

- `-r`: 先頭のディレクトリが指定されている場合、ディレクトリ以下にあるファイルも再帰的に削除
- `--cached`: インデックスからのみ削除（ワークツリーにあるファイル自体は削除されず、Git 管理のみ止める）

#### コマンド例

```bash
$ git rm <ファイル名> # 指定したファイルを削除（Git 管理も止める）
$ git rm -r --cached .  # ファイル全体キャッシュ削除
```

#### 備考

- rm コマンドでファイル名を変更しても、その後 git add をすれば同じ挙動になる

---

#### イメージ

#### 参考

- [git-rm – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-rm/)
- [【Git 初心者入門】いちいちステージングエリアに add しなくても削除できる git rm](https://hirocorpblog.com/git-rm/)
- [.gitignore に記載したのに反映されない件 - Qiita](https://qiita.com/fuwamaki/items/3ed021163e50beab7154)

---

### status

#### 機能

- ワークツリーにあるファイルの状態を表示する

#### ユースケース

- どのファイルを変更したのか、add, commit 済かどうかを知りたい
- コンフリクトしたのでどうすればいいか知りたい
- よく分からないけどエラーになったから対処方法を知りたい

#### 主なオプション

- `-s | --short`: 短い形式で表示

#### コマンド例

```bash
$ git status
$ git status -s
```

---

#### イメージ

#### 参考

- [git-status – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-status/)
- [git status -s でちょっと幸せになれる - Qiita](https://qiita.com/tommy_aka_jps/items/af536a7c20747f99aa42)

---

### add

#### 機能

- ファイルをインデックスに追加（ステージング）する（コミットの対象にする）

#### ユースケース

- 変更したファイルの一部をコミットしたい // TODO: もっといい表現がありそう
- コンフリクトを解決したファイルをコンフリクト解決済の状態に変更したい

#### 主なオプション

- `-p | --patch`: ファイル内の任意の変更行のみインデックスに追加

#### コマンド例

```bash
$ git add ./src/index.html  # ./src/index.html のみインデックスに追加
$ git add ./src/  # ./src ディレクトリ以下の全てのファイルをインデックスに追加
$ git add .  # 変更済の全てのファイルをインデックスに追加
$ git add -p ./src/index.html  # ./src/index.html の一部の変更行をインデックスに追加（インタラクティブモードで選択する）
```

---

#### イメージ

#### 参考

- [git-add – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-add/)
- [【 git add 】コマンド――変更内容をインデックスに追加してコミット対象にする](https://atmarkit.itmedia.co.jp/ait/articles/2003/13/news031.html)
- [git add -p 使ってますか？](https://qiita.com/cotton_desu/items/bf08ac57d59b37dd5188)

---

### commit

#### 機能

- インデックスに追加した変更をリポジトリに記録する

#### ユースケース

- 変更した内容を記録（コミット）したい
- 直前のコミットメッセージを修正したい

#### 主なオプション

- `-m | --message`: コミットと同時にコミットメッセージを記録する

#### コマンド例

```bash
$ git commit
$ git commit -m "<メッセージ>"
$ git commit --amend -m "<修正後のメッセージ>"
```

#### 備考

- 2 つ以上前のコミットを修正したい場合は `git rebase -i` を利用する

---

#### イメージ

#### 参考

- [git-commit – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-commit/)
- [コミットの修正には git commit --amend が便利](https://tech-blog.rakus.co.jp/entry/20191113/git)

---

### push

#### 機能

- ローカルリポジトリの変更内容をリモートリポジトリに送信する

#### ユースケース

- ローカルリポジトリに記録した内容をリモートリポジトリに反映したい

#### 主なオプション

- `-u | --set-upstream`: 上流ブランチを設定する
- `-f | --force`: プッシュを強制する **（非推奨）**
- `--force-with-lease`: プッシュを強制する **（リモートと比較してローカルが最新のときだけ成功する）**

#### コマンド例

```bash
$ git push -u origin <ブランチ名>  # 上流ブランチを設定
$ git push origin <ブランチ名>  # 上流ブランチが設定されている状態なら git push でも可
$ git push --force-with-lease origin  <ブランチ名> # 強制プッシュ
```

#### 備考

- 強制プッシュは過去のコミットを上書きする高リスクコマンド。極力使わない
- 強制プッシュが発生しない運用にする。設定で保護する。どうしてもプッシュしないといけない場合はチームメンバーに確認したうえで `--force-with-lease` で強制プッシュする

---

#### イメージ

#### 参考

- [git-push – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-push/)
- [git push コマンドの使い方と、主要オプションまとめ](https://www-creators.com/archives/1472)
- [Git 用語：上流ブランチとは？](https://www-creators.com/archives/4931)
- [git push -f をやめて --force-with-lease を使おう - Qiita](https://qiita.com/wMETAw/items/5f47dcc7cf57af8e449f)

---

### log

#### 機能

- コミット時のログを表示する

#### ユースケース

- コミット履歴を確認したい
  - 自分のコミットが成功したか確認したい
  - 他の人がこのブランチでどのようなコミットをしてきたのか知りたい

#### 主なオプション

- `--oneline`: 各コミットのログを 1 行で表示
- `--no-merges`: マージコミットを除いて表示

#### コマンド例

```bash
$ git log
$ git log --oneline
# 以下は応用例（エイリアスに登録しておくと便利）
$ git log --graph --pretty=format:'%x09%C(auto) %h %Cgreen %ar %Creset%x09by"%C(cyan ul)%an%Creset" %x09%C(auto)%s %d'
```

// TODO: 文字列部分の色を変える

---

#### イメージ

#### 参考

- [git-log – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-log/)
- [git log のオプションと綺麗にツリー表示するためのエイリアス - Qiita](https://qiita.com/kawasaki_dev/items/41afaafe477b877b5b73)

---

### diff

#### 機能

- コミット同士やコミットと作業ツリーの内容を比較する

#### ユースケース

- push する前にリモートリポジトリとの変更点を確認したい
- コミット同士を比較したい

#### コマンド例

```bash
$ git diff # git add する前に変更点の比較
$ git diff HEAD^ # 直前のコミットの差分を表示
$ git diff リモート名/ブランチ名..HEAD # git push する前にリモートとの変更点の比較
$ git diff <変更前のコミットID>..<変更後のコミットID> # コミット同士の比較（ハッシュ は git log で表示される commit の右にある文字列）
$ git diff <ブランチA>..<ブランチ名B> # ブランチ同士の比較
$ git diff -- <ファイルパスA> <ファイルパスB> # 別ファイル同士の比較（-- の後はパスとして認識される）
```

---

#### イメージ

#### 参考

- [git-diff – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-diff/)
- [忘れやすい人のための git diff チートシート](https://qiita.com/shibukk/items/8c9362a5bd399b9c56be)
- [【やっとわかった！】git の HEAD^と HEAD~の違い - Qiita](https://qiita.com/chihiro/items/d551c14cb9764454e0b9)

---

### config

#### 機能

- 現在の設定を取得、変更する

#### ユースケース

- 複数の git アカウントを使い分けたい

#### コマンド例

```bash
$ git config  # 現在いるリポジトリの Git 設定を表示
// TODO: Windows の場合の設定ファイルはどこ？
$ git config --global user.name "<メインアカウントのユーザー名>" # デフォルトのユーザー名を設定
$ git config --global user.email "<メインアカウントのメールアドレス>"  # デフォルトのメールアドレスを設定

$ cd ~/workspace/<リポジトリのルートディレクトリ>
$ git config --local user.name "<サブアカウントのユーザー名>" # 特定リポジトリのユーザー名を設定
$ git config --local user.email "<サブアカウントのメールアドレス>" # 特定リポジトリのメールアドレスを設定
```

#### 備考

- `--global` の設定ファイルは `~/.gitconfig` にある
- `--local` の設定ファイルは `<リポジトリのルートディレクトリ>/.git/config` にある

---

#### イメージ

#### 参考

- [git-config Documentation](https://git-scm.com/docs/git-config)
- [Git をインストールしたら真っ先にやっておくべき初期設定 - Qiita](https://qiita.com/wnoguchi/items/f7358a227dfe2640cce3)
- [複数の git アカウントを使い分ける - Qiita](https://qiita.com/0084ken/items/f4a8b0fbff135a987fea)

---

## ハンズオン

// TODO: コンテンツ作成
