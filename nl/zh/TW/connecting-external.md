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

# 連接外部應用程式
{: #connecting-external-app}

將外部應用程式連接至 {{site.data.keyword.composeForRedis_full}} 的方式有兩種：

- **連線字串**可由某些用戶端程式庫使用，且包含其他程式庫進行連接時所需的一切資訊；尤其是主機名稱及埠。
  - 已啟用 TLS/SSL 的連線將具有 "rediss:" 字首。大部分語言都有一個驅動程式，可支援利用 TLS/SSL 連接您的應用程式。 
  - 未加密的連線將具有 "redis:" 字首。當您的驅動程式無法處理加密，且您知道未加密資料流量的潛在風險時，就可以使用此項。 

- **指令行**是一個預先格式化的指令，它會使用正確的參數來呼叫 `redis-cli`。
  - 開放程式碼 Redis 沒有 TLS/SSL 支援，因此 Redis 指令行公用程式 `redis-cli` 只能使用此連線與其他配置搭配。
  - `redis-cli` 本質上可以使用未加密的連線，無需其他配置。

您將在 {{site.data.keyword.composeForRedis}} 服務的*概觀* 頁面上找到**連線字串**及**指令行**。


## 使用指令行連接

通常您將使用 `redis-cli` 指令手動連接至部署 - 這是遠端使用 Redis 安裝的最直接方式。它是 Redis 套件的一部分，所以您必須在本端安裝，才能使用它。您可以遵循 [Redis 下載頁面](http://redis.io/download)上的指示，下載原始檔並加以編譯。

### 未加密連線

如果您的 Redis 不受 TLS 加密保護（即「連線字串」顯示 `redis:`），請從顯示的**指令行**欄位取得字串，並將它貼入您的終端機：
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world"
```
您可以執行某些簡單的 Redis 指令來測試連線，如下所示。



### 已啟用 TLS/SSL 的連線

若要搭配使用 `redis-cli` 與加密連線，請設定 `stunnel` 這類公用程式，以在 TLS 加密中包裝 redis-cli 連線。設定 [stunnel](https://www.stunnel.org/index.html) 的步驟如下：

1. 安裝 stunnel
    
    使用 Linux、Homebrew for Mac 適用的套件管理程式，或抓取平台適用的[下載](https://www.stunnel.org/downloads.html)。

2. 剖析**連線字串**。例如，使用下列這類連線字串：
   ```text
   rediss://admin:PASSWORD@portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
   ```
   第二個冒號與 @ 符號之間的文字是密碼。在 @ 後面到下一個冒號之前的文字是主機，而該冒號後面的數字是埠號。因此，在此範例中，`PASSWORD` 是密碼、`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com` 是主機，而 `24370` 是埠。

3. 將此配置資訊新增至 stunnel.conf 檔案。配置是服務的名稱 (`[redis-cli]`)、指出此 stunnel 將是 TLS 用戶端的設定 (`client=yes`)、要接受連線的 IP 位址及埠 (`accept=127.0.0.1:6830`)，並連接您要連接至的主機名稱及埠 (`connect=`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370`)。
    ```text
    [redis-cli]
    client=yes
    accept=127.0.0.1:6830
    connect=portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
    ```
    如果您部署的結尾是 `composedb.com`，則會使用 Let's Encrypt 憑證，而不需要再執行任何動作。如果它的結尾是 `dblayer.com`，而且具有自簽憑證，則您需要從概觀的 *SSL 憑證* 標籤中取得憑證資訊，並將它全部複製到文字檔；例如 `cert.crt`。然後，將此憑證資訊的路徑新增至 stunnel.conf 檔案：
    
    ```text
    [redis-cli]
    client=yes
    accept=127.0.0.1:6830
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    verify=2
    checkHost=sl-us-south-1-portal.7.dblayer.com
    CAfile=/path/to/redis/cert.crt
    ```

3. 執行 stunnel
    在指令行中鍵入 `stunnel` 指令。它將立即在背景中執行。
    
4. 在新的「終端機」視窗中，執行指向本端主機及埠的 `redis-cli`，利用部署的認證進行鑑別。
    ```shell
    redis-cli -p 6830 -a <password>
    ```

## 使用應用程式連接

沒有官方的 Redis 用戶端程式庫。Redis 網站上列出的許多語言有多種用戶端程式庫。您可以在[這裡](http://redis.io/clients)看到完整清單。建議的用戶端會以星號標示。如果您想要快速啟動，建議選取的用戶端如下：       

語言|程式庫|使用連線字串
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[是](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[是](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|是 - 請參閱 [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details)、[2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

在 Compose 文章中也有 [Redis 入門之旅](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/)。您可以在 [Compose 部落格](https://www.compose.com/articles/)中查看針對更廣泛常用語言建議的驅動程式。
