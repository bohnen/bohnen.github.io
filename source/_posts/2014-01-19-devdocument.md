---
layout: post
title: "開発ドキュメント"
date: 2014-01-19 00:11:45 +0900
comments: true
categories: [PM, Document]
---
開発時に作成するドキュメントについての調査メモ。
特に開発チームが同一の場所で作業を行っていない場合、コミュニケーションを補う手段としての
ドキュメントや、チームで決めたことの記録としてのドキュメントが重要になってくる。

そういうドキュメントのガイドラインを作ろうと考えたので、調べたことをメモ。
<!--more-->

## 背景

下記のJoel on Softwareにあるような例は実際に多い。（個人的にも痛い目を見た）。
少なくともシステムを作るのであれば、設計は個人で行うものではないし、設計書を全く書かずに進めるべきではないと思っている

しかし、そもそも開発時のドキュメントとは、何を書くべきなんだろうか。できるだけ負担が少なく、
それでいて効果的なドキュメントを書きたいが、それはどんなものだろうか。

## Joel on Software

* [Painless Functional Specifications Part1: Why Bother?](http://www.joelonsoftware.com/articles/fog0000000036.html)

この記事では、全く仕様を書かないSpeedyと、仕様が決まらないとコーディングをしないMr.Rogerという
架空の人物の話を通じて、仕様を書く理由として下記を上げている。

1. 自然言語で書く仕様は、短期間で複数の仕様検討（可能な実装バリエーションの検討）が可能である。
	プログラミング言語では、これが週の単位になってしまう上に、どんなダメな実装になろうとも、その期間は実装に張り付かなければならない。
2. コミュニケーションの時間を短縮する。仕様を一度書いてしまえば、説明は一回で済む。

仕様がないことの弊害がその後も述べられているが、下記のような状況を何度も見たことがある。
政治的な理由とあるが、大体のところは「よく分からない領域について意見を言いたくない」「口を出せば仕事が増える」
「決めたら責任を取らなければいけなくなる」みたいな、消極的な理由によるものだ。

> In too many programming organizations, every time there's a design debate, 
> nobody ever manages to make a decision, usually for political reasons. 
> So the programmers only work on uncontroversial stuff. 
> As time goes on, all the hard decisions are pushed to the end. 
> 
> - Painless Functional Specificaions Part1: Why Bother?

> 本当に多くの開発組織で、設計で議論になったとき、誰もが決定をしようとしない。通常は政治的な理由によるものだ。
> そのためプログラマは反対意見のない作業ばかりやることになる。そうこうしているうちに、全ての困難な決定は後回しにされる。
> 
> - Painless Functional Specificaions Part1: Why Bother? より引用


## なにを書くべきか

[Painless Functional Specifications - Part 2: What's a Spec?](http://www.joelonsoftware.com/articles/fog0000000035.html) には、下記が例としてあげられている。

1. A disclaimer (免責事項)
2. An author. One author (1人の著者)
3. Scenarios (利用シナリオ)
4. Nongoals (目指さないもの)
5. An Overview (概要)
6. Details, details, details (詳細)
7. Open Issues (未解決の課題)
8. Side notes (読者に応じた付加情報)
9. Specs Need To Stay Alive (常に更新)



