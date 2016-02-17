# 実践！Androidプラグイン開発
* 株式会社KiHeiTai
* 小西 裕介（@konifar）
* 2016/02/18（木）
* DroidKaigi Day1


# こにふぁー（@konifar）
* GitHubの写真


# Taptrip

> グローバルSNS


# android-material-icon-generator
* GitHubの画像


#️ 説明


# android-material-icon-generator
* デモのgif


# Android Studioプラグインの作り方を話します

> 作ったことがある方いますか？
> わりとつらい。情報がまとまってない。


# 導入など基礎はこちら
* Qiitaのリンク


# 簡単に導入



# ここまではわりと簡単にできる



# 問題はここから先
* テキストを選択した時にメニュー出すには？
* ダイアログやアラートはどうやって出せばいいの？
* ファイル操作はどうやる？



# 今日のゴール
* 開発の流れがわかるようになる
* 調べ方のコツがわかるようになる
* 自分でも作れそうだなと思えるようになる



# 
* 1. 覚えておくべきクラスの役割
* 2. UIの実装j
* 3. 悩んだ時の調べ方

> プラグイン開発、最初は何をどうしたらいいかわからない。
> けれど、ActivityやContextみたいな、とりあえずこれは覚えとけみたいなクラスがいくつかある。それを掴んでおくだけで全然違うのでいくつか紹介する

> UIの実装は、適切なものを使うのが大事。これもAndroidと同じ。

> その2つの基礎を知った上で、悩んだときはこのへんのコード見ればだいたいやりたいこと真似できるよっていうのを紹介する


# 今日話さないこと
* swingの細かい話
* テストコードの話

> swingで画面を作る。これを話し出すとswingのセッションになってしまうのであんまり話さない。
> テストは実は自分自身まだ手をつけられていない。普通にJUnit4は動かせる。



# 1. 覚えておくべきクラスの役割


# 
 * AnActionEvent
 * Project
 * Editor
 * Document
 * PsiFile



 # AnActionEvent



 # Project



# Editor





# Document





# PsiFile





# UIの実装

 * Tool Window
 * Dialog
 * Editor Hint
 * Notification
 * File Chooser
 * Class、Package Chooser


# Tool Window



# Dialog



# Editor Hint



# Notification



# File Chooser






# アクションの探し方
* Android Studioのコードを読む
* GiHubリポジトリの紹介



# Androidに比べると簡単



