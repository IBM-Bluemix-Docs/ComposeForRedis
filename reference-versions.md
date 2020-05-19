---
copyright:
  years: 2016,2018
lastupdated: "2018-06-14"

keywords: redis, compose

subcollection: ComposeForRedis

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

You can find the list of available versions on the {{site.data.keyword.composeForRedis}} [catalog page](https://{DomainName}/catalog/compose-for-redis) or from the [GET /2016-07/deployments/:id/versions](https://apidocs.compose.com/v1.0/reference#2016-07-get-deployments-versions) API endpoint.

## Preferred Version

The preferred version is typically the newest version of the Redis database that is available for {{site.data.keyword.composeForRedis}}. It's the default version in the drop-down version selector on the catalog page, and the version that is automatically provisioned by API if no version is specified in the call.

### New Preferred Version Protocol

When a new version is made available, it is announced and made available for deployment. An approximately 7-day window follows the release; during this period the newest version is available, but isn't the preferred version. This window gives you a chance to deploy and test the new version, while the current version is still available. At the end of the 7-day window, the new version is set as the preferred version, or a new date for this change is announced.

