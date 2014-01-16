---
layout: post
title: "blog with octopress"
date: 2014-01-16 22:01:32 +0900
comments: true
categories: [Octopress]
---
blogをgithub pagesとoctopressでつけはじめたので、そのメモ。

<!--more-->

# インストール

まず、github pagesの準備。<ユーザー名>.github.io というリポジトリを作成しておく。

## Otcopressインストール

```bash 
$ git clone https://github.com/imathis/octopress.git
$ cd octopress
$ gem install bundler # 元々入っていたのでやってない
$ bundle install 
$ bundle exec rake install # デフォルトテーマのインストール
```

## github pages対応

```bash 
$ bundle exec rake setup_github_pages
```

ここで、github pagesのURLを聞かれるので、<ユーザー名>.github.io リポジトリの git: か https: のURLを入力

## ページ生成

```bash
$ bundle exec rake generate
$ bundle exec rake preview
```

ここで localhost:4000 にアクセスすると、初期ページが見える。

# テーマのインストール

デフォルトのテーマは暗くてちょっと嫌だったので、[ここ](http://opthemes.com/) から、octostrap3というテーマをチョイス。

```bash 
$ git clone https://github.com/kAworu/octostrap3 .themes/octostrap3
$ bundle exec rake install['octostrap3']
$ bundle generate
```

# 記事を書く

```bash 
$ bundle exec rake new_post['title']
```

# プレビュー

```bash 
$ bundle exec rake generate
$ bundle exec rake preview
```

サーバが立ち上がっているときに記事を編集すると、勝手にgenerateしてくれる。

# デプロイ

```bash 
$ bundle exec rake deploy
```

# コミット
```bash 
$ git add . 
$ git commit -m "hoge"
$ git push origin source # bundle exec rake push でもいいのかな...?
```

# おまけ
* sublime Text2でmarkdownを編集するいいプラグインがないかなと思って、markdowneditingを最初に試したが、
日本語入力のときに改行が入ることがあって結局使わないことにした。
* 現在はmarkdown extendedを使っている。

# 参考文献
1. [octopress](http://octopress.org/)
2. [30分のチュートリアルでJekyllを理解する](http://melborne.github.io/2012/05/13/first-step-of-jekyll/)
3. [markdownediting](http://sublimetext-markdown.github.io/MarkdownEditing/#gfm-spesific-features)
4. [markdown Extended](https://github.com/jonschlinkert/sublime-markdown-extended)