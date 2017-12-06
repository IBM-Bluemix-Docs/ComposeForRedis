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

# 외부 애플리케이션 연결
{: #connecting-external-app}

외부 애플리케이션을 {{site.data.keyword.composeForRedis_full}}에 연결하는 두 가지 방법이 있습니다.

- **연결 문자열**은 일부 클라이언트 라이브러리에서 사용될 수 있으며 다른 라이브러리가 연결하는 데 필요한 모든 정보(특히 호스트 이름 및 포트)를 포함합니다.

- **명령행**은 올바른 매개변수와 함께 `redis-cli`를 호출하는 사전 형식화된 명령입니다.

둘 다 {{site.data.keyword.composeForRedis}} 서비스의 *개요* 페이지에서 찾을 수 있습니다.

## 명령행을 사용하여 연결

일반적으로 `redis-cli` 명령을 사용하여 수동으로 배치에 연결합니다. 원격으로 Redis 설치에 대해 작업하는 것이 가장 직접적인 방법입니다. 이는 Redis 패키지의 파트로 제공되므로 이를 사용하려면 Redis가 로컬에 설치되어 있어야 합니다. Mac OS X에서 Redis를 가져오는 좋은 방법은 Homebrew를 사용하는 것입니다.

1. [brew](http://brew.sh)를 설치하십시오.
2. `brew install redis`를 사용하여 redis를 설치하고 시작하여 실행하십시오.

Linux에서 최신 빌드는 배포 패키지 관리자를 참조하십시오. 원하는 경우 [소스를 다운로드](http://redis.io/download)하여 직접 빌드할 수 있습니다. 

TCP 명령행을 사용하여 다음과 같이 이를 복사하여 터미널에 붙여넣으십시오.
```shell
$ redis-cli -h portal.brilliant-redis-41.compose-3.composedb.com -p 15639 -a secretpassword
portal.brilliant-redis-41.compose-3.composedb.com:15639> set hello "world"
OK
portal.brilliant-redis-41.compose-3.composedb.com:15639> get hello
"world"
portal.brilliant-redis-41.compose-3.composedb.com:15639> 

```
표시된 대로 몇 가지 단순 Redis 명령을 실행하여 연결을 테스트할 수 있습니다.

## 애플리케이션을 사용하여 연결

공식 Redis 클라이언트 라이브러리는 없습니다. Redis 사이트에 나열된 여러 언어에 대한 많은 클라이언트 라이브러리가 있습니다. [여기](http://redis.io/clients)에서 전체 목록을 볼 수 있습니다. 권장되는 클라이언트는 별표로 표시됩니다. 빠르게 시작하려는 경우 여기에 권장되는 클라이언트의 선택사항이 있습니다.       

언어|라이브러리|연결 문자열 사용
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[예](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[예](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|예, [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html) 참조 

Compose 문서의 [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/), 일반적으로 사용되는 광범위한 언어에 대해 권장되는 드라이버를 살펴보는 [Compose 블로그](https://www.compose.com/articles/)도 있습니다.
