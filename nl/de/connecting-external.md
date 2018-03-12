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

# Externe Anwendung verbinden
{: #connecting-external-app}

Es gibt zwei Möglichkeiten, eine externe Anwendung mit {{site.data.keyword.composeForRedis_full}} zu verbinden:

- Eine **Verbindungszeichenfolge** kann von bestimmten Clientbibliotheken verwendet werden und enthält alle Informationen, die andere Bibliotheken zum Herstellen einer Verbindung benötigen, insbesondere den Hostnamen und den Port.
  - Verbindungen, für die TLS/SSL aktiviert ist, sind mit einem Präfix "rediss:" gekennzeichnet. Die meisten Sprachen haben einen Treiber, der die Verbindung Ihrer Anwendung mit TLS/SSL unterstützt. 
  - Nicht verschlüsselte Verbindungen sind mit einem Präfix "redis:" gekennzeichnet. Dies kann verwendet werden, wenn Ihr Treiber die Verschlüsselung nicht unterstützt und Ihnen die potenziellen Risiken beim unverschlüsselten Datenverkehr bekannt sind. 

- Die **Befehlszeile** ist ein vorformatierter Befehl, der `redis-cli` mit den korrekten Parametern aufruft.
  - Open-Source-Redis umfasst keine TLS/SSL-Unterstützung, sodass das Redis-Befehlszeilendienstprogramm `redis-cli` diese Verbindung nur mit zusätzlicher Konfiguration verwenden kann.
  - `redis-cli` kann eine nicht verschlüsselte Verbindung ohne zusätzliche Konfiguration nativ verwenden.

Sie finden sowohl die **Verbindungszeichenfolge** als auch die **Befehlszeile** auf der Seite *Übersicht* Ihres {{site.data.keyword.composeForRedis}}-Service.


## Verbindung über die Befehlszeile herstellen

In der Regel verwenden Sie den Befehl `redis-cli`, um eine manuelle Verbindung zur Bereitstellung herzustellen. Das ist die direkteste Möglichkeit, über Fernzugriff mit Ihrer Redis-Installation zu arbeiten. Da der Befehl im Redis-Paket enthalten ist, müssen Sie Redis lokal installieren, um ihn verwenden zu können. Anhand der Anweisungen auf der [Redis-Downloadseite](http://redis.io/download) können Sie die Quelle herunterladen und kompilieren.

### Für TLS/SSL aktivierte Verbindungen
Wenn Sie `redis-cli` mit einer verschlüsselten Verbindung verwenden wollen, richten Sie ein Dienstprogramm wie `stunnel` ein, das die Verschlüsselung  handhaben kann. Die Schritte zum Einrichten von [stunnel](https://www.stunnel.org/index.html) sind:

1. stunnel installieren
    
    Verwenden Sie Ihren Paketmanager für Linux, Homebrew für Mac oder wählen Sie einen [Download](https://www.stunnel.org/downloads.html) für Ihre jeweilige Plattform.

2. Die Informationen aus dem Feld **Befehlszeile** in die stunnel.conf-Datei einfügen
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    ```
    
    Wenn Ihre Bereitstellung über ein selbst signiertes Zertifikat verfügt, müssen Sie die Zertifikatsinformationen in die stunnel.conf-Datei einfügen:
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    verify=2  
    checkHost=sl-us-south-1-portal.7.dblayer.com 
    CAfile=/path/to/redis/cert.crt
    ```

3. stunnel ausführen
    
    Geben Sie den `stunnel`-Befehl in der Befehlszeile ein. Das Programm wird sofort im Hintergrund ausgeführt.
    
4. `redis-cli` mit Zeiger auf den lokalen Host und Port ausführen und mit Berechtigungsnachweise der Bereitstellung authentifizieren.

    ```shell
    redis-cli -p 6830 -a <password>
    ```

### Nicht verschlüsselte HTTP-Verbindungen
Verwenden Sie die Zeichenfolge aus dem Feld **Befehlszeile** und fügen Sie sie in Ihrem Terminal ein:
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
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
