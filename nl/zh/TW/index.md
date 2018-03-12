---

copyright:
  years: 2016,2018
lastupdated: "2017-10-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 關於 {{site.data.keyword.composeForRedis}}
{: #about-compose-for-redis}

Redis 是開放程式碼記憶體內鍵值儲存庫。Redis 中的值可以是簡式字串、雜湊、清單，以及集合或強大的點陣圖、hyperloglogs 和地理空間索引。Redis 最適合用作應用程式快取或快速回應資料儲存庫。{{site.data.keyword.composeForRedis_full}} 提供已預先針對高可用性及磁碟內存持續性進行調整的配置，全部都透過額外安全特性鎖定。
{:shortdesc}

**附註：**在 2016 年 9 月 14 日之前佈建且仍然作用中的任何 Compose 服務實例，仍然可以使用，而且可以在 [https://www.compose.com/](https://www.compose.com) 直接存取。在 {{site.data.keyword.cloud}} 帳戶內，可以直接存取及使用從此點往前佈建的任何 Compose 服務實例。

## 建立 {{site.data.keyword.composeForRedis}} 服務實例

您可以從 {{site.data.keyword.cloud_notm}} 型錄中的 [{{site.data.keyword.composeForRedis}} 頁面](https://console.{DomainName}/catalog/services/compose-for-redis/)建立 {{site.data.keyword.composeForRedis}} 服務。

選擇服務名稱、地區、組織，以及要在其中佈建服務的空間。您可以使用**選取資料庫版本**欄位，從可用的資料庫版本中進行選擇。

有下拉清單可選取 TLS/SSL 加密。依預設，它會設為 **True**（加密）。如果選取 **False**，則佈建服務時不會加密。當您的驅動程式無法處理加密，且您知道未加密資料流量的潛在風險時，就可以使用此項。 

當您佈建 {{site.data.keyword.composeForRedis}} 實例時，可以選擇*標準* 或*企業* 方案。使用*企業* 方案，您可以將 {{site.data.keyword.composeForRedis}} 實例佈建到可用的 {{site.data.keyword.composeEnterprise}} 叢集。{{site.data.keyword.composeEnterprise}} 提供企業相符性所需的安全和隔離，並使用專用網路來確保已部署之資料庫的效能。如需詳細資料，請參閱 [Compose Enterprise 文件](../ComposeEnterprise/index.html)。

## 管理 {{site.data.keyword.composeForRedis}}

您可以從服務儀表板來管理服務。在這裡，您可以找到 {{site.data.keyword.cloud_notm}} Compose 資料庫的相關資訊，以及連接方式。您也可以：
- 管理備份
- 為您的服務配置更多資源
- 變更服務密碼
- 使用白名單來限制對資料庫的存取權。如需相關資訊，請參閱[設定](./dashboard-settings.html)。

## 連接至 {{site.data.keyword.composeForRedis}}

您可以使用與服務一起建立的認證，或使用服務儀表板的*概觀* 標籤中所提供的連線字串及指令行，來連接至服務。

## 將 {{site.data.keyword.cloud_notm}} 應用程式連接至 {{site.data.keyword.composeForRedis}}

若要將 {{site.data.keyword.cloud_notm}} 應用程式連接至服務，請使用與服務一起建立的認證。您可以在[連接 {{site.data.keyword.cloud_notm}} 應用程式](./connecting-bluemix-app.html)中，找到如何將 {{site.data.keyword.cloud_notm}} 應用程式連接至 {{site.data.keyword.composeForRedis}} 服務的資訊。

## 從 {{site.data.keyword.cloud_notm}}

 之外連接至 {{site.data.keyword.composeForRedis}}如果您想要從 {{site.data.keyword.cloud_notm}} 之外連接至 {{site.data.keyword.composeForRedis}}，則可以使用所提供的連線字串或指令行。您可以在[連接外部應用程式](./connecting-external.html)中，找到如何連接的相關資訊。
