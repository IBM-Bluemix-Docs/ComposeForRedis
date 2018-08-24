---

copyright:
  years: 2017,2018
lastupdated: "2018-03-02"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 備份
{: #backups}

您可以從服務儀表板的_管理_ 頁面的_備份_ 標籤中，建立及下載備份。有每日、每週、每月及隨需應變備份可供使用。系統會根據下列排程保留它們：

備份類型|保留排程
----------|-----------
每日|每日備份保留 7 日
每週|每週備份保留 4 週
每月|每月備份保留 3 個月
隨需應變|保留一份隨需應變備份。保留的備份一律是最新的隨需應變備份。
{: caption="表 1. 備份保留排程" caption-side="top"}

備份排程與保留原則是固定的。如果您需要保留的備份數目超過保留排程所容許的數目，則應該根據您的商業需求下載備份及保留保存檔。

## 檢視現有備份

資料庫的每日備份是自動排定的。若要檢視現有備份，請導覽至服務儀表板的*管理* 頁面。 

  ![備份](./images/redis-backups-show.png "服務儀表板中的備份清單")

按一下對應列來展開任何可用備份的選項。

  ![備份選項](./images/redis-backups-options.png "備份的選項。") 

### 使用 API 檢視現有備份

備份的清單位於 `GET /2016-07/deployments/:id/backups` 端點上。具有服務實例 ID 及部署 ID 的「基礎端點」都會顯示在服務的_概觀_ 中。例如： 
``` 
https://composebroker-dashboard-public.mybluemix.net/api/2016-07/instances/$INSTANCE_ID/deployments/$DEPLOYMENT_ID/backups
```  

## 依需求建立備份

除了排定的備份外，您也可以手動建立備份。若要建立手動備份，請導覽至服務儀表板的*管理* 頁面，然後按一下*立即備份*。

### 使用 API 建立備份

請將 POST 要求傳送至 backups 端點，以起始手動備份：`POST /2016-07/deployments/:id/backups`。它會立即傳回執行中備份的秘訣 ID 及相關資訊。您必須檢查 backups 端點，以查看備份是否已完成，並在使用之前找到其 backup_id。請使用 `GET /2016-07/deployments/:id/backups/`。

## 下載備份

若要下載備份，請導覽至服務儀表板的*管理* 頁面，然後針對您要下載的備份，按一下對應列中的*下載*。

### 使用 API 下載備份

在服務的_備份_ 頁面上，尋找您要從中還原的備份，並複製 backup_id，或透過 Compose API 使用 `GET /2016-07/deployments/:id/backups` 尋找備份及其 backup_id。然後，使用 backup_id 來尋找特定備份的資訊及下載鏈結：`GET /2016-07/deployments/:id/backups/:backup_id`。

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

### 透過 {{site.data.keyword.cloud_notm}} CLI 還原

請使用下列步驟，以使用 {{site.data.keyword.cloud_notm}} CLI 將備份從執行中 Redis 服務還原至新的 Redis 服務。 
1. 如果您需要，請[下載並安裝它](https://console.{DomainName}/docs/cli/index.html#overview)。 
2. 在服務的_備份_ 頁面上，尋找您要從中還原的備份，然後複製備份 ID。  
  **或**  
  透過 Compose API 使用 `GET /2016-07/deployments/:id/backups` 尋找備份及其 ID。「基礎端點」及服務實例 ID 都會顯示在服務的_概觀_ 中。例如： 
  ``` 
  https://composebroker-dashboard-public.mybluemix.net/api/2016-07/instances/$INSTANCE_ID/deployments/$DEPLOYMENT_ID/backups
  ```  
  回應將會有該服務實例之所有可用備份的清單。請挑選您要從中還原的備份，並複製其 ID。

3. 使用適當的帳戶及認證登入。`ibmcloud login`（或 `ibmcloud login -help` 以查看所有登入選項）。

4. 切換至「組織」及「空間」：`ibmcloud target -o "$YOUR_ORG" -s "YOUR_SPACE"`

5. 使用 `service create` 指令來佈建新的服務，並在 JSON 物件中提供您要還原的來源服務及特定備份。例如：
``` 
ibmcloud service create SERVICE PLAN SERVICE_INSTANCE_NAME -c '{"source_service_instance_id": "$SERVICE_INSTANCE_ID", "backup_id": "$BACKUP_ID" }'
```
  _SERVICE_ 欄位應該是 compose-for-redis，而 _PLAN_ 欄位應該是 Standard（標準）或 Enterpris（企業），視您的環境而定。_SERVICE\_INSTANCE\_NAME_ 是您將放置新服務名稱的位置。_source\_service\_instance\_id_ 是備份來源的服務實例 ID；其取得方式是執行 `ibmcloud cf service DISPLAY_NAME --guid`，其中 _DISPLAY\_NAME_ 是備份來源的 Redis 服務名稱。 
  
  企業使用者也將需要使用 `"cluster_id": "$CLUSTER_ID"` 參數，在 JSON 物件中指定要部署到哪個叢集。
  
### 移轉至新版本

現行執行中部署無法進行部分主要版本升級。您將需要佈建執行已升級版本的新服務，然後使用備份將您的資料移轉至其中。此處理程序與上面的還原備份處理程序相同，但您將指定要升級到的版本。

``` 
ibmcloud service create SERVICE PLAN SERVICE_INSTANCE_NAME -c '{"source_service_instance_id": "$SERVICE_INSTANCE_ID", "backup_id": ""$BACKUP_ID", "db_version":"$VERSION_NUMBER" }'
```

例如，將舊版的 {{site.data.keyword.composeForRedis}} 服務還原為執行 Redis 4.0.6 的新服務如下所示：
```
ibmcloud service create compose-for-redis Standard migrated_redis -c '{ "source_service_instance_id": "0269e284-dcac-4618-89a7-f79e3f1cea6a", "backup_id":"5a96d8a7e16c090018884566", "db_version":"4.0.6"  }'

