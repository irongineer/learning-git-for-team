# Git 勉強会

## 目的

- チーム開発おけるワークフローで Git でつまづくことを減らし、開発に集中できる時間を増やす

## 背景

- 自チームでメンバーが Git について躓き、様子を見ていたら一時間以上立っても解決しなかった
- 結局２時間近くペアプロしながら Git の rebase やコンフリクト解消の方法を教えたが、覚えてもらえず、その後も同じところで何度も躓いていた
- ペアプロして気づいたが、想像がつかないようなリポジトリの運用方法をしていた（ブランチごとにリポジトリを別フォルダに clone してくる）
- このまま目先の期限のために業務を進めるより、勉強する時間を取って Git に費やす時間をチーム的に減らしたほうがいいと感じた

## ターゲット
- Git 初心者、Git を恐れながら触っている人
  - 入社 1~2 年目の開発者
  - QA, DMO, デザイナーといった開発中心ではない開発所属の人
  - 年次に関係なく Git に心理的障壁を感じている人

## 目標

- メンタル
  - Git は怖くない
  - 何か分からないことがあっても自分で調べて解決ができる、または原因の目処がつく
- スキル
  - Git の概念の理解
  - Git でのチーム開発の方法と一通りのコマンドの修得
  - 誤った変更を元に戻せる
  - コンフリクトの解消ができる
  - GitHub を用いたプルリクエスト・レビュー・マージの開発フロー

## 雑多な気持ち

- ハンズオンを十分に入れたい
  - 手を動かさないと覚えないから
- 実務でつまづいたときに、「あの資料を見返せばいい」というインデックス的な存在にしたい
- 応用編で commit-lint や PR Template などの話をするつもりだけど、このリポジトリで利用したら実例として分かりやすそう

## ネタ帳

- 概念
  - Git
- ブランチ
  - Git switch
  - Git restore
  - 修正を一時退避する
- コミット
  - コミットを修正する
  - コミットメッセージを修正する
  - コミットをひとつにまとめる
  - .gitignore
- マージ
  - マージの種類
  - コンフリクト
  - git log
- チーム開発
  - Git Flow
  - Rebase
  - 最新を反映する
  - cherry pick
  - なるべく PR を溜めない
- 応用
  - VS Code の便利機能
    - Git Lens, 差分, コンフリクト解消, etc
  - GitHub PR の便利機能
    - PR Template, Suggestion,
  - コミット時にコミットメッセージ解析をする (commit-lint)
  - コミット時にソース解析をする (husky & lint-staged)
  - git log の整形
  - エイリアス登録

## 参考資料

### スライド

- ミクシィ
  - git 研修（[動画](https://youtu.be/aZ90usArA6g)、[スライド](https://docs.google.com/presentation/d/1EwjQnoqzzYsijrMNEsWGAj54yfQlbr2mvuxrDtKl-Ww)）
- カヤック
  - [2013 年技術部新卒研修](https://github.com/kayac/newbie-training) - GitHub
- ブレインパッド
  - [Git ハンズオン研修 / Git Hands-on](https://speakerdeck.com/brainpadpr/git-hands-on) - (2020/07/14)
- ドワンゴ
  - [2016 年度新卒デザイナー GitHub 研修の紹介](http://creator.dwango.co.jp/10989.html) - (2017/04/13)

### 記事

- [Git でやらかした時に使える 19 個の奥義](https://qiita.com/muran001/items/dea2bbbaea1260098051)
- [VSCode のオススメ拡張機能 24 選 (と Tips をいくつか)](https://qiita.com/sensuikan1973/items/74cf5383c02dbcd82234)
- [Git のコミットメッセージの書き方](https://qiita.com/itosho/items/9565c6ad2ffc24c09364)
- [GitHub で使われている実用英語コメント集](https://qiita.com/shikichee/items/a5f922a3ef3aa58a1839)
- [【今日からできる】コミットメッセージに 「プレフィックス」 をつけるだけで、開発効率が上がった話](https://qiita.com/numanomanu/items/45dd285b286a1f7280ed)
- [君には 1 時間で Git について知ってもらう(with VSCode)](https://qiita.com/jesus_isao/items/63557eba36819faa4ad9)
- [VSCode での Git の基本操作まとめ](https://qiita.com/y-tsutsu/items/2ba96b16b220fb5913be)
- [【GitHub 超初心者入門】この前初めて GitHub を使い始めたエンジニア見習いが書く GitHub の使い方と実践～とりあえず一緒に動かしてみようぜ！～](https://qiita.com/nnahito/items/565f8755e70c51532459)
- [[ver 1.2] Git でよく使われるコマンドにイラストによる説明を加えて 1 枚のチートシートにまとめてみた](https://qiita.com/kozzy/items/b42ba59a8bac190a16ab)
- [Git・GitHub に隠された便利な機能 | GitHub Cheat Sheet（日本語訳）](https://qiita.com/unbabel/items/1cf05f2a2be3d6fb3388)
- [【Git】基本コマンド](https://qiita.com/konweb/items/621722f67fdd8f86a017)

- [[Git] .gitignore の仕様詳解](https://qiita.com/anqooqie/items/110957797b3d5280c44f)

- [いまさらだけど Git を基本から分かりやすくまとめてみた](https://qiita.com/gold-kou/items/7f6a3b46e2781b0dd4a0)
-

- [Git-flow って何？ - Qiita](https://qiita.com/KosukeSone/items/514dd24828b485c69a05)
-
- [git で難しいことしたくなければこのフロー、3step だけ、という覚書](https://qiita.com/e99h2121/items/e9941211d9780d5b68c9)
- [[Windows 向け]Git クライアント使い分け](https://qiita.com/yukyt/items/da2d371fce4235bfb8e3)
-

### サイト

- Learn Git Branching へようこそ
  - https://learngitbranching.js.org/?locale=ja
- Pro Git 日本語版電子書籍公開サイト
  - http://progit-ja.github.io/
