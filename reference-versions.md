---
copyright:
  years: 2016,2018
lastupdated: "2018-06-14"

keywords: redis, compose

subcollection: compose-for-redis

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Versions 
{: #versions}

## Versions (supported and deployed)

Deployable Versions| Preferred Version
----------|-----------
3.2.12, 4.0.10 | 4.0.10
{: caption="Table 1. Redis versions" caption-side="top"}

## Preferred Version

The preferred version is typically the newest version of the Redis database that is available for {{site.data.keyword.composeForRedis}}. It's the default version in the drop-down version selector on the catalog page, and the version that is automatically provisioned by API if no version is specified in the call.

### New Preferred Version Protocol

When a new version is made available, it is announced and made available for deployment. An approximately 7-day window follows the release; during this period the newest version is available, but isn't the preferred version. This window gives you a chance to deploy and test the new version, while the current version is still available. At the end of the 7-day window, the new version is set as the preferred version, or a new date for this change is announced.

The list of versions available for provisions is on the {{site.data.keyword.composeForRedis}} [catalog page](https://{DomainName}/catalog/compose-for-redis).

To get a current list of available versions for your {{site.data.keyword.composeForRedis}} service, you can use the 
[GET /2016-07/deployments/:id/versions](https://apidocs.compose.com/v1.0/reference#2016-07-get-deployments-versions) endpoint.
