---
layout: post
title:  "Tor(ディープウェブ/ダークウェブ)にブログを作成する方法"
date:   2018-09-18 09:00:00 +0900
categories: blog
---


ハロー皆さん。スカーレットです。

今回は皆さん知りたいだろうなーっていう、Torにブログとかウェブサイトを作成する方法を教えてあげたいと思います。

今この記事が書かれているこのサイトも、おそらくですが！今回ご紹介するやり方で作成されたものになっているはずです。ので！ご参照頂ければと思いますー。

## 導入 セキュリティと匿名性の問題

今回紹介する方法では、環境として、

* ubuntu 18.04
* nginx
* jekyll

をメインとして使っています。

何故この構成なのかというと、簡単だからです。それだけです。セキュリティ的にも、問題ありません。

### なぜubuntuなのか

簡単だからです。

本音を言うと、一番安全なのはwhonixです。続いてdebianです。

ubuntuはインストールも簡単だし、情報も多いし、そもそもHTMLページ見せるくらいだったらあんま問題ないです。気にしなくて👍

### なぜnginxなのか

セキュリティとかハッキング攻撃に強いからです。
apacheじゃなくてnginxにしましょうね。

### なぜjekyllなのか

jekyllとは、静的HTMLサイトを生成するRubyのライブラリです。

なぜWordPressではなく、jekyllなのか。ですが、

単純にWordPressは脆弱性問題が多いからです。

それに、動的サイトがセキュリティリスクがあるため、オススメできませんのです。

HTMLページをいちいちアップロードしていく方法が一番なんですね。

### なぜVPSや有料のサーバーを使わないのか

Torのhidden serviceをホスティングしてくれるサービスはたくさんあり、それを利用しているサービスも多いですね。
しかしそれを利用しない理由は何でしょうか。

* お金がかかる
* 支払いに利用するビットコインに関する幅広い知識が必要
* ホスティングしているサーバーがハッキングされると自分のサイトも被害を受ける
* そもそも大手のホスティングサービスが潰れたりしていて信用に値するサイトが少ない

といったところです。

## 本題 Ubuntu 18.04 nginx jekyllでTorにブログを作成する方法

まずは。ubuntu 18.04をvirtualboxにインストールしましょうね。これは調べてね。

SSHで作業していくから、`sudo apt install openssh-server`しとこうね。

[Create a Tor Website on Ubuntu – TheCloud.org.uk](https://thecloud.org.uk/create-tor-hidden-service-website-ubuntu-linux/)がとてもわかり易かったよ！この記事を簡潔にご紹介するね。

ウェブサーバーnginxの設定をするよ！

```sh
# インストール
sudo apt install nginx

# ファイルをまるごと書き換え！
cat > /etc/nginx/sites-available/default
server {
       listen 127.0.0.1:8080 default_server;
       server_name localhost;
       root /usr/share/nginx/html;
       index index.html index.htm;
       location / {
               allow 127.0.0.1;
               deny all;
       }
}

```

`lsb_release -a`でubuntuのバージョンを確認しよう。

> Then visit this link and select your Linux version and codename from the drop down menu.

次に、[Tor Project: Debian/Ubuntu Instructions](https://www.torproject.org/docs/debian.html.en#ubuntu)へ行って、バージョンごとのTorのインストール方法を確認してみよう。

今回は、Ubuntu 18.04の場合を紹介するよ。

```sh
# ソースファイルに追記！
cat >> /etc/apt/sources
deb https://deb.torproject.org/torproject.org bionic main
deb-src https://deb.torproject.org/torproject.org bionic main

# rootで作業するよ
sudo su -
gpg2 --recv A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89
gpg2 --export A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89 | apt-key add -

apt update
apt install tor deb.torproject.org-keyring

```

torrcに追記

```sh
sudo nano /etc/tor/torrc

HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 80 127.0.0.1:8080
```

最後！

```sh
sudo service nginx restart
sudo service tor restart

cat /var/lib/tor/hidden_service/hostname
```

ドメイン名が出力されましたか？これをTorに入力してページを見てみましょう！

映ったよね！

次、jekyllいきます。

まずjekyllのブログ作ります。
jekyllはまた他の、開発用の仮想環境で構築しています。こっちのほうがやりやすいからね。

```sh
sudo apt install jekyll
cd ~/tmp
jekyll new www
cd www
jekyll build
```

デプロイしますね。
開発環境から、本番環境の先ほどnginxの設定をしたubuntuにファイルをコピーします。

```sh
rsync --rsync-path="sudo rsync" -av -e 'ssh' _site/ user@192.168.99.100:/usr/share/nginx/html
```

では先程のonionドメインのページを更新してみましょう。

nginxのページから、welcomeページに変わったかな？

おめでとう👍これで君もダークウェブブロガーだよ。

## まとめ

今回はダークウェブにブログを作る方法を紹介しました。

ぜひこの記事を活用してくれれば嬉しく思います。では！！
