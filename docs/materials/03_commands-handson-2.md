---
marp: true
paginate: true
theme: git
# header: 'Git勉強会 - 基本コマンド ＆ ハンズオン'
# footer: '![width:100](../../marp-themes/logo.png)'
---

# Git 勉強会 3 日目

〜基本コマンド ＆ ハンズオン ②〜
2022/03/28

---

## 2 日目アジェンダ

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

## 3 日目アジェンダ（今日はこっち）

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

### pull

#### 機能

- リモートリポジトリの内容を取得し、現在のブランチに取り込む（`git fetch` + `git merge`）

#### ユースケース

- リモートリポジトリの最新情報をローカルリポジトリに取り込みたい

#### 主なオプション

- `-r | --rebase`: フェッチ後に現在のブランチを上流ブランチの上にリベース
  - `git fetch` + `git rebase`

#### コマンド例

```bash
$ git switch <ブランチ名> # まず pull したいブランチへ切り替える
$ git pull origin <ブランチ名> # リモートリポジトリの内容を取得してマージ。上流ブランチを設定している場合は git pull で OK
$ git pull -r origin <ブランチ名> # リモートリポジトリの内容を取得してリベース。
```

---

#### イメージ

#### 参考

- [git-pull – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-pull/)
- [git pull コマンドの使い方と、主要オプションまとめ](https://www-creators.com/archives/2295)
- 【初心者向け】git fetch、git merge、git pull の違いについて
- [git pull と git pull –rebase の違いって？図を交えて説明します！](https://kray.jp/blog/git-pull-rebase/)

---

### fetch

#### 機能

- リモートリポジトリの内容を取得する
  - 取得した内容はローカルのリモート追跡ブランチに反映するが、ワーキングツリーには反映しない

#### ユースケース

- 他者が作成したブランチに切り替えたいので、リモートリポジトリの最新状態を取得したい
- pull だとワーキングツリーまで更新してしまうので、とりあえずリモートの状態を確認したい

#### 主なオプション

- `--all`: すべてのリモートリポジトリの内容を取得
  - リモートリポジトリが origin しかない場合は使うことはない

#### コマンド例

```bash
$ git fetch # リモートリポジトリの内容をローカルのリモート追跡ブランチに反映
```

---

#### イメージ

#### 参考

- [git-fetch – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-fetch/)
- [git pull と git pull –rebase の違いって？図を交えて説明します！](https://kray.jp/blog/git-pull-rebase/)

---

### merge

#### 機能

- 他のブランチやコミットの内容を現在のブランチに取り込む

#### ユースケース

- fetch した内容をワーキングツリーに反映したい
- マージ時にコンフリクトしたので、競合を解決したい

#### 主なオプション

- `--no-ff`: fast-forward であっても必ずマージコミットを作成
- `--continue`: コンフリクト解決後、マージを続行
- `--abort`: コンフリクト解決を中止し、マージ前の状態に再構築

#### コマンド例

```bash
$ git switch <マージ先のブランチ名>
$ git merge <マージ元のブランチ名>
```

---

#### イメージ

#### 参考

- [git-merge – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-merge/)
- [git pull と git pull –rebase の違いって？図を交えて説明します！](https://kray.jp/blog/git-pull-rebase/)

---

### rebase

#### 機能

- コミットを再適用する（ブランチの分岐点を変更したり、コミットの順番を入れ替えたりできる）

#### ユースケース

- fetch した内容をワーキングツリーに反映したい（コミットログは一直線に保ちたい）
- リベース時にコンフリクトしたので、競合を解決したい
- 複数のコミットをひとつにまとめたい（2 つ以上前のコミットを修正したい）

#### 主なオプション

- `--continue`: コンフリクト解決後、リベースを続行
- `--abort`: コンフリクト解決を中止し、リベース前の状態に再構築
- `-i | --interactive`: 複数のコミットを統合

#### コマンド例

```bash
$ git switch <マージ先のブランチ名>
$ git rebase <マージ元のブランチ名>
$ git rebase -i HEAD~4  # 最新から 4 つ分のコミットを修正・統合
```

---

#### イメージ

#### 参考

- [git-rebase – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-rebase/)
- [git pull と git pull –rebase の違いって？図を交えて説明します！](https://kray.jp/blog/git-pull-rebase/)
- [git rebase を初めて使った際のまとめ - Qiita](https://qiita.com/310ma3/items/e0ec74b47c6c219f2a8b)
- [rebase -i でコミットをまとめる - Qiita](https://qiita.com/takke/items/3400b55becfd72769214)
- [【やっとわかった！】git の HEAD^と HEAD~の違い - Qiita](https://qiita.com/chihiro/items/d551c14cb9764454e0b9)

---

### stash

#### 機能

-　未コミットの変更を退避する

#### ユースケース

- 他ブランチに切り替えたいが、作業が中途半端なのでコミットはしたくない

#### 主なオプション

- `-u | --include-untracked`: 追跡対象に含まれていないファイル（新規作成ファイルなど）も含めて退避

#### コマンド例

```bash
$ git stash -u  # 新規作成ファイルも含めて変更を退避
$ git stash -u push "<メッセージ>"  # メッセージを付けて変更を退避
$ git stash list  # 退避した作業の一覧を見る
$ git stash apply stash@{0} # 退避した作業を戻す。stash@{N} を省略した場合は直前に stash した情報を戻す
$ git stash show  stash@{0} -p # 退避した変更の詳細を見る
```

---

#### イメージ

#### 参考

- [git-stash Documentation](https://git-scm.com/docs/git-stash)
- [【git stash】コミットはせずに変更を退避したいとき - Qiita](https://qiita.com/chihiro/items/f373873d5c2dfbd03250)

---

### restore (checkout)

#### 機能

-

#### ユースケース

-

#### 主なオプション

- `-s| --source`: 指定したコミットの状態にワークツリーファイルを復元

#### コマンド例

```bash
git restore # 保存前に戻す
git restore -S # addされる前に戻す

git restore -s <コミット識別子> <ファイル名>  # 特定のファイルを、特定のコミット時点に戻す

```

---

#### イメージ

#### 参考

- [git-restore – Git コマンドリファレンス（日本語版）](https://tracpath.com/docs/git-restore/)

- git switch と restore の役割と機能について - Qiita
- [Git 初心者なら必ず覚えるべき git restore コマンド](https://iwb.jp/git-restore-s-head-commit-fix/)

---

### reset

#### 機能

- ファイルをインデックスから削除し、特定のコミットの状態まで戻す

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

- a

---

### revert

#### 機能

-

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

- a

---

### cherry-pick

#### 機能

-

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

- a

---

### blame

#### 機能

-

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

- a

---

### tag

#### 機能

- コミットにタグを付ける、削除する、一覧表示する

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

- a

---

## ハンズオン

// TODO: コンテンツ作成
