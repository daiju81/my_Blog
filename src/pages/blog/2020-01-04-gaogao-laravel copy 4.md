---
templateKey: 'blog-post'
title: 'Just in: small batch of Jamaican Blue Mountain in store next week'
date: 2017-01-04T15:04:10.000Z
featuredpost: true
description: >-
  We’re proud to announce that we’ll be offering a small batch of Jamaica Blue
  Mountain coffee beans in our store next week.
tags:
  - jamaica
  - green beans
  - flavor
  - tasting
---
# ログイン・会員登録不要！の画像投稿SNSアプリを自作した！（非同期）

## はじめに

このたび、画像共有SNSアプリ（通称treap）をデプロイしました。
下記サービスURLです。詳細は後述しますが、このURLにアクセスすればすぐに画像投稿できます。
1枚だけでもよろしければ！会員登録。ログインは一切必要ありません！
[treap-画像投稿URL-](https://newtreap.herokuapp.com/top?access_url=1525e4df64119a38Gname=SAMPLE)

大学で4年間情報工学を学び新卒でSEを経験してから、プログラムを書きたいため退職し勉強中です。プログラミング技術を磨いてきた今までの一つの集大成です笑

ぜひ使ってみてください。それでは詳しい説明をして行きます。

## treapとは？

<figure class="wp-block-video"><video controls="" src="https://daiju81.com/wp/wp-content/uploads/2020/02/画面収録-2020-02-20-11.12.45.mov"></video></figure>

一言で言うとログイン・会員登録不要の画像投稿サービスです。

グループを作成するとURLが発行され、それを共有するだけです。

発行されたURLをTwitter・ラインで共有するだけでグループに入室でき匿名で画像を投稿・閲覧できます。

## 画像の投稿（共有）方法

<figure class="wp-block-image size-large">![](https://daiju81.com/wp/wp-content/uploads/2020/02/スクリーンショット-2020-02-20-12.50.16-1024x451.png)</figure>

①で投稿したい**画像を選択**し（現在は1枚のみ、今後複数枚対応）

②のボタンで画像送信ボタンを押すと**投稿完了**です。

画像が投稿されると非同期で画像の表示が行われます。

[treap-画像投稿URL-](https://newtreap.herokuapp.com/top?access_url=1525e4df64119a38Gname=SAMPLE)

## treapの使用技術

* Laravel6
* PHP 7.3.11
* JavaScript/ajax

## これからの展望

このアプリはよりリアルに皆さんの意見を反映したいのでGitHubにオープンソースとして公開しております！是非プルリクを！

[https://github.com/daiju81/treap](https://github.com/daiju81/treap)