# セッションのゴール
* 多言語対応の実装イメージがなんとなく湧くようになる
* 明日からやれ、と言われた時になんとなく開発コストを想像できる。どこまでやるかの意思決定ができる。

# シナリオ
明日から1週間で英語とアラビア語とロシア語と中国語に対応してくれと言われた場合のロールプレイング。TaptripとDroidKaigiのアプリを例に、基本的にコードを見せながら解説していく。


# 見出し

### タイトル
* 17カ国の多言語対応


### 自己紹介
* GitHubの写真
* Taptripの説明


### キャッチ
* Taptripのstrings.xmlを見せる
* DroidKaigiアプリの説明


### アジェンダ
* シナリオの説明
* アジェンダ


### 翻訳ファイルをわける
* `values/strings.xml` に分ける
* デフォルトの言語はmanifestかgradleで指定する（推奨はen）
* `values-ja/strings.xml` 、 `values-ar/strings.xml` などを作る

* Q. 直書き箇所とかをLintで知ることができないか知りたい
* Q. strings.xmlの管理の工夫を知りたい
* Q. strings.xmlのソート
* Q. translation editor
* Q. 指定したlocaleのstringsを取得する方法は？


### 翻訳する
* Google翻訳
* 外部サービスの紹介
* Googleの公式サービスの紹介

* Q. いいプラグインとかない？
* Q. 翻訳のフローは？
* Q. アラビア語を編集できないんだけど！


### 数値の複数形に対応する
* 数字の修正（複数形の対応）

* Q. 複数形が必要になる言語は？


### 日付に対応する
* 日付の表記
* UTCとlocal時刻の変換

* Q. 日付はどうするのがいいの？
* Q. 一番簡単なやり方は？


### RTLに対応する
* ~start、~endのattributesをつける
* TextView、LinearLayout、RelativeLayout
* 画像の反転
* RTL markの挿入
* インドアラビア数字について

* Q. layout-arは必要？
* Q. APIレベル17未満はどうするべき？
* Q. ぶっちゃけやるべきなの？


### 細かいデザインを調整する
* 言語の長さの違い（改行？ellipsis？）
* マルチバイト文字の行間

* Q. いいやり方は？CustomView？DataBinding？


### まとめ
* めんどくささとやる効果のまとめ