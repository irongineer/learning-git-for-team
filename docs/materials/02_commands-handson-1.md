---
marp: true
paginate: true
theme: git
header: 'Git勉強会 - 基本コマンド ＆ ハンズオン'
# footer: '![width:100](../../marp-themes/logo.png)'
---

![width:200](../../marp-themes/logo.png)

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
  - pull
  - fetch
  - merge
  - rebase
  - stash
  - restore (checkout)
  - reset
  - revert
  - cherry-pick
  - blame
  - tag
  - reflog

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

![](../../assets/icons/logo.png)

#### 参考

- ***

---

### clone

#### 機能

- リポジトリのクローンを作成する

#### ユースケース

- 既に存在するリモートリポジトリ（GitHub/GitLab）のソースコードをローカルに複製したい

#### 主なオプション

- `-b`: 複製したいブランチを指定する（b: branch）

#### コマンド例

```bash
$ git clone <リモートリポジトリの URL>
$ git clone <リモートリポジトリの URL> -b <ブランチ>
```

---

#### イメージ

#### 参考

- ***

---

### switch (checkout) # TODO: branch の前後に移動する？

#### 機能

- 作業ツリーを異なるブランチに切り替える

#### ユースケース

- 既に存在するブランチに移動したい
- 新しいブランチを作成したい

#### 主なオプション

- `-c`: ブランチを新規作成して切り替え（c: create）

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

- `-v`: 詳細を表示（v: verbose）

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

#### コマンド例

```bash
$ git branch
$ git branch -m <変更前のブランチ名> <変更後のブランチ名>  # 今いるブランチ上で git branch -m <変更後のブランチ名> でも OK
$ git branch -d <ブランチ名>  # git branch -D <ブランチ名> で強制削除
```

---

#### イメージ

#### 参考

- [git-branch – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-branch/)
- [git branch コマンド - Qiita](https://qiita.com/chihiro/items/e178e45a7fd5a2fb4599)

---

### status

#### 機能

- ワークツリーにあるファイルの状態を表示する

#### ユースケース

- どのファイルを変更したのか、add, commit 済かどうかを知りたい
- コンフリクトしたのでどうすればいいか知りたい
- よく分からないけどエラーになったから対処方法を知りたい

#### 主なオプション

- `-s`: 短い形式で表示（s: short）

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

- `-p`: ファイル内の任意の変更行のみインデックスに追加（p: patch）

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

- 2 つ以上まえのコミットを修正したい場合、`git rebase -i` を利用する

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

-

#### 主なオプション

-

#### コマンド例

```bash
$ git
```

---

#### イメージ

#### 参考

- [git-push – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-push/)

---

### log

#### 機能

- コミット時のログを表示する

#### ユースケース

-

#### 主なオプション

-

#### コマンド例

```bash
$ git
```

---

#### イメージ

#### 参考

- ***

---

### diff

#### 機能

- コミット同士やコミットと作業ツリーの内容を比較する

#### ユースケース

-

#### 主なオプション

-

#### コマンド例

```bash
$ git
```

---

#### イメージ

#### 参考

- ***

##

---

<style scoped>
  section { font-size: 190%; }
</style>

---

## Fin.
