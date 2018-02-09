---

copyright:
  years: 2016,2017
lastupdated: "2017-10-16"
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

**Note:** Any Compose service instances that were provisioned before 14 September 2016 that are still active can still be used and directly accessed at [https://www.compose.com/](https://www.compose.com). Any Compose service instance that is provisioned from this point forward is directly accessed and used within your {{site.data.keyword.cloud}} account.

## Creating a Compose for Redis service instance

[Create a {{site.data.keyword.composeForRedis}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-redis/).

When you create an instance of the service, ensure that you choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned. The various credential values are listed in the *Available credentials* section.

There is a drop-down to select TLS/SSL encryption. It is set to **True** encryption by default. If you select **False** then the service will be provisioned without encryption. This can be used when your drivers do not handle encryption and you are aware of the potential risks of unencrypted traffic. 

When you provision your {{site.data.keyword.composeForRedis}} instance you can choose the *Standard* or *Enterprise* plans. With the *Enterprise* plan, you can provision your {{site.data.keyword.composeForRedis}} instance into an available {{site.data.keyword.composeEnterprise}} cluster. {{site.data.keyword.composeEnterprise}} provides the security and isolation required by enterprise compliance and uses dedicated networking to ensure the performance of the deployed databases. See the [Compose Enterprise documentation](../ComposeEnterprise/index.html) for more details.

## Managing Compose for Redis

You can manage your service from the service dashboard. Here you can find information about your {{site.data.keyword.cloud_notm}} Compose database and how to connect to it. You can also:
- manage your backups
- allocate more resources for your service
- change the service password
- use whitelists to restrict access to your databases. 
For more information, see [Settings](./dashboard-settings.html).

## Connecting to Compose for Redis

You can connect to your service using the credentials that are created along with the service, or with the connection strings and command line that are provided in the *Overview* tab of your service dashboard.

## Connecting an {{site.data.keyword.cloud_notm}} application to Compose for Redis

To connect an {{site.data.keyword.cloud_notm}} application to your service, use the credentials that are created along with the service. You can find information on how to connect an {{site.data.keyword.cloud_notm}} application to a {{site.data.keyword.composeForRedis}} service in [Connecting an {{site.data.keyword.cloud_notm}} Application](./connecting-bluemix-app.html).

## Connecting to Compose for Redis from outside {{site.data.keyword.cloud_notm}}

If you want to connect to {{site.data.keyword.composeForRedis}} from outside {{site.data.keyword.cloud_notm}}, you can use the provided connection strings or command line. You can find information on how to connect in [Connecting an external application](./connecting-external.html).
