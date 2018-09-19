---
layout: post
title:  "Torのブログやサイトをサーフェイスにも同期する方法"
date:   2018-10-10 09:00:00 +0900
categories: blog
---



こんばんは。スカーレットだよ。

このブログはTorとサーフェイスネットの両方で閲覧できるようになっているよ。
それぞれのURLはサイトの一番下に書いてあるから見てみてね。

さて、このTorとサーフェイスにサイトを同期するっていうことだけど、これ、実は結構難しかったよ。

難しいというかなんというか、
考える力が必要がだったかな！

私はこのブログのサーフェイスで公開するのに、Github pagesを選択したけど、他の選択肢もあるっていうのは、詳しい人ならわかるよね！

## ドメインを買う

例えば、とても一般的なやり方だと、ドメインを買って、サーバーやVPSを借りて、サイトを運営する方法。
これが最も、サイトを運用する上では望ましいんだけれど、これはできなかったよ！

なんでかというと、まず、ドメインを買うためには、アイデンティティ、つまり、個人情報が必要だよ。
これはなぜ必要かというと、whois情報とか、だね。

まず私は、この情報を契約時に、存在しないものを書く、または、誰かさんの情報を書く方法を考えたよ。だけど、両方共厳しそうなんだな。

存在しないものを書く方法はまず、すぐにバレてしまうみたい。
いいや、普通の健全なウェブサイトを運営しているぶんには、目をつけられなければバレることはないかもしれない。だけど、法律に抵触するような内容を書いているサイトだったら、「これは誰が書いているんだ！」ってなる可能性が高いよね！

誰かさんの情報を書く方法も同様で、誰が書いているんだ騒ぎになった時点で、書いた人が私のじゃないよーって言ったら、「あれーおかしいなー、とりあえずこのサイトは公開停止処置しよう！」ってなるよね！

だからだめなのですよ。

ただし、独自ドメインで運用する方法はまだあって、無料のドメインを利用する方法だよ。

無料ドメインはメールアドレスだけで取得できるみたいだし、どんなサーバーにもDNSが登録できるみたい。

## サーバーを契約

次に、サーバーの契約の問題だね。

サーバーの契約にも当然だけど、個人情報が必要だよ。
これも、ドメインの理由と同じで、あまり偽装情報を載せるのは好ましくないね。

だけど、サーバーはアノニマスなサーバーがいくつか存在するよ。
ビットコインとメールアドレスだけで契約ができてしまうから、便利だね。

ただし、こういうサーバーはSSHなどの便利な機能が使えない場合があるよ。
また、お金もかかるし、ビットコインの知識も必要だよ。

私がこの手法を取らなかったのは、SSHが使えなかったから、というのが大きいかな！

## 無料ブログ

WordPress.comやWIX、国内なら、アメブロなどがこれにあたるよ！

ただ単に匿名性を保ったままサーフェイスでブログがしたい、というだけなら、WordPress.comでいいと思うよ！

WIXは詳しくないけど、アメブロとかはてなとかは匿名性が必要なことを書いているサイトは容赦なく消されると思うから、おすすめできないね！

しかし、今回の趣旨は、Torのブログをサーフェイスにも同じように表示したい、という趣旨だからね。

WordPress.comじゃ、手動で一つ一つの記事をコピペしていくならともかく、同期はできそうにないね。

## Github pages

最終的に思いついた方法がgithub pagesを利用する方法だよ！

github pagesなら、SSHからコマンドを打つだけでデプロイできるし、
jekyllと相性が良いからね！

それに実質サブドメインだけど、独自ドメインみたいなものだし、いいと思うよ！

相当なこと書かなければ削除されるってことはないと…思うよ！
消されたら消されてから考えようね。

## まとめ

今の所は、github pagesが一番オススメかな！