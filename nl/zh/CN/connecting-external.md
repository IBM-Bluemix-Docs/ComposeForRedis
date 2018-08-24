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

# 连接外部应用程序
{: #connecting-external-app}

有两种方法可将外部应用程序连接到 {{site.data.keyword.composeForRedis_full}}：

- **连接字符串**可由某些客户机库使用，并包含其他库连接所需的所有信息，具体包括主机名和端口。
  - 启用 TLS/SSL 的连接将具有“rediss:”前缀。大多数语言都有支持通过 TLS/SSL 来连接应用程序的驱动程序。 
  - 未加密的连接将具有“redis:”前缀。在驱动程序不处理加密，并且您了解未加密流量的潜在风险时，可以这样做。 

- **命令行**是一个预先格式化的命令，它将使用正确的参数来调用 `redis-cli`。
  - 开放式源代码 Redis 中未纳入 TLS/SSL 支持，因此 Redis 命令行实用程序 `redis-cli` 只能通过附加配置来使用此连接。
  - `redis-cli` 可以通过本机方式使用未加密的连接，无需其他配置。

您将在 {{site.data.keyword.composeForRedis}} 服务的*概述*页面上找到**连接字符串**和**命令行**。


## 使用命令行进行连接

通常，您将使用 `redis-cli` 命令以手动方式连接到部署：这是远程使用 Redis 安装的最直接的方法。它作为 Redis 软件包的一部分提供，因此您需要在本地安装才能使用 Redis。您可以按照 [Redis 下载页面](http://redis.io/download)上的指示信息来下载源代码并进行编译。

### 未加密的连接

如果 Redis 不受 TLS 加密的保护，即“连接字符串”显示 `redis:`，请获取显示的**命令行**字段中的字符串，并将其粘贴到您的终端：
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
您可以按如下所示运行一些简单的 Redis 命令来测试连接。



### 启用 TLS/SSL 的连接

要将 `redis-cli` 用于加密连接，请设置实用程序（如 `stunnel`）以将 redis-cli 连接包装在 TLS 加密中。设置 [stunnel](https://www.stunnel.org/index.html) 的步骤如下：

1. 安装 stunnel
    
    使用 Linux 软件包管理器、Mac 的 Homebrew 或者获取适合您平台的[下载](https://www.stunnel.org/downloads.html)。

2. 解析**连接字符串**。例如，使用如下的连接字符串：
   ```text
   rediss://admin:PASSWORD@portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
   ```
   第二个冒号和 @ 符号之间的文本是密码。@ 与下一个冒号之间的文本是主机，该冒号后面的数字是端口号。所以，在此示例中，`PASSWORD` 是密码，`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com` 是主机，`24370` 是端口。

3. 将此配置信息添加到 stunnel.conf 文件中。配置是服务的名称 (`[redis-cli]`)、表示此 stunnel 将是 TLS 客户机的设置 (`client=yes`)、用于接受连接的 IP 地址和端口 (`accept=127.0.0.1:6830`)，以及要连接到的主机名和端口 (`connect=`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370`)。
    ````text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
    ```
    如果部署以 `composedb.com` 结尾，它将使用 Let's Encrypt 证书，并且不必执行其他任何操作。如果以 `dblayer.com` 结尾，说明部署具有自签名证书，您需要从概述的 *SSL 证书*选项卡中获取证书信息，然后将其全部复制到一个文本文件中；例如 `cert.crt`。接下来，将此证书信息的路径添加到 stunnel.conf 文件中：
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    verify=2  
    checkHost=sl-us-south-1-portal.7.dblayer.com 
    CAfile=/path/to/redis/cert.crt
    ```

3. 运行 stunnel
    在命令行上输入 `stunnel` 命令。该命令会立即在后台运行。
    
4. 在新的终端窗口中，运行指向本地主机和端口的 `redis-cli`，并使用部署凭证进行认证。
    ```shell
    redis-cli -p 6830 -a <password>
    ```

## 使用应用程序进行连接

没有正式的 Redis 客户机库。在 Redis 站点上列出了许多语言的客户机库。您可以在[此处](http://redis.io/clients)查看完整列表。建议的客户机用星号标记。如果要快速启动，以下是建议的客户机选择：       

语言|库|连接字符串使用
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[是](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[是](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|是，请参阅 [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details)、[2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

在 Compose 文章中还有 [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/)，这是 [Compose 博客](https://www.compose.com/articles/)，用于查看常用的多种语言的建议驱动程序。
