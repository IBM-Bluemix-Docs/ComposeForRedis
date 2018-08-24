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
  - TLS/SSL 対応接続の接頭部は「rediss:」になります。 ほとんどの言語には、TLS/SSL でのアプリケーションの接続をサポートするドライバーがあります。 
  - 非暗号化接続の接頭部は「redis:」になります。 これは、ドライバーが暗号化を処理しない場合に使用できますが、暗号化されないトラフィックにはリスクが潜んでいる可能性があることを意識しておく必要があります。 

- **コマンド・ライン**: 正しいパラメーターを使用して `redis-cli` を呼び出すために予め形式設定されたコマンドです。
  - オープン・ソースの Redis には TLS/SSL サポートが組み込まれていないので、Redis のコマンド・ライン・ユーティリティーである `redis-cli` でこの接続を使用するには、追加の構成が必要になります。
  - `redis-cli` では、ネイティブに非暗号化接続を使用できます。追加の構成は不要です。

{{site.data.keyword.composeForRedis}} サービスの*「概要」*ページには、**「接続ストリング」**と**「コマンド・ライン」**の両方が表示されます。


## コマンド・ラインによる接続

通常は、`redis-cli` コマンドを使用して、デプロイメントに手動で接続します。これが、Redis のインストール済み環境をリモートから操作するための最も直接的な方法です。 このコマンドは Redis パッケージに含まれているので、使用するには、ローカル環境にこのパッケージをインストールする必要があります。 ソースをダウンロードしてコンパイルするには、[Redis のダウンロード・ページ](http://redis.io/download)にある手順に従ってください。

### 暗号化されていない接続

Redis が TLS 暗号化で保護されていない場合、つまり、接続ストリングに `redis:` が表示される場合は、表示された**「コマンド・ライン」**フィールドの文字列を端末に貼り付けてください。
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
次のようにシンプルな Redis コマンドをいくつか実行して、接続をテストできます。

### TLS /SSL 対応接続

暗号化された接続で `redis-cli` を使用するには、redis-cli 接続を TLS 暗号化でラップできる `stunnel` などのユーティリティーをセットアップします。 [stunnel](https://www.stunnel.org/index.html) をセットアップする手順は、以下のとおりです。

1. stunnel をインストールします。
    
    Linux 用のパッケージ・マネージャー、Mac 用の Homebrew を使用するか、ご使用のプラットフォームに適した[ダウンロード](https://www.stunnel.org/downloads.html)を取得します。

2. **「接続ストリング」**を解析します。 例えば、以下のような接続ストリングがあるとします。
   ```text
   rediss://admin:PASSWORD@portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
   ```
   2 番目のコロンとアットマークの間のテキストがパスワードです。 @ の後の次のコロンまでのテキストがホスト、そのコロンの後の番号がポート番号です。 つまり、この例では、`PASSWORD` がパスワード、`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com` がホスト、`24370` がポートです。

3. この構成情報を stunnel.conf ファイルに追加します。 この構成は、サービスの名前 (`[redis-cli]`)、この stunnel が TLS クライアントになるという設定 (`client=yes`)、接続を受け入れて接続する IP アドレスとポート (`accept=127.0.0.1:6830`)、接続しようとしているホスト名とポート (`connect=`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370`) です。
    ````text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
    ```
    末尾が `composedb.com` であるデプロイメントでは、Let's Encrypt 証明書が使用されるので、これ以上の操作は必要ありません。 末尾が `dblayer.com` である場合は、自己署名証明書があるので、概要の*「SSL 証明書」*タブから証明書情報を取得し、それをすべてテキスト・ファイル (`cert.crt` など) にコピーする必要があります。 そして、その証明書情報へのパスを stunnel.conf ファイルに追加します。
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    verify=2  
    checkHost=sl-us-south-1-portal.7.dblayer.com 
    CAfile=/path/to/redis/cert.crt
    ```

3. stunnel を実行します。コマンド・ラインで `stunnel` コマンドを入力します。 すぐにバックグラウンドで実行されます。
    
4. 新しい端末ウィンドウで、ローカル・ホストとポートを指定した `redis-cli` を実行し、デプロイメントの資格情報で認証します。
    ```shell
    redis-cli -p 6830 -a <password>
    ```

## アプリケーションを使用した接続

公式の Redis クライアント・ライブラリーはありません。 Redis のサイトには、多く言語のためのクライアント・ライブラリーが多数リストされています。 完全なリストは[こちら](http://redis.io/clients)から確認できます。 推奨クライアントには星印が付いています。 すぐに始められるように、推奨クライアントのセレクションを次に示します。       

言語|ライブラリー|接続ストリングの利用
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[はい](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[はい](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|はい - [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details)、[2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html) を参照

また、[Compose ブログ](https://www.compose.com/articles/)にも、一般的に使用されている幅広い言語の推奨ドライバーが記載された Compose 記事 [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) があります。
