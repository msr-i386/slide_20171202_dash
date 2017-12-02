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
# セットアップ(1)

* Dash Buttonの初期設定を行う
* 環境整備  
  node.js, pythonが必要

---
# セットアップ(2)

* dasherのセットアップ  
$ git clone  https://github.com/maddox/dasher.git  
$ cd dasher  
$ npm install

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
