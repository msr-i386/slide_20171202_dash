# Amazon Dash Hack

@第33回シェル芸勉強会 大阪サテライト

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
# Amazon Dash Button

* 押すだけで商品が買えるボタン (※要設定)
* 定価500円
* 初回購入時に500円割引してくれるので実質タダで入手可能
* Amazon Prime会員限定

---
# 今回の目的

* Dash Buttonをハックする
    * ボタンを押しても商品を買えないようにする
    * dasherを使用してHTTPリクエストをオーバーライドする
    * シェルコマンドが実行されるようにする

---
# セットアップ(1) Dash Buttonの初期設定

* スマートフォン向けAmazonアプリから、Dash Buttonの設定を行う  
  [Amazon公式のセットアップ方法](https://www.amazon.co.jp/gp/help/customer/display.html/ref=amb_link_1?ie=UTF8&nodeId=201746340)を
  参照し、Dash Buttonの設定を行っていく。ただし...
* 商品選択画面(下図)で商品を選ばずに終了する (重要)  
  商品を選んでしまうと、注文が成立してしまう

---
# セットアップ(2) 環境整備

* node.js, pythonのインストール
```
$ sudo apt install nodejs python
$ node -v
$ python --version
```

* dasherのインストール
```
$ git clone  https://github.com/maddox/dasher.git  
$ cd dasher  
$ npm install
```

---
# セットアップ(3)

* Dash ButtonのMACアドレスを取得  
$ ./script/find_button

---
# セットアップ(4)

* config/config.jsonを編集  

```
{"buttons":[
  {
    "name" : "test",
    "address": "xx:xx:xx:xx:xx:xx",
    "url": "http://localhost:8000/cgi-bin/exec",
    "method": "GET",
    "json": true,
    "body": {"echo TEST":""}
  }
]}
```

※urlの値を http://localhost/cgi-bin/exec に、bodyの値にコマンドを書く

---
# セットアップ(5)

* 実行CGIを書く  

```
$ cat cgi-bin/exec  
#!/bin/sh  
  
eval \`echo ${QUERY_STRING} | tr '%' '=' | nkf -WwmQ\`
```

* 簡易Webサーバーを実行  
$ python -m CGIHTTPServer

---
# デモ

---
# 参考

* Amazon Dash ButtonをただのIoTボタンとして使う  
https://qiita.com/jsoizo/items/3b8bba4160f41aef20f4
* ワンライナーWebサーバを集めてみた  
https://qiita.com/sudahiroshi/items/e74d61d939f18779970d#pythoncgihttpserver%E7%B7%A8
