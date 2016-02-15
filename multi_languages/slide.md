# タイトル
* 17カ国の多言語対応Tips
* 株式会社KiHeiTai
* 小西 裕介（@konifar）
* 2016/02/19（金）
* DroidKaigi


# アプリ何言語対応してますか？
> * 日本語と英語やってるよって人？
> * 3ヶ国語やってるよって人？
> * 5ヶ国語以上やってるよって人？
> * 5ヶ国語以上の人がいたらどんなアプリなのか聞いてみる。
> * 5ヶ国語以上やってる人がほとんどだったら自分が話すことなくなるところだった。


# Taptrip
* 17ヶ国語対応
> 17を強調する。

* 世界中に友だちを作るグローバルSNS


# 17ヶ国語・・・？
* strings.xmlが並んだ部分の画像

> 運動会状態


# こにふぁー（@konifar）
* GitHubの写真

> そんなTaptripを作っているという流れで自己紹介をする


# android-material-icon-generator
* 画像
* Googleのマテリアルアイコンをプロジェクトに簡単に入れられる便利プラグイン
* URL


# DroidKaigi 2016
* 画像
* DroidKaigiの公式アプリ。このセッションのサンプルとして作った。
* URL

> これをインストールして見ながら聞けば、たぶんより楽しめる。
> もしかしたら特定端末でちゃんと動かないかもしれない。その場合は、あぁすごくAndroidっぽいなと思って聞いて、Issueもあげといてください。


# Q. 多言語対応は大変？


# A. 「対応」のレベルによる。
* 言語をGoogle翻訳で翻訳？
* RTL言語に応じた細かいレイアウトの調整？
* 通貨や時刻表記などの切替？
* ジェンダーやニュアンスなど細かい翻訳の違いにも完全対応？

> 一つずつ出していく。


# Q. どこまで対応すべきか？


# A. アプリの種類と納期による
* アラビア語圏をターゲットにしたアプリならガッツリRTLも対応すべき
* 2日で英語でつかえるようにするなら、とりあえず翻訳と調整だけ


# 今日のゴール
* 多言語対応の全体の種類と実装イメージ、開発コストがなんとなくわかるようになる

> 例えば明日から1週間で多言語対応しろと言われた時に、どこまで対応するか意思決定できるようになる


# 今日話すTips
* strings.xmlの管理
* 翻訳の外部サービス、フロー
* 複数形の対応
* 日付のローカライズ
* RTL（Right To Left）
* 細かいデザインの調整

> みんな大好きRTL
> 言語によってロシア語は日本語の2倍くらいあったり、中国語は短かかったりする。そのへんのデザインの調整。


# 今日話さないこと
* テスト手法
* ジェンダーの違いなど細かい言語仕様
* 方言レベルのローカライズ
* サーバーを含めた全体の設計
* API17未満のRTL対応
* 多言語対応の効果

> テストは、Spoonつかってキャプチャ撮るのがいいかなぁと考えているがまだ手が出せていないので話さない。この前fastlaneが出したscreengrabも多言語のためのテストツールでよさそう。
https://github.com/fastlane/screengrab

> 言語仕様の話は、話すとそれだけで日が暮れてしまう。どちらかというと翻訳時のやりとりとか全体のフローの話。今日はコードをメインにした話にしたいので省く。

> 方言の話はまだ自分も対応できてないのでしません。中国であれば、values-zhの後にさらに続けて地域のコードも入れるらしいです。

> ユーザーの設定言語をテーブルのカラムに持つとか、サーバーで翻訳するとかそういう話はケースバイケースなのでしません。Taptripではこうしてるみたいな話は後で話せるので気軽に声をかけてみてください。

> API17未満のRTL対応は、個人的には無視でいいと思ってるので話しません。対応するならレイアウトを言語ごとに分ける覚悟が必要です。カスタムビューに細かく分ければちょっと綺麗にできるかもしれません。

> 開発とコードの話をメインにしたいので、効果の話もしません。

# Ready


# 1. strings.xmlの管理


