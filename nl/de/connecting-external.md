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

# Externe Anwendung verbinden
{: #connecting-external-app}

Es gibt zwei Möglichkeiten, eine externe Anwendung mit {{site.data.keyword.composeForRedis_full}} zu verbinden:

- Eine **Verbindungszeichenfolge** kann von bestimmten Clientbibliotheken verwendet werden und enthält alle Informationen, die andere Bibliotheken zum Herstellen einer Verbindung benötigen, insbesondere den Hostnamen und den Port.

- Die **Befehlszeile** ist ein vorformatierter Befehl, der `redis-cli` mit den korrekten Parametern aufruft. 

Beides finden Sie auf der Seite *Übersicht* Ihres {{site.data.keyword.composeForRedis}}-Service.

## Verbindung über die Befehlszeile herstellen

In der Regel verwenden Sie den Befehl `redis-cli`, um eine manuelle Verbindung zu der Bereitstellung herzustellen. Das ist die direkteste Möglichkeit, über Fernzugriff mit Ihrer Redis-Installation zu arbeiten. Da er im Redis-Paket enthalten ist, müssen Sie Redis lokal installieren, um ihn verwenden zu können. Unter Mac OS X können Sie Redis gut abrufen, indem Sie Homebrew verwenden.

1. Installieren Sie [brew](http://brew.sh).
2. Installieren Sie Redis mit dem Befehl `brew install redis`, um betriebsbereit zu sein.

Wenden Sie sich unter Linux an Ihren Verteilerpaketmanager, um den neuesten Build zu erhalten. Wenn Sie entsprechende Begabungen haben, können Sie auch die [Quelle herunterladen](http://redis.io/download) und den Build selbst erstellen. 

Nehmen Sie die TCP-Befehlszeile, schneiden Sie sie aus und fügen Sie sie in Ihr Terminal ein. Das geht wie folgt:
```shell
$ redis-cli -h portal.brilliant-redis-41.compose-3.composedb.com -p 15639 -a secretpassword
portal.brilliant-redis-41.compose-3.composedb.com:15639> set hello "world"
OK
portal.brilliant-redis-41.compose-3.composedb.com:15639> get hello
"world"
portal.brilliant-redis-41.compose-3.composedb.com:15639>

```
Sie können Ihre Verbindung testen, indem Sie einige einfache Redis-Befehle wie angezeigt ausführen.

## Verbindung mit Anwendungen herstellen

Es gibt keine offizielle Redis-Clientbibliothek. Es gibt zahlreiche Clientbibliotheken für viele Sprachen, die auf der Redis-Website aufgeführt sind. Die vollständige Liste finden Sie [hier](http://redis.io/clients). Die empfohlenen Clients sind mit einem Stern markiert. Um Ihnen einen schnellen Start zu ermöglichen, sind hier einige empfohlene Clients aufgeführt:       

Sprache|Bibliothek|Verwendung der Verbindungszeichenfolge
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Ja](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Ja](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Ja - Siehe [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

Außerdem gibt es in den Compose-Artikeln eine [Tour der Redis-Sterne](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) sowie den [Compose-Blog](https://www.compose.com/articles/), der die empfohlenen Treiber für weitere gängige Sprachen untersucht.
