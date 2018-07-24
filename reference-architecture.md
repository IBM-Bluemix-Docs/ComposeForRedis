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

# Architecture 
{: #architecture}

## Replication

An {{site.data.keyword.composeForRedis_full}} service uses [Redis Sentinel](https://redis.io/topics/sentinel) to provide high-availability and monitoring for your databases. Each service consists of three data nodes; all three run the sentinel process and two run the redis process. When you select a region where the serivce is deployed, the three nodes spread over the region's availablity zones, and your data is replicated across them. Should one data member become unreachable, your cluster will continue to operate normally.

## Disk Encryption

All {{site.data.keyword.composeForRedis}} services all have encryption at rest. Your data resides on servers that have volume-level encryption enabled. 

Because this is {{site.data.keyword.composeForRedis}} is a managed service, it is possible for {{site.data.keyword.cloud}} Compose operators to see data. In addition to the disk encryption, we recommend that if you are storing personal information in your database that you encrypt information before storing it or by using extensions or features to enable encryption on the database itself. While these methods may impact usability or performance, it is good practice to ensure that personal information is protected with encryption.

## Auto-scaling

Resources are scaled automatically based on the total memory use of the Redis databases. Storage is based on a ratio of provisioned RAM at 1:1. These resources are bundled as units.

Auto-scaling is designed to respond to the short-to-medium term trends of your database. Every minute, your service is checked and if it is running short on RAM, then more units are allocated to the deployment. 

Auto-scaling does not scale down deployments where disk/memory usage has shrunk. The resources provisioned to your databases will remain for your future needs, or until you scale down your deployment manually.
{: .tip}