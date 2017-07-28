---

copyright:
  years: 2017
lastupdated: "2017-06-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting an external application
{: #connecting-external-app}

There are two ways of connecting an external application to {{site.data.keyword.composeForRedis}}:

- A **Connection String** can be used by some client libraries and contains all the information needed for other libraries to connect; specifically the host name and the port.

- **Command Line** is a preformatted command which will invoke `redis-cli` with the correct parameters.

You'll find both on the *Overview* page of your {{site.data.keyword.composeForRedis}} service.

## Connecting with the command line

You will usually be using the `redis-cli` command to manually connect to the deployment - it's the most direct way to remotely work with your Redis installation. It comes as part of the Redis package, so you will need to have Redis installed locally to use it. On Mac OS X, a good way to get Redis is by using Homebrew.

1. Install [brew](http://brew.sh)
2. Install redis with `brew install redis` to get up and running.

On Linux, refer to your distributions package manager for the latest build. If you are so inclined, you can [download the source](http://redis.io/download) and build it yourself. 

Take the TCP Command Line and cut and paste it into your terminal like so:
```shell
$ redis-cli -h portal.brilliant-redis-41.compose-3.composedb.com -p 15639 -a secretpassword
portal.brilliant-redis-41.compose-3.composedb.com:15639> set hello "world"
OK
portal.brilliant-redis-41.compose-3.composedb.com:15639> get hello
"world"
portal.brilliant-redis-41.compose-3.composedb.com:15639> 

```
You can test your connection by running some simple Redis commands as shown. 

## Connecting with applications

There is no official Redis client library. There are numerous client libraries for many languages which are listed on the Redis site. You can see the full list [here](http://redis.io/clients). Recommended clients are marked with a star. If you want to start quickly, here are a selection of recommended clients:       

Language|Library|Connection String Use
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Yes](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Yes](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[lettuce](https://github.com/mp911de/lettuce)|Yes- See [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](http://redis.paluch.biz/docs/api/releases/latest/com/lambdaworks/redis/RedisClient.html)

There is also a [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) in Compose articles, the [Compose blog](https://www.compose.com/articles/) which looks at the recommended drivers for a wider range of languages in common use.