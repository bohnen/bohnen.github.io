---
layout: post
title: "開発ドキュメント(技術仕様)"
date: 2014-01-20 08:31:55 +0900
comments: true
categories: [PM, Document]
---
前回に引き続き、開発ドキュメントについてのメモ。
<!--more-->

## google WebSocket Design Doc

blog等でよく設計ドキュメントとして上げられている例で、[WebKit WebSocket design doc](https://docs.google.com/document/d/1s1ryja1V8dDotMK2WBGT2wnwchZ_x7Tag2L3OZfn5Po/preview) がある。
Googleは開発時に必ず設計ドキュメントを作成する必要があるらしい。

これは前述のJoel on Softwareの分類だと、技術仕様に相当するドキュメントと考えられる。
開発者が主に他の開発者への情報共有として記載するドキュメントのようだ。

個人的な経験から、この手の技術ドキュメントは軽視される傾向にあるが、必ず無いことを後悔することになる。
後悔するのは主に下記の点になる。

* 明らかな設計の誤りを誰も指摘せずそのまま実装されてしまうこと。設計の誤りは様々な種類があるが、
機能仕様が実現できないことと、作りがまずいことの2つが大部分を占める。この2つはしかし、的確なレビューによって
未然に防ぐことができる。

* 他の誰にも理解できない実装（もしくは、理解コストが高くなり理解する気が失せるといってもいい）実装になり、
実装だけならまだしも、障害対応のメンバーの固定化を招いてしまう。

こういったドキュメントの必要性は、もちろんメンバーの人数や仕事の形態（同一箇所の開発か、遠隔地か）に
よっても異なるが、「＊＊さんに聞かないとちょっとわからないなぁ」という会話が頻繁に（個人的には1度でも）聞かれるようだと、必要だと認識した方がよい。

## 記載事項

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

もちろん、著者のクレジットも記載されている。

## サマリー

まとめると下記のようになると思う

|         | 機能仕様			| 技術仕様  						
|:--------|:---------:	|:--------:						
|When     | 機能検討時		| 実装前     					
|What     | 機能について	| 実装の概要について 		
|Who      | 機能検討者		| 実装者 							
|Whom     | 機能提案者		| 機能検討者, 他の実装者	


## 参考文献
1. [WebKit WebSocket design doc](https://docs.google.com/document/d/1s1ryja1V8dDotMK2WBGT2wnwchZ_x7Tag2L3OZfn5Po/preview)
2. [Game Design Document](https://docs.google.com/document/d/1ct5-qyUZC9cAKn-iLUgtOczDkERmPzNNwPLDfT9Hgjs/preview#)
3. [Joel on Software](http://www.joelonsoftware.com/articles/WhatTimeIsIt.html)
4. [Joel on Software](http://www.joelonsoftware.com/articles/fog0000000035.html)
5. [Software Engineer in Google](http://www.youtube.com/watch?v=pc-IQkVmOdI)