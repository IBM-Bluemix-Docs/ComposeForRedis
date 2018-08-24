---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-22"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting an external application
{: #connecting-external-app}

You can connect an external application to {{site.data.keyword.composeForRedis_full}} in two ways.

- A **Connection String** can be used by some client libraries and includes all the information that is needed for other libraries to connect; specifically, the host name and the port.
  - TLS/SSL-enabled connections have a `rediss:` prefix. Most languages have a driver that supports connecting your application with TLS/SSL. 
  - Unencrypted connections have a "redis:" prefix. You can use it when your drivers don't handle encryption and you're aware of the potential risks of unencrypted traffic. 

- **Command Line** is a preformatted command that invokes `redis-cli` with the correct parameters.
  - Open source Redis does not include TLS/SSL support, so the Redis command line utility, `redis-cli` needs additional configuration to use this connection.
  - `redis-cli` can use an unencrypted connection natively, without additional configuration.

You can both the **Connection String** and the **Command Line** on the *Overview* page of your {{site.data.keyword.composeForRedis}} service.


## Connecting with the command line

To manually connect to the deployment, you usually use the `redis-cli` command - it's the most direct way to remotely work with your Redis installation. It comes as part of the Redis package, so you need to install locally to use it. You can download the source and compile it following the instructions on the [Redis download page](http://redis.io/download).

### Unencrypted connections

If your Redis is not protected by TLS encryption (if the Connection String shows `redis:`), then take the string from the **Command Line** field that is displayed and paste it into your terminal:
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
You can test your connection by running some simple Redis commands as shown.

### TLS/SSL enabled connections

To use the `redis-cli` with an encrypted connection set up a utility like `stunnel`, which can wrap the redis-cli connection in TLS encryption. The steps to set up [stunnel](https://www.stunnel.org/index.html) are:

1. Install `stunnel`. Use your package manager for Linux, Homebrew for Mac, or [download](https://www.stunnel.org/downloads.html) the appropriate package for your platform.

2. Parse the **Connection String**.
   
    ```text
    rediss://admin:PASSWORD@portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
    ```

    - The password is the text between the second colon and at-symbol: `PASSWORD`.
    - The host is the text after the @ and up to the next colon: `portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com`.
    - The port is the number following that colon: `24370`.

3. Add your configuration information to the `stunnel.conf` file. The configuration includes the following information.
    - A name for a service (`[redis-cli]`)
    - A setting that says this stunnel is a TLS client (`client=yes`)
    - An IP address and port to accept connections on (`accept=127.0.0.1:6830`) and connect
    - The host name and port we want to connect to (`connect=`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370`).

    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
    ```

    If your deployment ends with `composedb.com`, it uses Let's Encrypt certificates and nothing more must be done.
    
    If your deployment ends with `dblayer.com`, it has a self-signed certificate. You need to get the certificate information from the overview's *SSL Certificate* tab, and copy it all to a text file. Then, add the path to this certificate information to the `stunnel.conf` file.
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    verify=2  
    checkHost=sl-us-south-1-portal.7.dblayer.com 
    CAfile=/path/to/redis/cert.crt
    ```

3. Run `stunnel`.

    Type the `stunnel` command at the command line. It immediately runs in the background.
    
4. In a new Terminal window, run `redis-cli` pointing to the local host and port, and authenticate with the deployment's credentials.

    ```shell
    redis-cli -p 6830 -a <password>
    ```

## Connecting with applications

There is no official Redis client library. Numerous client libraries are available for many languages, however, and you can see the full list on the [Redis site](http://redis.io/clients). Recommended clients are marked with a star.

Language|Library|Connection String Use
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Yes](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Yes](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Yes - See [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

For more information, see the [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2) in Compose articles, and the [Compose blog](https://www.compose.com/articles), which looks at the recommended drivers for a wider range of languages in common use.
