---

copyright:
  years: 2016,2018
lastupdated: "2018-01-03"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 定价
{: #pricing}

## 基本配置

{{site.data.keyword.composeForRedis_full}} 服务一开始有两个 redis/sentinel 节点，每个节点有 256 MB 内存和 256 MB 存储空间，相当于 1 个资源单元。该服务_包含_复制和高可用性，因此每个单元和单元单价都_包含_两个节点上资源的成本。

基本配置还包含一个专用 sentinel 节点（用于处理复制）和一个 HAProxy 门户网站（用于管理连接）。sentinel 节点和 HAProxy 门户网站分别有 64 MB 内存。

基本服务配置具有固定价格。有关以本地货币为单位的基础定价，请查阅 {{site.data.keyword.cloud_notm}} 上的“目录”磁贴。例如，以美元为单位的基础价格是 13 美元/月。

## 增加资源

如果服务需要更多内存，您可以增加按 1:1 的磁盘存储量与内存单元比率分配的资源。一个 {{site.data.keyword.composeForRedis}} 单元包含 256 MB 存储空间和 256 MB 内存，每个单元和单元单价都_包含_增加两个节点上资源的成本。

## 计算部署成本
{: #tiered-pricing}

每增加一个单元（256 MB 存储空间/256 MB 内存）都会有相应的单元单价，该单价会在服务的 {{site.data.keyword.cloud_notm}}“目录”磁贴上以本地货币列出。以美元为单位时，每增加一个单元需要的成本是 13 美元。随着所有 {{site.data.keyword.composeForRedis}} 服务的_总_大小增加，单元单价会下降，如下面的分层定价表所示。

单元数|单元单价
----------|-----------
1 - 9 个单元|基础单元单价 -- 13.00 美元/单元
10 - 24 个单元|10% 折扣 -- 11.70 美元/单元
25 - 49 个单元|20% 折扣 -- 10.40 美元/单元
50 - 99 个单元|30% 折扣 -- 9.10 美元/单元
100 - 499 个单元|40% 折扣 -- 7.80 美元/单元
500 - 999 个单元|50% 折扣 -- 6.50 美元/单元
1,000 - 4,999 个单元|60% 折扣 -- 5.20 美元/单元
5,000 个及以上单元|70% 折扣 -- 3.90 美元/单元
{: caption="表 1. {{site.data.keyword.composeForRedis}} 分层定价" caption-side="top"}