# values-xx/strings.xml
* DroidKaigiのstrings.xmlの3つを並べた画像

> 知っている人も多いと思いますが、strings.xmlは言語ごとに持てます。


# values-xx/strings.xml
* 表示が切り替わった画像

> 置くだけで、端末の言語に応じて表示されます。


# デフォルトの言語の設定
* AndroidManifest


# インドネシア語などの国コードに注意
* × values-id
* ○ values-in

```java
private String convertOldISOCodes(String language) {
    // we accept both the old and the new ISO codes for the languages whose ISO
    // codes have changed, but we always store the OLD code, for backward compatibility
    language = toLowerCase(language).intern();
    if (language == "he") {
        return "iw";
    } else if (language == "yi") {
        return "ji";
    } else if (language == "id") {
        return "in";
    } else {
        return language;
    }
}
```

> http://stackoverflow.com/a/13974180/4440607
> 昔Javaがミスった名残り。Taptripでもミスって、実はインドネシア語が翻訳されていないという事件があった。


# 直書き箇所の洗い出し
* Analyze > Run Inspection by name... > Hard Corded strings
* setText("タイトル") とか検出できる。全て検出されるのでちょっと辛いかもしれない。

```
➜  layout git:(local_time_setting) ✗ grep -n "android:text=\"" * | grep -v "@string" | grep -v "@{"
item_session.xml:54:                    android:text="タイトル"
```


# translation edotorの使いどころ
* strings.xml > Open editor
* 画像
* まだそんなに賢くない
* 抜け漏れ防止くらいにはつかえる

# 17カ国語だと正直使えない
* Taptripのtranslation editorの画像


# 2. 翻訳のフロー

> ここは開発以外の部分もあってわりと退屈なところなので、さらっと流します。


# Taptripの場合
* 1. 日本語でざっと実装
* 2. 社内で英語に翻訳
* 3. 外部サービス（GENGO）を利用して翻訳依頼
* 4. 言語ごとにstrings.xmlに適用

> 3と4を強調する
> たぶんイメージしづらいのはこの部分だと思うのでここを詳しく説明する


# 機械翻訳 or 人力翻訳

機械翻訳 : 無料だけど正確じゃない
人力翻訳 : 高いけど正確

> 大きく2つに分かれる
> 当然、機械翻訳の方が精度はよい。


# 機械翻訳でも読めるレベルになることもある
* 日本語 => 韓国語はすごい精度高い
* 例文

* 奇兵隊で調べた調査結果の表を参照する


# AndroidLocalizationer
* Google翻訳 or Bing翻訳で一発で他の言語のstrings.xmlを作ってくれる
* 画像
https://github.com/westlinkin/AndroidLocalizationer


# 人力翻訳サービスの選定ポイント
* 単価 : 1文字or1単語4~7円くらい
* 速さ : 30分〜1日
* 機能 : API、辞書機能、チャット機能

> このへんはさらっと流す


# 例 : GENGO
* 単価 : 安い。1単語/1文字4〜5円
* 速さ : 17カ国語でも3時間くらいで大体揃う。
* 機能 : APIがある。辞書もあるチャットでやりとりもできる


# xml適用のめんどくささ
* 依頼するときはSpreadSheet or テキストで依頼する
* strings.xmlに入れるときに結構めんどくさい

# 変換スクリプトを使って解決する
* xml <=> csvの変換スクリプト or ASプラグイン
https://github.com/pandawarrior91/Android-strings-xml-csv-converter


# xmlのまま依頼する
* GENGOの場合、 [[[]]]で囲むとその部分は翻訳対象にならない（お金もかからない）ので、xmlのタグ部分を囲って依頼するASプラグインを使っている
* AliceのキャプチャとURL

> AliceはGENGOでしか動かないが、もう少し抽象化してそのうち公開したい
> 正直ここのへんの適用は、翻訳が多いと時間かかるわりにあんまり工夫できていない。経験から言うと、長くても1〜2時間くらいの作業なので、最初はあんまり深く考えずひとまず作業と割り切って頑張るというのでも十分まわる。もちろんエンジニアとしてはこういう作業はなくしていきたいけれども。


