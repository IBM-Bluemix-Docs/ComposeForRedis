---

copyright:
  years: 2017
lastupdated: "2017-07-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 備份
{: #backups}

您可以從服務儀表板的*管理* 頁面中建立及下載備份。提供有排程備份及手動備份。

## 檢視現有備份

資料庫的每日備份是自動排定的。若要檢視現有備份，請導覽至服務儀表板的*管理* 頁面。 

![備份](./images/redis-backups-show.png "服務儀表板中的備份清單")

按一下對應列來展開任何可用備份的選項。

![備份選項](./images/redis-backups-options.png "備份的選項。") 

## 依需求建立備份

除了排程備份外，您也可以手動建立備份。若要建立手動備份，請導覽至服務儀表板的*管理* 頁面，然後按一下*立即備份*。

## 下載備份

若要下載備份，請導覽至服務儀表板的*管理* 頁面，然後針對您要下載的備份，按一下對應列中的*下載*。

## 備份內容

依預設，Redis 會儲存資料的二進位 Snapshot。然後，可以使用 dump.rdb 檔案作為復原點回復的備份。為了讓 Snapshot Redis 分出，Snapshot 的所有工作都是由子處理程序來完成，而母處理程序會繼續正常處理您的資料。備份處理程序不會影響您的應用程式或資料庫。您可以下載備份的副本，或將它們直接還原至新部署。

## 使用備份與本端資料庫搭配

您可以使用 {{site.data.keyword.composeForRedis}} 備份來執行資料庫的本端副本。

1. 將 dump.rdb 檔案移至其本身的目錄，例如 'db'。
2. 我們將需要 Redis 配置檔來啟動 Redis 實例，因此，您想要使用 dump.rdb 檔案，將安裝中的 redis.conf 檔案複製到 db 目錄。比方說，如果您已在 OSX 上使用 homebrew 安裝 Redis，而且 redis.conf 檔案位於 `/usr/local/etc`，請從 db 目錄執行 `cp /usr/local/etc/redis.conf`。
3. 編輯配置檔，以指向它啟動時的現行目錄。使用文字編輯器開啟 redis.conf，並將 `dir /usr/local/var/db/redis/` 一行變更為 `dir .`。儲存檔案並結束。
4. 在提供配置檔的 db 目錄中啟動 Redis 伺服器：`redis-server redis.conf`。

## 還原備份

若要將備份還原至新的服務實例，請遵循步驟來檢視現有備份，然後按一下對應列以展開您要下載之備份的選項。按一下**還原**按鈕。即會顯示一則訊息，讓您知道已起始還原。新的服務實例會自動命名為 "redis-restore-[timestamp]"，而且在佈建開始時，儀表板上會出現這個實例。
