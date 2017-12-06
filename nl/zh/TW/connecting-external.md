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

# 連接外部應用程式
{: #connecting-external-app}

將外部應用程式連接至 {{site.data.keyword.composeForRedis_full}} 的方式有兩種：

- **連線字串**可由某些用戶端程式庫使用，且包含其他程式庫進行連接時所需的一切資訊；尤其是主機名稱及埠。

- **指令行**是一個預先格式化的指令，它會使用正確的參數來呼叫 `redis-cli`。

您將在 {{site.data.keyword.composeForRedis}} 服務的*概觀* 頁面上找到這兩者。

## 使用指令行連接

通常您將使用 `redis-cli` 指令手動連接至部署 - 這是遠端使用 Redis 安裝的最直接方式。它是 Redis 套件的一部分，所以您必須在本端安裝 Redis，才能使用它。在 Mac OS X 上，取得 Redis 的好方法是使用 Homebrew。

1. 安裝 [brew](http://brew.sh)
2. 使用 `brew install redis` 來安裝 Redis，以開始進行。

在 Linux 上，請參照您的配送套件管理程式，以取得最新的建置。如果您要這麼做，可以[下載原始檔](http://redis.io/download)並自行建置。 

採用「TCP 指令行」，然後將它剪下並貼至您的終端機，如下所示：
```shell
$ redis-cli -h portal.brilliant-redis-41.compose-3.composedb.com -p 15639 -a secretpassword
portal.brilliant-redis-41.compose-3.composedb.com:15639> set hello "world"
OK
portal.brilliant-redis-41.compose-3.composedb.com:15639> get hello
"world"
portal.brilliant-redis-41.compose-3.composedb.com:15639> 

```
您可以執行某些簡單的 Redis 指令來測試連線，如下所示。

## 使用應用程式連接

沒有官方的 Redis 用戶端程式庫。Redis 網站上列出的許多語言有多種用戶端程式庫。您可以在[這裡](http://redis.io/clients)看到完整清單。建議的用戶端會以星號標示。如果您想要快速啟動，建議選取的用戶端如下：       

語言|程式庫|使用連線字串
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[是](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[是](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|是 - 請參閱 [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details)、[2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

在 Compose 文章中也有 [Redis 入門之旅](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/)。您可以在 [Compose 部落格](https://www.compose.com/articles/)中查看針對更廣泛常用語言建議的驅動程式。