# Google公式翻訳サービスを利用する時の工夫
* 実はAndroid Studioのtranslation editorから翻訳依頼ができる
* 参考URL


# strings.xmlのメタタグを利用する
* translatable=falseとか
* descriptionとか
* 翻訳しない文字を囲むとか
* 置換文字の説明とか
* ioschedは参考になる


# アラビア語の編集するときの工夫
* AndroidStudioのエディタは、RTLのテキストに優しくない。
* punchdrunckerさんとのやりとりを載せる。
* デモgif
* エディタを使う
* sublime text、vimなら大丈夫。Atomはダメだった。emacsは見れてない

> 自分でもなれすぎて忘れていたが、カーソル位置がわからなくなる。


# 3. 数詞の複数形対応


# 日本語の場合

1人
2人
3人 <= 変わらない
...


# 英語の場合

1 person
2 people
3 people <= 1かそれ以上かで変わる
...


# アラビア語の場合

0 أشخاص
1 شخص
2 شخصين
3~10 أشخاص
11~100 شخص
100~ شخص


# ？？？？？


# Language Plural Rules
* 画像
http://www.unicode.org/cldr/charts/27/supplemental/language_plural_rules.html


# strings.xml
values-ja/strings.xml
```
<plurals name="number_with_brackets">
    <item quantity="zero">(%1$d أشخاص)</item>
    <item quantity="one">(%1$d شخص)</item>
    <item quantity="two">(%1$d شخصين)</item>
    <item quantity="few">(%1$d أشخاص)</item>
    <item quantity="many">(%1$d شخص)</item>
    <item quantity="other">(%1$d شخص)</item>
</plurals>
```

values-ar/strings.xml
```
<plurals name="number_with_brackets">
    <item quantity="zero">(%1$d أشخاص)</item>
    <item quantity="one">(%1$d شخص)</item>
    <item quantity="two">(%1$d شخصين)</item>
    <item quantity="few">(%1$d أشخاص)</item>
    <item quantity="many">(%1$d شخص)</item>
    <item quantity="other">(%1$d شخص)</item>
</plurals>
```

> plurals.xmlを作った方がいいという人もいるが、同じテキストなのでstrings.xmlにいれる方が管理しやすいと思う。


# getQuantityString()

```java
getResources().getQuantityString(R.plurals.number_with_brackets, count, count);
```

* 代入する数値
* 適用するルールとなる数値

> 順番に表示して説明する


# 数値の区切り

* 日本語: 10,000
* 英語: 10,000
* フランス語: 10.000
* アラビア語: ١٠٬٠٠٠


# NumberFormat
* getNumberInstance()
* getCurrencyInstance()
* getIntegerInstance()
* getPercentInstance()

> 表を用意したい。Qiita書けばよかった


# 4. 日付のローカライズ


# 日付のローカライズ
* DroidKaigiの日付部分の画像を言語ごとに。
* DateFormatとDateUtilsがわりと優秀なのでこれを使えばだいたいできる

> JavaのDateと聞くだけで頭が痛くなる人もいそう
> DroidKaigiのアプリを例に幾つか説明します。

> DateUtilsはQiitaにまとめたい


# 2月19日
```
    public static String getMonthDate(Date date, Context context) {
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN_MR2) {
            String pattern = DateFormat.getBestDateTimePattern(Locale.getDefault(), FORMAT_MMDD);
            return new SimpleDateFormat(pattern).format(date);
        } else {
            int flag = DateUtils.FORMAT_ABBREV_ALL | DateUtils.FORMAT_NO_YEAR;
            return DateUtils.formatDateTime(context, date.getTime(), flag);
        }
    }
```

# 16:00
```
    public static String getHourMinute(Date date) {
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN_MR2) {
            String pattern = DateFormat.getBestDateTimePattern(Locale.getDefault(), FORMAT_KKMM);
            return new SimpleDateFormat(pattern).format(date);
        } else {
            return String.valueOf(DateFormat.format(FORMAT_KKMM, date));
        }
    }
```

