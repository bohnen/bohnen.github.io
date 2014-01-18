---
layout: post
title: "Octopressの設定"
date: 2014-01-18 22:25:32 +0900
comments: true
categories: [Octopress]
---
Octopressでいくつかblogを書いたので、カスタマイズに着手。カスタマイズ点をメモ。
<!--more-->

## サイドバー

サイドバーの設定は、_config.ymlのdefault asidesに説明が書いてある。
/source/_includes/custom/asides/ にサイドバーに表示したいhtmlスニペットを配置して、default asidesに
custom/asides/foo.html のように書けば良い。

とりあえずデフォルトabout.me が置いてあるので、これを修正してプロフィールが表示できるようにした。

## カテゴリリスト

https://github.com/tokkonopapa/octopress-tagcloud からタグクラウド pluginをダウンロードして利用。
ただ、bootstrap3 のテーマでは、Recent postを見る限り divタグとaタグで構成されているので、
このプラグインではulタグを使っているのでそのままでは見栄えが悪い。Recent postと一致するように、プラグインを書き換えて対応。

```ruby
#        html << "<li><a href='/#{category_dir}/#{category.to_url}/'>#{category}"
        html << "<a class='list-group-item' href='/#{category_dir}/#{category.to_url}/'>#{category}"
        if @opts['counter']
          html << " (#{categories[category].count})"
        end
#        html << "</a></li>"
        html << "</a>"
```

## google analytics, disqus

トラッキングIDとショートネームを _config.yml に書けば使える。

## haml

hamlプラグインなるものが最初から入っており、.hamlを.htmlにコンバートしてくれるみたいだが、サイドバーを
hamlで書いて generateしても htmlファイルはできなかった。ぐぐって察するところによると、markdownの代わりに.haml を
使うと変換してくれるみたいだが、markdownの方が100倍楽だし見やすいのでこのままにする。

サイドバーは手でhaml実行してhtml生成した。プラグインの対象ディレクトリを広げることができれば良さそうだが、
Jekyllのplugin仕様をしらべないといけない。めんどい。プラグイン自体を作ることはそんなに面倒ではなさそうなので、
暇があったらやってみよう。

