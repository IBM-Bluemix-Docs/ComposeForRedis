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

# 외부 애플리케이션 연결
{: #connecting-external-app}

외부 애플리케이션을 {{site.data.keyword.composeForRedis_full}}에 연결하는 두 가지 방법이 있습니다.

- **연결 문자열**은 일부 클라이언트 라이브러리에서 사용될 수 있으며 다른 라이브러리가 연결하는 데 필요한 모든 정보(특히 호스트 이름 및 포트)를 포함합니다.
  - TLS/SSL 사용 연결에는 "rediss:" 접두부가 있습니다. 대부분의 언어에는 TLS/SSL을 사용하여 애플리케이션을 연결하는 것을 지원하는 드라이버가 있습니다. 
  - 암호화되지 않은 연결에는 "redis:" 접두부가 있습니다. 이는 드라이버가 암호화를 처리하지 않으며 사용자가 암호화되지 않은 트래픽의 잠재적 위험에 대해 알고 있는 경우 사용할 수 있습니다. 

- **명령행**은 올바른 매개변수와 함께 `redis-cli`를 호출하는 사전 형식화된 명령입니다.
  - 오픈 소스 Redis에는 TLS/SSL 지원이 포함되어 있지 않으므로 Redis 명령행 유틸리티 `redis-cli`는 이 연결만 추가 구성과 함께 사용할 수 있습니다.
  - `redis-cli`는 추가 구성 없이 암호화되지 않은 연결을 기본적으로 사용할 수 있습니다.

{{site.data.keyword.composeForRedis}} 서비스의 *개요* 페이지에서는 **연결 문자열**과 **명령행**을 둘 다 볼 수 있습니다.


## 명령행을 사용하여 연결

일반적으로 사용자는 `redis-cli` 명령을 사용하여 수동으로 배치에 연결하며, 이는 원격으로 Redis 설치에 대해 작업하는 방법 중 가장 직접적인 방법입니다. 이는 Redis 패키지의 일부로서 제공되므로 사용하려면 이를 로컬에 설치해야 합니다. 사용자는 소스를 다운로드하고 [Redis 다운로드 페이지](http://redis.io/download)의 지시사항에 따라 컴파일할 수 있습니다.

### 암호화되지 않은 연결

Redis가 TLS 암호화로 보호되지 않는 경우(즉, 연결 문자열에 `redis:`가 표시됨) 표시되는 **명령행** 필드에서 문자열을 복사하여 터미널에 붙여넣으십시오.
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
표시된 대로 몇 가지 단순 Redis 명령을 실행하여 연결을 테스트할 수 있습니다.

### TLS/SSL 사용 연결

암호화된 연결을 통해 `redis-cli`를 사용하려면 TLS 암호화에서 redis-cli 연결을 랩핑할 수 있는 `stunnel`과 같은 유틸리티를 설정하십시오. [stunnel](https://www.stunnel.org/index.html) 설정 단계는 다음과 같습니다.

1. stunnel을 설치하십시오.
    
    Linux용 패키지 관리자, Mac용 Homebrew를 사용하거나 자신의 플랫폼에 적합한 항목을 [다운로드](https://www.stunnel.org/downloads.html)하십시오.

2. **연결 문자열**을 구문 분석하십시오. 예를 들어, 다음과 같은 연결 문자열을 사용하는 경우
   ```text
   rediss://admin:PASSWORD@portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
   ```
   두 번째 콜론과 @ 기호 사이의 텍스트가 비밀번호입니다. @ 다음부터 다음 콜론까지의 텍스트는 호스트이며 이 콜론 다음의 숫자는 포트 번호입니다. 따라서 이 예에서는 `PASSWORD`가 비밀번호이고 `portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com`이 호스트이며 `24370`이 포트입니다.

3. 이 구성 정보를 stunnel.conf 파일에 추가하십시오. 구성은 서비스의 이름(`[redis-cli]`), 이 stunnel이 TLS 클라이언트임을 알리는 설정(`client=yes`), 연결을 허용할 IP 주소 및 포트(`accept=127.0.0.1:6830`), connect 및 연결하려는 호스트 이름과 포트(`connect=`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370`)입니다.
````text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
    ```
    배치가 `composedb.com`으로 끝나는 경우 Let's Encrypt 인증서를 사용하며 추가 작업을 수행할 필요가 없습니다. 배치가 `dblayer.com`으로 끝나는 경우 자체 서명된 인증서가 있으므로 개요의 *SSL 인증서* 탭에서 인증서 정보를 가져와서 모두 텍스트 파일(예: `cert.crt`)에 복사해야 합니다. 그런 다음 이 인증서 정보에 대한 경로를 stunnel.conf 파일에 추가하십시오.
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    verify=2  
    checkHost=sl-us-south-1-portal.7.dblayer.com 
    CAfile=/path/to/redis/cert.crt
    ```

3. 명령행에서 `stunnel` 명령을 입력하여 stunnel을 실행하십시오. 즉시 백그라운드에서 실행됩니다.
    
4. 터미널 창에서 로컬 호스트 및 포트를 대상으로 하는 `redis-cli`를 실행하고 배치의 신임 정보를 인증하십시오.
    ```shell
    redis-cli -p 6830 -a <password>
    ```

## 애플리케이션을 사용하여 연결

공식 Redis 클라이언트 라이브러리는 없습니다. Redis 사이트에 나열된 여러 언어에 대한 많은 클라이언트 라이브러리가 있습니다. [여기](http://redis.io/clients)에서 전체 목록을 볼 수 있습니다. 권장되는 클라이언트는 별표로 표시됩니다. 빠르게 시작하려는 경우 여기에 권장되는 클라이언트의 선택사항이 있습니다.       

언어|라이브러리|연결 문자열 사용
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[예](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[예](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|예, [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html) 참조

Compose 문서의 [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/), 일반적으로 사용되는 광범위한 언어에 대해 권장되는 드라이버를 살펴보는 [Compose 블로그](https://www.compose.com/articles/)도 있습니다.
