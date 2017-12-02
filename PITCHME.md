# Amazon Dash Hack

@第32回シェル芸勉強会 大阪サテライト

---
# 目次
* Amazon Dash Buttonとは
* Dash Button Hack方法
* デモ
* まとめ

---
# 自己紹介

* ハンドルネーム: MSR
 * [Twitter ID: @msr386](https://twitter.com/msr386)
* Webブラウザ [Tungsten](https://app.tungsten-start.net/) の作者

---
# 目次

* 前回の復習、今回の目標
* fork爆弾爆発中のロードアベレージの取り方を考える
* デモ

---
# Amazon Dash Button

* 押すだけで決まった商品を買えるボタンを搭載
* 定価500円
* 初回購入時に500円割引してくれるので実質タダで手に入る
* Amazon Prime会員限定

---
# 今回の目的

* 押しても商品を買えないようにする
* 代わりにシェルコマンドを実行するようにハックする

---
# セットアップ

* Dash Buttonの初期設定を行う
* 環境整備  
  node.js, pythonが必要
* dasherのセットアップ  
$ git clone  
$ vi dasher/config.json  
※urlの値をhttp://localhost/cgi-bin/execに、bodyの値にコマンドを書く
* Dash ButtonのMACアドレスを取得  
MACアドレスはconfig.jsonへ
* 実行CGIを書く
$ 
* 簡易Webサーバーを実行
$ python -m CGIHTTPServer

---
# デモ

