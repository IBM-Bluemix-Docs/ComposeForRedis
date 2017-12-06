---

copyright:
  years: 2017
lastupdated: "2017-06-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 外部アプリケーションの接続
{: #connecting-external-app}

外部アプリケーションを {{site.data.keyword.composeForRedis_full}} に接続する方法は 2 つあります。

- **接続ストリング**: いくつかのクライアント・ライブラリーで使用できます。他のライブラリーが接続するために必要なすべての情報、具体的にはホスト名とポートが含まれています。

- **コマンド・ライン**: 正しいパラメーターを使用して `redis-cli` を呼び出すために予め形式設定されたコマンドです。

両方とも {{site.data.keyword.composeForRedis}} サービスの*概要*ページに表示されます。

## コマンド・ラインによる接続

通常は、`redis-cli` コマンドを使用してデプロイメントに手動で接続します。これは Redis のインストール環境をリモートから最も直接的に使用できる方法です。このコマンドは Redis パッケージに含まれているので、使用するには Redis をローカルにインストールする必要があります。Mac OS X の場合は、Homebrew を使用して Redis を入手することをお勧めします。

1. [brew](http://brew.sh) をインストールします
2. `brew install redis` を使用して redis をインストールして実行します。

Linux の場合は、配布パッケージ・マネージャーで最新のビルドを確認します。必要に応じて、[ソースをダウンロード](http://redis.io/download)して自分でビルドできます。 

TCP コマンド・ラインを取得してターミナルにカット・アンド・ペーストします。
```shell
$ redis-cli -h portal.brilliant-redis-41.compose-3.composedb.com -p 15639 -a secretpassword
portal.brilliant-redis-41.compose-3.composedb.com:15639> set hello "world"
OK
portal.brilliant-redis-41.compose-3.composedb.com:15639> get hello
"world"
portal.brilliant-redis-41.compose-3.composedb.com:15639> 

```
次のようにシンプルな Redis コマンドをいくつか実行して、接続をテストできます。
## アプリケーションを使用した接続

公式の Redis クライアント・ライブラリーはありません。Redis のサイトには、多く言語のためのクライアント・ライブラリーが多数リストされています。完全なリストは[こちら](http://redis.io/clients)から確認できます。推奨クライアントには星印が付いています。すぐに始められるように、推奨クライアントのセレクションを次に示します。       

言語|ライブラリー|接続ストリングの利用
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[はい](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[はい](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|はい - [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details)、[2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html) を参照

また、[Compose ブログ](https://www.compose.com/articles/)にも、一般的に使用されている幅広い言語の推奨ドライバーが記載された Compose 記事 [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) があります。
