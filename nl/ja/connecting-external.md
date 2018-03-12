---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-22"
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
  - TLS/SSL 対応接続の接頭部は「rediss:」になります。ほとんどの言語には、TLS/SSL でのアプリケーションの接続をサポートするドライバーがあります。 
  - 非暗号化接続の接頭部は「redis:」になります。 これは、ドライバーが暗号化を処理できない場合に使用できますが、暗号化されないトラフィックにはリスクが潜んでいる可能性があることを意識しておく必要があります。 

- **コマンド・ライン**: 正しいパラメーターを使用して `redis-cli` を呼び出すために予め形式設定されたコマンドです。
  - オープン・ソースの Redis には TLS/SSL サポートが組み込まれていないので、Redis のコマンド・ライン・ユーティリティーである `redis-cli` でこの接続を使用するには、追加の構成が必要になります。
  - `redis-cli` では、ネイティブで (追加の構成なしで) 非暗号化接続を使用できます。

{{site.data.keyword.composeForRedis}} サービスの*「概要」*ページには、**「接続ストリング」**と**「コマンド・ライン」**の両方が表示されます。


## コマンド・ラインによる接続

通常は、`redis-cli` コマンドを使用して、デプロイメントに手動で接続します。これが、Redis のインストール環境をリモートから操作するための最も直接的な方法です。このコマンドは Redis パッケージに含まれているので、使用するには、ローカル環境に Redis をインストールする必要があります。ソースをダウンロードしてコンパイルするには、[Redis のダウンロード・ページ](http://redis.io/download)にある手順に従ってください。

### TLS /SSL 対応接続
暗号化接続で `redis-cli` を使用するには、暗号化を処理する `stunnel` などのユーティリティーをセットアップする必要があります。[stunnel](https://www.stunnel.org/index.html) をセットアップする手順は、以下のとおりです。

1. stunnel をインストールします。
    
    Linux 用のパッケージ・マネージャー、Mac 用の Homebrew を使用するか、ご使用のプラットフォームに適した[ダウンロード](https://www.stunnel.org/downloads.html)を取得します。

2. **「コマンド・ライン」**フィールドの情報を stunnel.conf ファイルに追加します。
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    ```
    
    デプロイメントに自己署名証明書がある場合は、証明書の情報を stunnel.conf ファイルに追加する必要があります。
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    verify=2  
    checkHost=sl-us-south-1-portal.7.dblayer.com 
    CAfile=/path/to/redis/cert.crt
    ```

3. stunnel を実行します。
    
    コマンド・ラインで `stunnel` コマンドを入力します。すぐにバックグラウンドで実行されます。
    
4. ローカル・ホストとローカル・ポートを指定した `redis-cli` を実行し、デプロイメントの資格情報で認証します。

    ```shell
    redis-cli -p 6830 -a <password>
    ```

### 非暗号化 HTTP 接続
**「コマンド・ライン」**フィールドのストリングを端末に貼り付けます。
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
次のようにシンプルな Redis コマンドをいくつか実行して、接続をテストできます。 


## アプリケーションを使用した接続

公式の Redis クライアント・ライブラリーはありません。 Redis のサイトには、多く言語のためのクライアント・ライブラリーが多数リストされています。 完全なリストは[こちら](http://redis.io/clients)から確認できます。 推奨クライアントには星印が付いています。 すぐに始められるように、推奨クライアントのセレクションを次に示します。       

言語|ライブラリー|接続ストリングの利用
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[はい](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[はい](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|はい - [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details)、[2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html) を参照

また、[Compose ブログ](https://www.compose.com/articles/)にも、一般的に使用されている幅広い言語の推奨ドライバーが記載された Compose 記事 [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) があります。
