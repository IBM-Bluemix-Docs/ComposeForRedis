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

### Nicht verschlüsselte Verbindungen

Falls Ihr Redis nicht durch TLS-Verschlüsselung geschützt ist, das heißt, wenn in der Verbindungszeichenfolge `redis:` angezeigt wird, verwenden Sie die angezeigte Zeichenfolge aus dem Feld **Befehlszeile** und fügen Sie sie in Ihrem Terminal ein: 
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
Sie können Ihre Verbindung testen, indem Sie einige einfache Redis-Befehle wie angezeigt ausführen.

### Für TLS/SSL aktivierte Verbindungen

Wenn Sie die `redis-cli` mit einer verschlüsselten Verbindung verwenden wollen, richten Sie ein Dienstprogramm wie `stunnel` ein, das die Verbindung zur redis-cli in eine TLS-Verschlüsselung einschließen kann. Die Schritte zum Einrichten von [stunnel](https://www.stunnel.org/index.html) sind:

1. 'stunnel' installieren
    
    Verwenden Sie Ihren Paketmanager für Linux, Homebrew für Mac oder wählen Sie einen [Download](https://www.stunnel.org/downloads.html) für Ihre jeweilige Plattform.

2. Führen Sie ein Parsing für die **Verbindungszeichenfolge** aus. Zum Beispiel für eine Verbindungszeichenfolge wie: 
   ```text
   rediss://admin:PASSWORD@portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
   ```
   Der Text zwischen dem zweiten Doppelpunkt und dem At-Zeichen (@) ist das Kennwort. Der Text nach dem At-Zeichen (@) bis zum nächsten Doppelpunkt ist der Hostname und die Anzahl nach dem Doppelpunkt ist die Portnummer. Also ist das Kennwort in diesem Beispiel `PASSWORD` und `portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com` ist der Hostname während `24370` die Portnummer ist. 

3. Fügen Sie diese Konfigurationsdaten zur Datei 'stunnel.conf' hinzu. Die Konfiguration besteht aus einem Namen für einen Service (`[redis-cli]`), einer Einstellung, die aussagt, dass dieser 'stunnel' ein TLS-Client sein wird (`client=yes`), einer IP-Adresse und einem Port, an denen die Verbindungen akzeptiert und hergestellt werden (`accept=127.0.0.1:6830`), dem Hostnamen und dem Port, zu dem wir eine Verbindung herstellen möchten (`connect=`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370`). 
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
    ```
    Wenn Ihre Bereitstellung mit `composedb.com` endet, verwendet sie 'Let's Encrypt'-Zertifikate und Sie müssen nichts unternehmen. Wenn sie mit `dblayer.com` endet, dann verwendet die Bereitstellung selbst signierte Zertifikate und Sie müssen die Zertifikatinformationen von der Registerkarte *SSL-Zertifikat* der Übersicht abrufen und alle Informationen in eine Textdatei kopieren. Diese kann zum Beispiel den Namen `cert.crt` erhalten. Fügen Sie dann den Pfad zu diesen Zertifikatsinformationen zur Datei 'stunnel.conf' hinzu. 
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    verify=2  
    checkHost=sl-us-south-1-portal.7.dblayer.com 
    CAfile=/path/to/redis/cert.crt
    ```

3. Führen Sie 'stunnel' aus.
    Geben Sie den Befehl `stunnel` in der Befehlszeile ein. Das Programm wird sofort im Hintergrund ausgeführt.
    
4. Führen Sie in einem neuen Terminalfenster `redis-cli` aus und verweisen Sie dabei auf den lokalen Host und den Port und authentifizieren Sie sich mit den Berechtigungsnachweisen der Bereitstellung. 
    ```shell
    redis-cli -p 6830 -a <password>
    ```

## Verbindung mit Anwendungen herstellen

Es gibt keine offizielle Redis-Clientbibliothek. Es gibt zahlreiche Clientbibliotheken für viele Sprachen, die auf der Redis-Website aufgeführt sind. Die vollständige Liste finden Sie [hier](http://redis.io/clients). Die empfohlenen Clients sind mit einem Stern markiert. Um Ihnen einen schnellen Start zu ermöglichen, sind hier einige empfohlene Clients aufgeführt:       

Sprache|Bibliothek|Verwendung der Verbindungszeichenfolge
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Ja](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Ja](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Ja - Siehe [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

Außerdem gibt es in den Compose-Artikeln eine [Tour der Redis-Sterne](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) sowie den [Compose-Blog](https://www.compose.com/articles/), der die empfohlenen Treiber für weitere gängige Sprachen untersucht.
