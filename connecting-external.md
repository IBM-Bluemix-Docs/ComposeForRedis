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

There are two ways of connecting an external application to {{site.data.keyword.composeForRedis_full}}:

- A **Connection String** can be used by some client libraries and contains all the information needed for other libraries to connect; specifically the host name and the port.
  - TLS/SSL-enabled connections will have a "rediss:" prefix. Most languages have a driver that supports connecting your application with TLS/SSL. 
  - Unencrypted connections will have a "redis:" prefix. This can be used when your drivers do not handle encryption and you are aware of the potential risks of unencrypted traffic. 

- **Command Line** is a preformatted command which will invoke `redis-cli` with the correct parameters.
  - There is no TLS/SSL support baked into the open source Redis, so the Redis command line utility, `redis-cli` can only use this connection with additional configuration.
  - `redis-cli` can use an unencrypted connection natively, without additional configuration.

You'll find both the **Connection String** and the **Command Line** on the *Overview* page of your {{site.data.keyword.composeForRedis}} service.


## Connecting with the command line

You will usually use the `redis-cli` command to manually connect to the deployment - it's the most direct way to remotely work with your Redis installation. It comes as part of the Redis package, so you will need to have installed locally to use it. You can download the source and compile it following the instructions on the [Redis download page](http://redis.io/download).

### TLS/SSL enabled connections
To use the `redis-cli` with an encypted connection set up a utility like `stunnel` to handle the encryption. The steps to set up [stunnel](https://www.stunnel.org/index.html) are:

1. Install stunnel
    
    Use your package manager for Linux, Homebrew for Mac, or grab a [download](https://www.stunnel.org/downloads.html) appropriate for your platform.

2. Add the information from the **Command Line** field to the stunnel.conf file
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    ```
    
    If your deployment has a self-signed certificate, you will need to add certificate information to the stunnel.conf file:
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    verify=2  
    checkHost=sl-us-south-1-portal.7.dblayer.com 
    CAfile=/path/to/redis/cert.crt
    ```

3. Run stunnel
    
    Type the `stunnel` command at the command-line. It will immediately run in the background.
    
4. Run `redis-cli` pointing to the local host and port, authenticate with the deployment's credentials.

    ```shell
    redis-cli -p 6830 -a <password>
    ```

### Unencrypted HTTP connections
Take the string from the **Command Line** field and paste it into your terminal:
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
You can test your connection by running some simple Redis commands as shown. 


## Connecting with applications

There is no official Redis client library. There are numerous client libraries for many languages which are listed on the Redis site. You can see the full list [here](http://redis.io/clients). Recommended clients are marked with a star. If you want to start quickly, here are a selection of recommended clients:       

Language|Library|Connection String Use
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Yes](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Yes](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Yes- See [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

There is also a [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) in Compose articles, the [Compose blog](https://www.compose.com/articles/) which looks at the recommended drivers for a wider range of languages in common use.
