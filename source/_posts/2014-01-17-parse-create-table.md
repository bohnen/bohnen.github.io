---
layout: post
title: "SQLのパース"
date: 2014-01-17 20:48:03 +0900
comments: true
categories: [Ruby]
---

ALTERやらCREATE TABLEやらCREATE INDEXやらがごちゃ混ぜになったDDLファイルから、
CREATE TABLEだけを引っこ抜き、それぞれの属性の名称と型を調べる必要に迫られた。

SQLの解析はちょっと面倒で、特に、型がそれぞれパターンが異なることから、パーサー使わないといけないと
思い立ち、そこからRubyのパーサライブラリ探索の旅が始まるのであった。

<!--more-->

## CREATE TABLE文の抜き出し

なにはともあれCREATE TABLE文だけを抽出しなければいけないが、これは最短マッチを使うことですんなり行く。

```ruby
match = ARGF.read.scan(/CREATE TABLE.*?;/m)
```

## parslet と Rsec

今回はパーサライブラリとして、使うのが簡単そうな [parslet](http://kschiess.github.io/parslet/install.html)を
使ってみる。

と、思ったんだけど、途中で[こんなスレ](https://www.ruby-forum.com/topic/3444183)を見つけてしまい、速いと評判だった
[Rsec](https://github.com/luikore/rsec) を使って書くことにした。

くせがあって慣れるのが大変だったんだけど、慣れたら全然使い易い。Rsecの使い方はメモしておかないと忘れそうだ。
明日にでも書こう。

## PEG (Parsing Expression Grammer)

パーサージェネレーターとか触るの10年ぶりくらいだったので、Rsecのようにプログラム中にごりごり書けるのは衝撃だった。
それ以上に、PEGが何かが分かっていなくて、/[^,]*/ でマッチするようなルールを書いてしまい、「あっれー？おかしいな、
どんなルールを書いても末尾まで読んでしまってSyntax error吐いちゃう・・・」みたいなことで頭を悩ませていた。

PEGの "|" は左から実行され、失敗したらバックトラックして右側に進んでいく。

これだけ分かると、後は簡単。汎用的なマッチほど、後ろに書けばいいわけだ。
例えばCHARは CHARACTERでもいいけど、この場合は 'CHARACTER'.r | 'CHAR'.r と書かないと、先にCHARにマッチしてしまって
そちらで評価されることになる。（それを防ぐ為の word('CHAR')という書き方もあって、これだと単語として独立していないとマッチしない）

PEGをベースにしたパーサーはずいぶん使いやすい。何より書いてすぐ試行錯誤できるのがいい。

