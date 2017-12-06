---

Copyright:
  Years: 2017
lastupdated: "2017-09-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Service Overview

The _Overview_ page shows you information about your {{site.data.keyword.cloud}} Compose database. The overview includes essential identifying information and current resource usage. You'll also find a section for connection strings that you can use with tools or make use of tools to connect to your database.

## Deployment Details

The _Deployment Details_ panel shows details of your service.

![Deployment Details](./images/redis-deployment-details.png "A view of the Deployment Details panel")

### Type

The type of database that is offered by the service, and the database version that your service uses.

### Name

An internal identifier for the service.

### Usage

The size of your database and the amount of storage provided by your service plan.


## Connecting

There are two ways of connecting an external application to your database. You can either connect using a **Connection String** or with a **Command Line**. Both are provided on your service dashboard overview.

### HTTPS

The **HTTPS** connection string can be used by some client libraries and contains all the information needed for other libraries to connect. You can find out how to use the connection string to connect in [Connecting an external application](./connecting-external.html).

**Please Note:** At this time this connection is **NOT** SSL/TLS secured. 

### Command Line

The **Command Line** is a preformatted command which will invoke `redis-cli` with the correct parameters. To use it, you'll need to have the Redis client tools installed on the local system. You can find out more about how to do this in [Connecting an external application](./connecting-external.html).

**Please Note:**  This connection is **NOT** SSL/TLS secured. Redis does not support encryption.


