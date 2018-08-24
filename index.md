---

copyright:
  years: 2016,2018
lastupdated: "2018-03-27"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# About {{site.data.keyword.composeForRedis}}
{: #about-compose-for-redis}

Redis is an open source, in-memory, key-value store. Values in Redis can be simple strings, hashes, lists, and sets or powerful bitmaps, hyperloglogs, and geospatial indexes. Redis is ideal as an application cache or quick response data store. {{site.data.keyword.composeForRedis_full}} gives you a configuration that is pre-tuned for high availability and on-disk persistence, all locked down with extra security features.
{:shortdesc}

**Note:** Compose service instances that were provisioned before 14 September 2016 that are still active can still be used and directly accessed at [https://www.compose.com](https://www.compose.com). Any Compose service instance that is provisioned from this point forward is directly accessed and used within your {{site.data.keyword.cloud}} account.

## Creating a {{site.data.keyword.composeForRedis}} service instance

You can create a {{site.data.keyword.composeForRedis}} service from the [{{site.data.keyword.composeForRedis}} page](https://console.{DomainName}/catalog/services/compose-for-redis/) in the {{site.data.keyword.cloud_notm}} catalog.

Choose a service name, and a region, organization, and space to provision the service in. You can use the **Select a database version** field to choose from the available database versions.

There is a drop-down to select TLS/SSL encryption. It is set to **True** encryption by default. If you select False,** then the service is provisioned without encryption. This can be used when your drivers do not handle encryption and you are aware of the potential risks of unencrypted traffic. 

When you provision your {{site.data.keyword.composeForRedis}} instance, you can choose the *Standard* or *Enterprise* plans. With the *Enterprise* plan, you can provision your {{site.data.keyword.composeForRedis}} instance into an available {{site.data.keyword.composeEnterprise}} cluster. {{site.data.keyword.composeEnterprise}} provides the security and isolation that is required by enterprise compliance and uses dedicated networking to ensure the performance of the deployed databases. See the [{{site.data.keyword.composeEnterprise}} documentation](/docs/services/ComposeEnterprise/index.html) for more details.

## Managing {{site.data.keyword.composeForRedis}}

You can manage your service from the service dashboard. Here you can find information about your {{site.data.keyword.cloud_notm}} Compose database and how to connect to it. You can also:
- Manage your backups
- Allocate more resources for your service
- Change the service password
- Use whitelists to restrict access to your databases. 

For more information, see [Settings](./dashboard-settings.html).

{{site.data.keyword.composeForRedis}} relies on Cloud Foundry roles to manage access to the service. Only users with the Developer role can see or use the service dashboard. For more information about Cloud Foundry roles, see the [Cloud Foundry access](https://console.{DomainName}/docs/iam/cfaccess.html#cfaccess) and the [Managing Cloud Foundry access](https://console.{DomainName}/docs/iam/mngcf.html#mngcf) pages.
{: tip}

## Connecting to {{site.data.keyword.composeForRedis}}

You can connect to your service by using the credentials that are created along with the service, or with the connection strings and command line that are provided in the *Overview* tab of your service dashboard.

## Connecting an {{site.data.keyword.cloud_notm}} application to {{site.data.keyword.composeForRedis}}

To connect an {{site.data.keyword.cloud_notm}} application to your service, use the credentials that are created along with the service. You can find information on how to connect an {{site.data.keyword.cloud_notm}} application to a {{site.data.keyword.composeForRedis}} service in [Connecting an {{site.data.keyword.cloud_notm}} Application](./connecting-bluemix-app.html).

## Connecting to {{site.data.keyword.composeForRedis}} from outside {{site.data.keyword.cloud_notm}}

If you want to connect to {{site.data.keyword.composeForRedis}} from outside {{site.data.keyword.cloud_notm}}, you can use the provided connection strings or command line. You can find information on how to connect in [Connecting an external application](./connecting-external.html).
