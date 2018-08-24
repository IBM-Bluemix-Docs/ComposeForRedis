---

copyright:
  years: 2016,2018
lastupdated: "2018-05-09"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting an {{site.data.keyword.cloud_notm}} application

To connect an {{site.data.keyword.cloud}} application to your service, use the service credentials that are created when the service is provisioned. 

## Using the 'Hello World' sample app

The [sample app](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) demonstrates how to use Node.js and your service credentials to connect to a {{site.data.keyword.composeForRedis}} service. The application uses a web interface to create, read from, and write data to a database.

Download the sample app and follow the instructions in the readme file. Then, in your application details page in {{site.data.keyword.cloud_notm}}, click **View APP** to view the contents of the *examples* table.

## Available credentials

Field Name|Description
----------|-----------
`uri`|The URI to be used when connecting to the service. It includes the schema (redis:), admin user name and password, the host name of the server and the port number to connect to.
`uri_direct_1`|A secondary URI that can be used when connecting to the service. The format is the same as for `uri`.
`ca_certificate_base64` `(optional)`|A base64 encoded, self-signed certificate that is used to confirm that an application is connecting to the appropriate server. The certificate is only present on services that have a self-signed instead of a Let's Encrypt certificate. You need to decode the key before you can use it, as shown in the sample application.
`uri_cli`|A `redis-cli` command line that connects to the database instance.
`deployment_id`|An internal identifier for the service as created within Compose.
`db_type`|The type of database that is offered by the service; in this case `redis`.
`name`|The database deployment name.
{: caption="Table 1. Compose for Redis credentials" caption-side="top"}

**Note:** Two `haproxy` portals provide access to the Redis service. Both `uri` and `uri_direct_1` can be used to connect. In your applications, switch between `uri` and `uri_direct_1` to manage responses to connection failures.
