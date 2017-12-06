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

# 连接外部应用程序
{: #connecting-external-app}

有两种方法可将外部应用程序连接到 {{site.data.keyword.composeForRedis_full}}：

- **连接字符串**可由某些客户机库使用，并包含其他库连接所需的所有信息，具体包括主机名和端口。

- **命令行**是一个预先格式化的命令，它将使用正确的参数来调用 `redis-cli`。

您将在 {{site.data.keyword.composeForRedis}} 服务的*概述*页面上找到这两项。

## 使用命令行进行连接

通常，您将使用 `redis-cli` 命令，以手动方式连接到部署：它是与 Redis 安装远程协作的最直接的方法。它作为 Redis 软件包的一部分提供，因此您需要在本地安装 Redis，才能使用它。在 Mac OS X 上，使用 Homebrew 是获得 Redis 的好方法。

1. 安装 [brew](http://brew.sh)
2. 使用 `brew install redis` 安装 redis，以启动并运行。

在 Linux 上，请参阅分发软件包管理器以了解最新构建。如果您愿意，可以[下载源](http://redis.io/download)并自行构建。 

执行 TCP 命令行并将其剪切并粘贴到您的终端，如下所示：
```shell
$ redis-cli -h portal.brilliant-redis-41.compose-3.composedb.com -p 15639 -a secretpassword
portal.brilliant-redis-41.compose-3.composedb.com:15639> set hello "world"
OK
portal.brilliant-redis-41.compose-3.composedb.com:15639> get hello
"world"
portal.brilliant-redis-41.compose-3.composedb.com:15639> 

```
您可以按如下所示运行一些简单的 Redis 命令来测试连接。

## 使用应用程序进行连接

没有正式的 Redis 客户机库。在 Redis 站点上列出了许多语言的客户机库。您可以在[此处](http://redis.io/clients)查看完整列表。建议的客户机用星号标记。如果要快速启动，以下是建议的客户机选择：       

语言|库|连接字符串使用
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[是](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[是](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|是，请参阅 [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details)、[2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

在 Compose 文章中还有 [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/)，这是 [Compose 博客](https://www.compose.com/articles/)，用于查看常用的多种语言的建议驱动程序。
