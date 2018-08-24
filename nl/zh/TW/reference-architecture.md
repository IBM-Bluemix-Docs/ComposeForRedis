---
copyright:
  years: 2016,2018
lastupdated: "2018-06-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 架構 
{: #architecture}

## 抄寫

{{site.data.keyword.composeForRedis_full}} 服務使用 [Redis Sentinel](https://redis.io/topics/sentinel) 來提供資料庫的高可用性及監視功能。每一個服務都包含三個資料節點；三個節點全都執行 Sentinel 程序，而有兩個節點執行 Redis 程序。當您選取部署服務的地區時，三個節點會分散在地區的可用性區域，然後您的資料會在它們之間抄寫。萬一某一個資料成員變成無法聯繫，您的叢集將繼續正常運作。

## 磁碟加密

所有 {{site.data.keyword.composeForRedis}} 服務都有靜態加密。您的資料位於已啟用磁區層次加密的伺服器上。 

由於 {{site.data.keyword.composeForRedis}} 是一項受管理的服務，因此 {{site.data.keyword.cloud}} Compose 操作員能夠看到資料。除了磁碟加密外，我們建議您，如果要將個人資訊儲存在資料庫中，請先將資訊加密再儲存它，或使用延伸或特性對資料庫本身啟用加密。這些方法固然可能影響可用性或效能，確定個人資訊受到加密保護仍是個很好的作法。

## 自動調整

資源會根據 Redis 資料庫的記憶體總用量而自動調整。儲存空間是以 1:1 的佈建 RAM 比例為基礎。這些資源組合成為單位。

自動調整的設計是要回應資料庫的中短期趨勢。每分鐘都會檢查您的服務，如果它的 RAM 不足，便會將更多的單位配置給該部署。 

自動調整對於磁碟/記憶體用量收縮的部署，不會將其縮減。針對您的資料庫佈建的資源將會保留以供您未來需要，或是直到您手動縮減部署為止。
{: .tip}
