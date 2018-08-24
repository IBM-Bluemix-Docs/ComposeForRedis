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

# 体系结构 
{: #architecture}

## 复制

{{site.data.keyword.composeForRedis_full}} 服务使用 [Redis Sentinel](https://redis.io/topics/sentinel) 为数据库提供高可用性和监视功能。每个服务都包含三个数据节点；三个节点都运行 sentinel 进程，其中两个节点运行 redis 进程。选择部署了该服务的区域时，三个数据节点会分布在该区域的可用性专区中，然后数据会在三个数据节点之间进行复制。如果一个数据成员变为不可访问，集群仍会继续正常运行。

## 磁盘加密

所有 {{site.data.keyword.composeForRedis}} 服务都具有静态加密。数据位于启用了卷级别加密的服务器上。 

由于 {{site.data.keyword.composeForRedis}} 是受管服务，因此 {{site.data.keyword.cloud}} Compose 操作员可以查看数据。除了磁盘加密外，还建议您在数据库中存储个人信息之前，对这些信息加密，或者使用扩展或功能启用对数据库本身的加密。虽然这些方法可能会影响可用性或性能，但确保个人信息受到加密保护是比较好的做法。

## 自动扩展

资源将根据 Redis 数据库的内存总使用量自动进行扩展。存储量基于按 1:1 比率供应的 RAM。这些资源会捆绑为单元。

自动扩展旨在响应数据库的中短期趋势。系统每分钟会检查一次服务，如果该服务的 RAM 不足，那么会向部署分配更多单元。 

自动扩展不会向下扩展部署，即减少磁盘/内存使用量。向数据库供应的资源将保留以满足您的未来需求，或者直到您手动向下扩展部署为止。
{: .tip}
