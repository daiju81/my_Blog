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

# [プログラミング編]この7日間で出会ったエラー・壁・やったことをまとめてみた

ベトナムにきてから 早１週間が過ぎました。

オリジナルtodoアプリ、ユーザー管理アプリ作成、そして、SNSアプリを作成中というように濃密な時間を過ごしています。

この後も、バリバリ作業していきます！！

さてさて、本題ですが今回はこの濃密な7日間に起きたさまざまなエラー・壁を忘れずに記憶として残せるようゆるくアウトプットしていきます。

自分の記憶用なのでだいぶ雑になっちゃってます笑

## 作成したアプリ、ぶつかった壁・エラー集

### 作成した自作アプリ１

まずは、下のtodoアプリを何も参考にせずに作りました。基本的なCRUD（この時は削除は実装しませんでした笑）が理解できてシンプルながらやりごたえはありました。

<figure class="wp-block-embed-twitter wp-block-embed is-type-rich is-provider-twitter">

<div class="wp-block-embed__wrapper">https://twitter.com/daiju08/status/1224290020053307392</div>

</figure>

削除機能追加後

<figure class="wp-block-embed-twitter wp-block-embed is-type-rich is-provider-twitter">

<div class="wp-block-embed__wrapper">https://twitter.com/daiju08/status/1226321086247096320</div>

</figure>

### 作成した自作アプリ2

2つ目はユーザ管理アプリを作ってみました！viewはgithubに乗っている物をお借りしました。これも基本的なCRUDは体験できるので意外とやりごたえはありました。

<figure class="wp-block-embed-twitter wp-block-embed is-type-rich is-provider-twitter">

<div class="wp-block-embed__wrapper">https://twitter.com/daiju08/status/1224719525871939585</div>

</figure>

### アプリを自作した感想

今までは何かのudemyやドットインストールといった教材をみながらプログラミングしていましたが、今回はほぼ何も参考にせずアプリを作ってみました。

やはり、今まで見えてなかった景色が見えました。今までは当たり前のようにやっていた作業なのに参考文献がないとこんなに手が動かないのか？状態になりました、、

ただ、小さいアプリながら自分で0から10までを作り上げる経験をできたのは自身につながりました。やって良かった！

## エラー集

### **htmlspecialchars() expects parameter 1 to be string, object given**

「htmlspecialchars関数は、1つ目の引数に文字列を要求しているのにオブジェクトが指定されてるよ」という意味

#### 解決方法

結論としては、viewで使用している{{}}の中身には配列を入れる場合は要素を指定してあげる必要があったみたい。

下記のサイトがとても分かりやすかった。

> {{ }}内にhtmlspecialcharsに対応しているstring等を入れる必要がある。配列を表示したいのであれば{{$array[i]}}のように一つの要素に絞る必要がある。
> 
> <cite>[https://qiita.com/kuhblume/items/37aa2981de6d36d4d3d7](https://qiita.com/kuhblume/items/37aa2981de6d36d4d3d7)</cite>

### **Illuminate\Database\QueryException : SQLSTATE[HY000] [2002] Connection refused (SQL: select * from information_schema.tables where table_schema = xxxxx and table_name = migrations and table_type = 'BASE TABLE')**

このエラーはDBの接続が拒否されている。

このエラーは非常にシンプルですぐに修正できた。

#### 解決方法

以下2点を確認して、エラーが解決できた

* .envファイルに以下が記述されているか？

```
DB_DATABASE=データベース名 DB_USERNAME=ユーザ名 DB_PASSWORD=パスワード
```

* config/database.phpにunix_socketが記述されているか？

### **Illuminate\Database\QueryException : SQLSTATE[HY000]: General error: 1215 Cannot add foreign key constraint (SQL: alter table `comments` add constraint `comments_post_id_foreign` foreign key (`post_id`) references `posts` (`id`) on delete cascade)**

このエラーは外部キーに関するエラーだった。おそらく以下の2択。

* 外部キーで関連づけているデータ型が同じか？
* マイグレーションファイルの作成順序

よくあるのはuseridがbigincrementsでそれに関連づけているpostのuser_idがbigではなくincrementsだったケース。このようなケースはbigの有無を統一すればいい。以下のサイトが参考になった。

[https://qiita.com/luccafort/items/0e7c61440c15f86fbfa0](https://qiita.com/luccafort/items/0e7c61440c15f86fbfa0)

もう一つよくあるのは、userテーブルを作っていないのにuser_idを関連づけ用としているケース(userテーブルはデフォルトでついているので実際にはuserテーブルの箇所が別のテーブルになると思う)。このような場合は、一旦マイグレーションファイルを消して、順番を考えて作成する必要がある。

### Undefined index: xxxxx

後よく出会うのがこれ。xxxxxが定義されてないやつ。どこかで値や定義する箇所を入れてあげればいい。

これに関してはエラーの意味はわかるが、作成中のアプリのロジックが複雑で解決できないことが多い。

## まとめ

今回はこの1週間でよく出会ったエラーについてまとめてみました。

本当はもっとたくさんありますが、めちゃくちゃ時間かかりそうなのでこの辺にしときます！