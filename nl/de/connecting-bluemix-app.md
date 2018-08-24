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

# {{site.data.keyword.cloud_notm}}-Anwendung verbinden

Verbinden Sie eine {{site.data.keyword.cloud}}-Anwendung mit Ihrem Service mithilfe der Berechtigungsnachweise dieses Service, die bei dessen Bereitstellung erstellt werden. Die Beispielapp veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung zu einem {{site.data.keyword.composeForRedis_full}}-Service mithilfe der bereitgestellten Berechtigungsnachweise und die Vorgehensweise zur Erstellung einer Datenbank sowie Lese- und Schreibvorgänge in dieser Datenbank.

## Verbindung mithilfe der Beispielapp 'Hello World' herstellen

Die Beispielapp [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung zu einem {{site.data.keyword.composeForRedis}}-Service mithilfe der bereitgestellten Berechtigungsnachweise. Die Anwendung erstellt eine Datenbank, liest daraus und schreibt darin.

Laden Sie die Beispielapp herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in {{site.data.keyword.cloud_notm}} auf **App anzeigen**, um den Inhalt der Tabelle *examples* anzuzeigen.

## Verfügbare Berechtigungsnachweise

Feldname|Beschreibung
----------|-----------
`uri`|Der bei der Verbindungsherstellung zum Service zu verwendende URI, in dem Folgendes enthalten ist: das Schema (redis:), Benutzername und Kennwort des Administrators, der Hostname des Servers und die Nummer des Ports, zu dem die Verbindung hergestellt werden soll.
`uri_direct_1`|Ein sekundärer URI, der bei der Verbindungsherstellung zum Service verwendet werden kann. Das Format ist dasselbe wie für `uri`.
`ca_certificate_base64` `(optional)`|Ein selbst signiertes Zertifikat in Base64-Codierung, mit dem bestätigt wird, dass eine Anwendung eine Verbindung zum entsprechenden Server herstellt. Das Zertifikat ist nur für Services vorhanden, die ein selbst signiertes Zertifikat anstelle eines Zertifikats von Let's Encrypt verwenden. Der Schlüssel muss vor seiner Verwendung decodiert werden, wie in der Beispielanwendung gezeigt.
`uri_cli`|Eine `redis-cli`-Befehlszeile, die eine Verbindung zur Datenbankinstanz herstellt.
`deployment_id`|Eine interne ID für den Service entsprechend der Erstellung in Compose.
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `redis`.
`name`|Der Name der Datenbankimplementierung.
{: caption="Tabelle 1. Compose for Redis - Berechtigungsnachweise" caption-side="top"}

**Hinweis:** Zwei `haproxy`-Portale bieten Zugriff auf den Redis-Service. Sowohl `uri` als auch `uri_direct_1` können zum Herstellen der Verbindung verwendet werden. In Ihrer Anwendung wechseln Sie zwischen `uri` und `uri_direct_1`, um die Reaktionen auf Verbindungsfehler zu verwalten.
