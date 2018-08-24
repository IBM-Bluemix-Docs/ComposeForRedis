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

# Pricing
{: #pricing}

## Base Configuration

An {{site.data.keyword.composeForRedis_full}} service starts with two redis/sentinel nodes that each have 256 MB memory and 256 MB storage, which is equal to one unit of resources. The service _includes_ replication and high-availability, so each unit and the price per unit _includes_ the cost of the resources across both nodes.

The base configuration also includes a dedicated sentinel node to handle replication and a HAProxy portal to manage connections. The sentinel node and the HAProxy portal have 64 MB memory each.

The base service configuration has a set price. Consult the catalog tiles on {{site.data.keyword.cloud_notm}} for base pricing in your local currency. For example, the base price in US dollars is $13/month.

## Increasing resources

If you need extra memory for your service, you can increase the resources that are allocated in a 1:1 ratio of disk storage to memory unit. A {{site.data.keyword.composeForRedis}} unit consists of 256 MB of storage and 256 MB of memory, and each unit and the price per unit _includes_ the cost to increase the resources on both nodes.

## Calculating the cost of your deployment
{: #tiered-pricing}

Each additional unit (256 MB storage/256MB memory) has a per unit price, which is listed in your local currency on the {{site.data.keyword.cloud_notm}} catalog tile for the service. In US dollars each additional unit costs $13. As the _total_ size of all your {{site.data.keyword.composeForRedis}} services increases, the per unit price decreases, as shown in the tiered pricing table.

Number of Units|Price per Unit
----------|-----------
1 - 9 units|Base price per unit - $13.00 USD/Unit
10 - 24 units|10% reduction - $11.70 USD/Unit
25 - 49 units|20% reduction - $10.40 USD/Unit
50 - 99 units|30% reduction - $9.10 USD/Unit
100 - 499 units|40% reduction - $7.80 USD/Unit
500 - 999 units|50% reduction - $6.50 USD/Unit
1,000 - 4,999 units|60% reduction - $5.20 USD/Unit
5,000+ units|70% reduction - $3.90 USD/Unit
{: caption="Table 1. {{site.data.keyword.composeForRedis}} tiered pricing" caption-side="top"}