# 2016年2月19日 16:00
```
    public static String getLongFormatDate(Date date, Context context) {
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN_MR2) {
            String pattern = DateFormat.getBestDateTimePattern(Locale.getDefault(), FORMAT_YYYYMMDDKKMM);
            return new SimpleDateFormat(pattern).format(date);
        } else {
            java.text.DateFormat dayOfWeekFormat = java.text.DateFormat.getDateInstance(java.text.DateFormat.LONG);
            java.text.DateFormat shortTimeFormat = java.text.DateFormat.getTimeInstance(java.text.DateFormat.SHORT);
            dayOfWeekFormat.setTimeZone(LocaleUtil.getDisplayTimeZone(context));
            shortTimeFormat.setTimeZone(LocaleUtil.getDisplayTimeZone(context));
            return dayOfWeekFormat.format(date) + " " + shortTimeFormat.format(date);
        }
    }
```

> 何枚かスライド使って説明する
> 既存のクラスを使えばできることがおおいと説明する。


# RTL

> 対応するかわからないけれども、お金持ちも多いし意外と人口もいるので攻めていくぞ！となった時になんとなく思い出せるレベルの話をします。


# This is RTL
* Twitterの画像
https://twitter.com/?lang=ar


# DroidKaigi 2016
* アラビア語の画像を出す


# そもそもやるべきなのか？

> 正直、ネイティブの感覚じゃないとよくわからない。
> 元同僚の友達に聞いてみることにした。持つべきものはアラビア人の友達。


# ヨルダン人のイムラン（25）
* イムランの画像


# 対話
こにふぁー : 文字が左から流れてるとやっぱり変なの？
イムラン : 変です。短い文章だと、なんで右側に空白があるの？って思います。

こにふぁー : Drawerとかも右から出てくる方がいいの？
イムラン : そうですね。ヨルダンのアラビア語のアプリはだいたいそうなってます。その方が自然です。

こにふぁー : じゃあよくわからないけど、全部右からの方がいいんだね。
イムラン : 間違いないです。


# ただし
* イムランに教えてもらったアプリはDrawerは左から出てきた。
* 画像

> そんなにこだわらなくてもいいのかもしれない。ただし、文字は右からの方がいいらしい。
> 今回は、完全に対応して鏡にうつしたような形に実装するにはどうしたらいいのかを話す。
> たぶん、皆さんが思ってるより難しくない。そのわりに、ものすごくちゃんと対応できてる感あるのでオススメ


# start、end attributes
* 例のxmlのbefore、after

> paddingやmargin、to~ofなど、layout_~やgravity系の位置を制御するattributesには、startとendを指定する。


# Android Studioの便利ツール
* Refactor > Add RTL Support Where Possible...を使おう！
* 画像


# Drawerも同様
```
    <android.support.v4.widget.DrawerLayout
        android:id="@+id/drawer"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:fitsSystemWindows="true"
        tools:openDrawer="start">
```


# ViewPager
* RtlViewPagerを適用する前のgif
* ViewPagerはRTLに対応できていない
* DroidKaigiアプリでは、Wrapperを用意した


# RtlViewPager
* ViewPagerとAdapterを包んでscrollと順番を反転してくれる。
* 中でRTLにすべきかどうかの判定をしている。
* 判定部分のコード
* RtlViewPagerのコードのURL


# RTL markの挿入
* 文字の1文字目がアラビア語じゃない時、左から流れてしまう。
* 対応しきれていない状態の画像
* これはTwitter公式アプリも未対応。
* RTLmarkのリンク
* 強制的にRTLにする装飾文字。


# RTL mark in strings.xml
コード


# RTL mark in Java
* CustomViewを作ってsetTextをオーバーライド
* DataBindingのcustom attributesを使う

