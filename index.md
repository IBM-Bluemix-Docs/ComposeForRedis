---

copyright:
  years: 2016,2017
lastupdated: "2017-07-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with Compose for Redis
{: #getting-started-with-compose-for-redis}

Redis is an open source, in-memory, key-value store. Values in Redis can be simple strings, hashes, lists, and sets or powerful bitmaps, hyperloglogs, and geospatial indexes. Redis is ideal as an application cache or quick response data store. {{site.data.keyword.composeForRedis_full}} gives you a configuration that is pre-tuned for high availability and on-disk persistence, all locked down with extra security features.
{:shortdesc}

**Note:** Any Compose service instances that were provisioned before 14 September 2016 that are still active can still be used and directly accessed at [https://www.compose.com/](https://www.compose.com). Any Compose service instance that is provisioned from this point forward is directly accessed and used within your Bluemix account.

## Creating a Compose for Redis service instance

[Create a {{site.data.keyword.composeForRedis}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-redis/).

When you create an instance of the service, ensure that you choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned. The various credential values are listed in the *Available credentials* section.

When you provision your {{site.data.keyword.composeForRedis}} instance you can choose the *Standard* or *Enterprise* plans. With the *Enterprise* plan, you can provision your {{site.data.keyword.composeForRedis}} instance into an available {{site.data.keyword.composeEnterprise}} cluster. {{site.data.keyword.composeEnterprise}} provides the security and isolation required by enterprise compliance and uses dedicated networking to ensure the performance of the deployed databases. See the [Compose Enterprise documentation](../ComposeEnterprise/index.html) for more details.

## Managing Compose for Redis

You can manage your service from the service dashboard. Here you can find information about your Bluemix Compose database and how to connect to it. You can also manage your backups from the dashboard and allocated more resources for your service. For more information, see [Service Overview](./dashboard-overview.html), [Backups](./dashboard-backups.html), and [Scaling Resources](./dashboard-scaling-resources.md).

## Connecting to Compose for Redis

You can connect to your service using the credentials that are created along with the service, or with the connection strings and command line that are provided in the *Overview* tab of your service dashboard.

## Connecting a Bluemix application to Compose for Redis

To connect a Bluemix application to your service, use the credentials that are created along with the service. You can find information on how to connect a Bluemix application to a {{site.data.keyword.composeForRedis}} service in [Connecting a Bluemix Application](./connecting-bluemix-app.html).

## Connecting to Compose for Redis from outside Bluemix

If you want to connect to {{site.data.keyword.composeForRedis}} from outside Bluemix, you can use the provided connection strings or command line. You can find information on how to connect in [Connecting an external application](./connecting-external.html).