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
# [laravel] view作成時の(@include/@yield/@section)の違い

## はじめに

laravelでwebアプリを作成している時に@include/@yield/@sectionの違いが気になったので調べてみた。

## @includeとは？

まずは、公式リファレンスを見てみる。

> Blade's `@include` directive allows you to include a Blade view from within another view. All variables that are available to the parent view will be made available to the included vi
> 
> <cite>https://laravel.com/docs/6.x/blade</cite>

要約すると、@includeを使用すると、別のBladeファイルを使えるようになりますということ。

## @yieldとは？

公式リファレンスをみてみる。

> When defining a child view, use the Blade `@extends` directive to specify which layout the child view should "inherit". Views which extend a Blade layout may inject content into the layout's sections using `@section` directives. Remember, as seen in the example above, the contents of these sections will be displayed in the layout using `@yield`:
> 
> <cite>[https://laravel.com/docs/6.x/blade](https://laravel.com/docs/6.x/blade)</cite>

つまり、@yieldを使用すると別のBladeテンプレートからコンテンツを挿入して、テンプレートを拡張することができますということ。

## @sectionとは？

> When defining a child view, use the Blade `@extends` directive to specify which layout the child view should "inherit". Views which extend a Blade layout may inject content into the layout's sections using `@section` directives. Remember, as seen in the example above, the contents of these sections will be displayed in the layout using `@yield`:
> 
> <cite>[https://laravel.com/docs/6.x/blade#extending-a-layout](https://laravel.com/docs/6.x/blade#extending-a-layout)</cite>

つまり、@sectionを使用すると別のBladeテンプレートからコンテンツを挿入して、テンプレートを拡張することができ、継承もできますということ。
@yieldの継承ができる版のようなイメージだと思います。
@parentを使えば元のBladeテンプレートに追記することができます。

## 具体的な使い方

まずは親テンプレートのソースコードから。

```
<!-- Stored in resources/views/layouts/layout.blade.php --> <!DOCTYPE html> <html lang="ja"> <head> <meta charset="UTF-8"> <meta name="viewport" content="width=device-width, initial-scale=1.0"> <meta http-equiv="X-UA-Compatible" content="ie=edge"> <title>title</title> </head> <body> @include('inc.navbar') @yield('content') @section('footer') footer @show </body> </html>
```

そして、子テンプレートのソースコード 。

```
<!-- Stored in resources/views/home.blade.php --> @extends('layouts.layout') //上記のlayout.blade.htmlを継承 @section('content') <p>コンテンツ</p> @endsection @section('footer') @parent <p>footer追記</p> //上記テンプレートに追記する形になる。 @endsection
```

## @includeの使い方

親テンプレートの@include('inc.navbar')という箇所に下記のコードが挿入されます。これが最初に言った「別のBladeファイルを使えるようになる」と言うこと。
下記のようにnavbarやarticleなど部品ごとに分割して使用することですっきりした記述ができるようになります。

```
<!-- Stored in resources/views/inc/navbar.blade.php --> <nav class="navbar navbar-light bg-light"> <a class="navbar-brand" href="#">Navbar</a> </nav>
```

## @yieldの使い方

```
<!-- Stored in resources/views/home.blade.phpの一部抜粋 --> @section('content') <p>コンテンツ</p> @endsection
```

上記の@section('content')@endsectionの間に記述された内容を親テンプレートの@yield('content')に挿入
今回の場合は「<p>コンテンツ</p>」が挿入される。

## @sectionの使い方

```
<!-- Stored in resources/views/home.blade.phpの一部抜粋 --> @section('footer') @parent <p>footer追記</p> //上記テンプレートに追記する形になる。 @endsection
```

子テンプレートの@section('footer')@endsectionの間に記述された内容を親テンプレートの「@section('footer')」に挿入（これは@yieldと同じ）。
@yieldと異なる点は@parentと記述することで親テンプレートに追記する形になる。(footer, footer追記が表示される。)

## 参考サイト

下記サイトを参考にさせていただきました。

[https://qiita.com/makies/items/2ab24188e7f8482bfddc](https://qiita.com/makies/items/2ab24188e7f8482bfddc)

[https://laravel.com/docs/6.x/blade#extending-a-layout](https://laravel.com/docs/6.x/blade#extending-a-layout)

[https://engineering.mobalab.net/2019/03/08/laravel%E3%81%AE%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%81%A7%E3%81%AEinclude-yield-section%E3%81%AE%E9%81%95%E3%81%84/](https://engineering.mobalab.net/2019/03/08/laravel%E3%81%AE%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%81%A7%E3%81%AEinclude-yield-section%E3%81%AE%E9%81%95%E3%81%84/)

## まとめ

@include/@yield/@sectionの違いを説明していきました。使いこなすとすっきりしたコードになり、手間も減るので慣れておいた方がいいかと思いました。