# RTL mark using DataBinding
```
    @BindingAdapter("textRtlConsidered")
    public static void setTextRtlConsidered(TextView textView, String text) {
        textView.setText(LocaleUtil.getRtlConsideredText(text));
    }

    public static boolean shouldRtl() {
        return TextUtilsCompat.getLayoutDirectionFromLocale(Locale.getDefault()) == ViewCompat.LAYOUT_DIRECTION_RTL;
    }

    public static String getRtlConsideredText(String text) {
        if (shouldRtl()) {
            return RTL_MARK + text;
        } else {
            return text;
        }
    }
```

> 簡単に説明する


# RTL mark using DataBinding
* xmlで `android:text` の代わりに `app:textRtlConsidered`を使うだけ。

> DatabindingのBindingAdapterは、既存のViewにちょっと機能を追加したい時に結構よさそう


# インドアラビア数字
* DroidKaigiアプリの画面


# 使い分け聞いてみた by イムラン
こにふぁー : これやっぱりこの数字の方がいいの？
イムラン : そうですね！日付はその方が自然です。
こにふぁー : 時刻は？
イムラン : 時刻は・・・普通のアラビア数字の方がいいかもしれないです。
こにふぁー : ？！じゃあ30分とかは？
イムラン : それはアラビア数字の方がいいです。

> 使い分けがよくわからん。イムランも悩んでいたので違う人にも聞いてみた


# 使い分け聞いてみた by ざかりあ from アルジェリア
こにふぁー : 日付はインドアラビア数字の方がいいんだよね？
ザカリア : アラビア数字の方がいいと思う。僕は生まれてからあんまりインドアラビア数字を使ったことがないよ
こにふぁー : ？！

> 結局なんかよくわからないけれども、たぶん地域にもよる。なので正直どちらでもいいけれども、電話番号とかはアラビア数字の方がいいらしい。


# NumberFormatやDateUtils
* とりあえずこの2つにしたがって変換しておけばよいと思う。
* 無理に変換するロジックをかませる必要はなさそう。
* やるとしたら、CustomViewを作るかDataBindingを使うのがよさそう


# 6. 細かいデザインの調整

> デザインの話になるので、あんまり詳しくははなさない。
> Taptripの場合、デザインを先にあげてもらってエンジニアが見てレビューをするんですけれども、その時によく指摘する勘所があるので紹介する


# 言語によるテキストの長さの違い
* 日本語
* 中国語
* ロシア語

> 日本語はわりと短い言語
> 中国語が一番短い
> ロシア語が一番すごい。長すぎる。基本日本語の2倍あると思った方がいい。

# テキスト長さの違いをどうするか
* そもそもテキストを使わない
* 行固定にする
* 文字サイズを変える


# 行固定にする場合、
* ellipsisとlines、maxLinesで調整する
* コード


# 言語によって行間を変える
* 行間が大きい方が読みやすい言語があります。
* 画像


# values-xxで対応する
* 画像
* dimens.xmlを言語ごとに用意して使うのがいいと思います。
> DataBindingを使ったりCustomViewを作ってもいいんですが、


# まとめ

> ざーっと駆け足て話してきたので、全体をまとめます。


# まとめ
* 1. strings.xmlの管理
* 言語ごとの用意は必須です。漏れのないようにAndroidStudioの機能を利用しましょう。

* 2. 翻訳のフロー
* できればお金をかけて精度をあげましょう。プラグインやスクリぷとを駆使して手間は減らしましょう。

* 3. 複数形の対応
* pluralsを正しく使いましょう。

* 4. 日付のローカライズ
* DateUtils、SimpleDateFormatを使いましょう。

* 5. RTL（Right To Left）
* アラビアを責めるならガッツリやりましょう。start、endの対応だけでもだいぶ違います。

* 6. 細かいデザインの調整
* デザイナーさんと協力しつつ、文字の長さや行間を考慮しましょう。本気で対応するなら言語ごとに表示を変えるレイアウトやカスタムビューを用意しましょう。


# 多言語対応はstep by step


# どこまでやるかを認識合わせて


# できることからコツコツと


# 海外で話題になるとちょっと嬉しい
> Taptripの例を出したい。


# ありがとうございました
* DroidKaigiアプリのURL


