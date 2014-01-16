---
layout: post
title: "パーフェクトRuby ch.15"
date: 2014-01-16 19:26:26 +0900
comments: true
categories: [Ruby, Book]
---

積ん読になってたパーフェクトRubyを実際にコーディングしながら読み進めてみた。
15章はコマンドラインのTodoアプリケーションの開発だ。

Rubyは初級レベル。awkの代わりにちょっとしたスクリプトを作成するのに使うかという程度の利用しかやってなかったので、Rubyでのアプリケーションの開発は初めて（仕事ではほとんどJavaだし）。

<!--more-->

ポイント
--------
* bundlerによるgemのスケルトンの作成。gemの構造の理解
* ActiveRecordによるDB接続と、ORMの提供
* OptionParaserによるコマンドライン引数の解析

Gemの作り方を学べたのと、OptionParaserでのサブコマンドの作り方を丁寧に書いてあって分かりやすかった。

Bundler
-------

* [本家サイト]( http://bundler.io/ )
* bundlerはrubyのアプリケーションでのgemの依存関係を整理してくれる
* gemのスケルトンの生成もやってくれて便利

```
> $ bundler gem todo -b 
```

* 設定はGemfileに記載。Gemfileから、todo.gemspecを読み込むようだ。
* bundle execコマンドで、ruby や rakeなどのコマンドを Gemfile/todo.gemspecを読み込んだ上で実行してくれる。環境依存の情報はこの二つのファイルに書けばよく、アプリケーションコードを汚さない。
* 開発時に必要だけどプロダクションでは不要といった依存関係も書ける。

ActiveRecord
-------------

* [API Document](http://api.rubyonrails.org/files/activerecord/README_rdoc.html)
* ActiveRecord::Baseを使ってDB接続の作成、テーブルの作成を実施
* ActiveRecord::Baseを継承したクラスはテーブルに対応したモデルクラスになる。このときクラス名は単数、テーブル名は複数形というネーミングルール
* [scope](http://guides.rubyonrails.org/active_record_querying.html#scopes) を使って、複雑な条件をまとめた新たな検索メソッドを定義できる。
16章でview側に検索結果を引き渡すときに役立った。

OptionParser
--------------
* [API Document](http://guides.rubyonrails.org/active_record_querying.html#copes) 
* サブコマンドの解析はできないので、サブコマンドを解析させるときは、サブコマンド毎にOptionParserのインスタンスを作成する
* ヘルプは opt.banner, opt.separator などのメソッドでカスタマイズできる。opt.on で解析するオプションは自動で出力されるが、サブコマンドのヘルプは自動で出力されないので、自分で組み立てて表示する必要がある。


