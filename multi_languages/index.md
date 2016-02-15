# セッションのゴール
* 多言語対応の実装イメージがなんとなく湧くようになる
* 明日からやれ、と言われた時になんとなく開発コストを想像できる。どこまでやるかの意思決定ができる。

# シナリオ
明日から1週間で英語とアラビア語とロシア語と中国語に対応してくれと言われた場合のロールプレイング。TaptripとDroidKaigiのアプリを例に、基本的にコードを見せながら解説していく。


# 話さないこと
* テストの話
* ジェンダーの違いなど言語仕様の細かい話
* サーバーを含めた全体の設計が関わる話
* API17未満のRTL対応


# 見出し

### タイトル
* 17カ国の多言語対応
* 株式会社奇兵隊kiheitai


### 自己紹介
* GitHubの写真
* Taptripの説明

* H. よく「何ヶ国語話せるんですか？」と聞かれるけど、日本語だけ。英語も危ういので頑張ってる。


### キャッチ
* Taptripのstrings.xmlを見せる
* DroidKaigiアプリの説明


### アジェンダ
* シナリオの説明
* アジェンダ



### [基本] 1. 翻訳ファイルをわけよう
* `values/strings.xml` に分ける
* `values-ja/strings.xml`、 `values-ar/strings.xml` などを作る

* Q. 直書き箇所とかをLintで知ることができないか知りたい
* Q. strings.xmlのソート
* Q. translation editorの使いどころ


### [基本] 2. 翻訳する
* Google翻訳
* 外部サービスの紹介（GENGO、単価、速さ、API）
* Googleの公式サービスの紹介

* Q. strings.xmlの管理の工夫を知りたい
* Q. 共通化すべきstringsは？ [ref](http://qiita.com/eggmobile/items/95062a44dba3d63d43da)
* Q. いいプラグインとかない？
* Q. 翻訳のフローは？
* Q. アラビア語を編集できないんだけど！
* Q. 指定したlocaleのstringsを取得する方法は？（入れない）


### [ローカライズ] 3. 数値の複数形に対応する
* 数字の修正（複数形の対応）
* カンマ、ピリオドなど [ref](http://qiita.com/aqubi/items/36e24c2896321cd6df0f)

* Q. 複数形が必要になる言語は？
* Q. 複数形の表を用意する


### [ローカライズ] 日付に対応する
* 日付の表記
* UTCとlocal時刻の変換

* Q. 日付はどうするのがいいの？
* Q. 一番簡単なやり方は？


### [ローカライズ] RTLに対応する
* ~start、~endのattributesをつける
* TextView、LinearLayout、RelativeLayout
* 画像の反転
* RTL markの挿入
* ViewPager
* インドアラビア数字について

* Q. layout-arは必要？
* Q. APIレベル17未満はどうするべき？ <= はなさない
* Q. ぶっちゃけやるべきなの？


### [デザイン] 細かいデザインを調整する
* 言語の長さの違い（改行？ellipsis？） [ref](http://qiita.com/hachi8833/items/4666638e930de65dcdef)
* マルチバイト文字の行間

* Q. いいやり方は？CustomView？DataBinding？


### まとめ
* めんどくささとやる効果のまとめ