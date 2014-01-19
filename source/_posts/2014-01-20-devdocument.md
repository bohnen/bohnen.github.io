---
layout: post
title: "開発ドキュメント_2"
date: 2014-01-20 08:31:55 +0900
comments: true
published: false
categories: [PM, Document]
---
前回に引き続き、開発ドキュメントについてのメモ。blog等で言及している例について調べる。
<!--more-->

## google WebSocket Design Doc

Googleは開発時に必ず設計ドキュメントを作成する必要があるらしい。

よく例にあげられている、googleのWebSocket Design Doc(参考文献1)を見てみる。何が書いてあるかというと

1. Objective (目的)
2. Background (背景)
3. High Level Structure (ハイレベル構造）
4. WebCore Classes 
5. Flows （処理フロー）
6. JavaScript binding
7. Platform code requirements
8. Layout Test Plan
9. Security Considerations
10. Open Issues (未解決の課題)
11. Reference (参考文献)
12. Document History (改訂履歴)

## 検討事項
When, What, Who, Whom, Where, How.

* いつ書くドキュメントか
* 何を書くか
* 誰が書くか
* 誰が読むか、レビューするか
* 対象は何か
* どうやって書くか

* メンテナンス。実装との乖離はどうするか?

## ツール

## 参考文献
1. [WebKit WebSocket design doc](https://docs.google.com/document/d/1s1ryja1V8dDotMK2WBGT2wnwchZ_x7Tag2L3OZfn5Po/preview)
2. [Game Design Document](https://docs.google.com/document/d/1ct5-qyUZC9cAKn-iLUgtOczDkERmPzNNwPLDfT9Hgjs/preview#)
3. [Joel on Software](http://www.joelonsoftware.com/articles/WhatTimeIsIt.html)
4. [Joel on Software](http://www.joelonsoftware.com/articles/fog0000000035.html)
5. [Software Engineer in Google](http://www.youtube.com/watch?v=pc-IQkVmOdI)