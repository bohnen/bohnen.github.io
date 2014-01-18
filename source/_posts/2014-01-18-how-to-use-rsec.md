---
layout: post
title: "Rsecメモ"
date: 2014-01-18 19:22:00 +0900
comments: true
categories: [Ruby, Rsec]
---
sqlの簡単な解析を行ったときに[Rsec](https://github.com/luikore/rsec) を使ったので、そのメモ。
Rsecは2年ほど前から更新されていないが、コンパクトで使いやすいし、動かしながら慣れていけるのが良い。

<!--more-->

## インストール
Ruby 1.9用とあるが、2.0でも利用できた。

```bash
$ gem install rsec
```

## 使い方

```ruby
require 'rsec'
include Rsec::Helper
```

これで、http://rsec.heroku.com/ref にあるようなDSLが利用できるようになる。これだけでも簡単な処理には十分。

## パターンマッチ

```ruby 
regex_match  = /\w+/.r
string_match = 'test'.r
number_match = prim :int32
```

Regexや文字列に追加される .r メソッドを呼ぶことで、Rsecのパターンを作ることができる。マッチすると、マッチした文字列が返る。
ブロックを渡すか、mapメソッドを呼ぶことで、マッチしたときのアクションを変更できる。

```ruby 
> t = 'test'.r.map{|s| {:matched => s}}
> t.parse 'test'
=> {:matched => "test"}
```

文字列のパースは parseもしくは parse!。失敗したときの挙動がことなる。失敗したときにどの解析に失敗したかを分かりやすく
するために、failメソッドを使う。

```ruby
> t = 'abc'.r.fail 'abc'
> t.parse 'ab'
INVALID_TOKEN
> t.parse! 'ab'
in source:1 at 1, expect token [ abc ]
ab
 ^
```

## 組み合わせ

上記の基本的なパターンを組み合わせて、より複雑なパターンを構成できる。まずは最も基本的な、連接。
連接はseqを使う。seqはデリミタなし。seq_は、デフォルトで空白をデリミタとする。skip: でデリミタを指定できる。
マッチした配列を返す。

```ruby
> t = seq_('a','b','c', skip: ';')
> t.parse 'a;b;c'
 => ["a", "b", "c"]
```

2項の繰り返しは、joinを使っても書ける。これは、 a, b, c, ...といった任意個数の連接の解析に使える。

```ruby
> t = /[\w\* ]+/.r.join(':')
> t.parse 'root:*:0:0:System Administrator'
 => ["root", ":", "*", ":", "0", ":", "0", ":", "System Administrator"]
```

選択は "|" を使う。選択は左から順に試されることに注意

```ruby
> t = 'aaa'.r | 'aa'.r | 'a'.r
> t.parse 'aa'
=> 'aa'
> t = 'a'.r | 'aa'.r | 'aaa'.r
> t.parse 'aa'
=> 'a'
```

繰り返しは .star 、または *(n) を使う

```ruby
> t = 'a'.r.star
> t.parse ''
 => []
> t.parse 'aaa'
 => ["a","a","a"]
> t = 'a'.r * 5
> t.parse 'aaaaa'
 => ["a", "a", "a", "a", "a"] 
> t2 = t.map(&:join)
> t2.parse 'aaaaa'
 => "aaaaa"
```

# 選択

基本的にマッチしたすべての箇所が配列で返るのだが、それをいちいち[n]やブロックで必要なところだけとるのは面倒なので、
簡略記法がある。

```ruby
> t = one_of('+-') >> /\d+/.r # one_ofはどれか一文字の選択。 >> は、右辺の結果のみを返す
> t.parse '+1234'
 => "1234"

> t = '('.r >> /\w+/.r << ')'.r
> t.parse '(  test  )' # <<は、空白を無視する
 => "test"
```

joinでは、繰り返しの左側、右側のみを取得する .odd, .even がある。

```ruby
> t = /[\w\* ]+/.r.join(':').even
> t.parse 'root:*:0:0:System Administrator'
 => ["root", "*", "0", "0", "System Administrator"]
> t = ':'.r.join(/[\w\* ]+/).odd
> t.parse ':root:*:0:0:System Administrator:'
 => ["root", "*", "0", "0", "System Administrator"]
```

## Gist

基本は上記の通りで、それをベースにcreate table文(db2)をパースして、属性とその型の一覧を出力するサンプル

{% gist 8488424 tableparse.rb %}