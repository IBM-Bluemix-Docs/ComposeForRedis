---

copyright:
  years: 2016,2018
lastupdated: "2017-10-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informationen zu {{site.data.keyword.composeForRedis}}
{: #about-compose-for-redis}

Redis ist ein speicherinterner Open-Source-Schlüssel/Wert-Speicher. Die Werte in Redis können einfache Zeichenfolgen, Hashwerte, Listen und Gruppen oder leistungsfähige Bitmapdateien, HyperLOG-Protokolle und geografisch-räumliche Indizes sein. Redis eignet sich ideal als Anwendungscache oder als Datenspeicher für schnelle Antworten. {{site.data.keyword.composeForRedis_full}} bietet Ihnen eine Konfiguration, die für hohe Verfügbarkeit und persistente Plattenspeicherung voreingestellt ist, alles mit speziellen Sicherheitsfunktionen gesichert.
{:shortdesc}

**Hinweis:** Alle Compose-Serviceinstanzen, die vor dem 14. September 2016 bereitgestellt wurden und noch aktiv sind, können weiterhin verwendet werden und sind über [https://www.compose.com/](https://www.compose.com) zugänglich. Jede Compose-Serviceinstanz, die ab diesem Punkt bereitgestellt wird, ist direkt über Ihr {{site.data.keyword.cloud}}-Konto zugänglich und kann dort verwendet werden.

## {{site.data.keyword.composeForRedis}}-Serviceinstanz erstellen

Sie können einen {{site.data.keyword.composeForRedis}}-Service über die [{{site.data.keyword.composeForRedis}}-Seite](https://console.{DomainName}/catalog/services/compose-for-redis/) im {{site.data.keyword.cloud_notm}}-Katalog erstellen.

Wählen Sie einen Servicenamen und eine Region, eine Organisation und einen Bereich zur Bereitstellung des Service aus. Im Feld **Datenbankversion auswählen** können Sie eine der verfügbaren Datenbankversionen auswählen.

Über ein Dropdown-Menü kann die TLS/SSL-Verschlüsselung ausgewählt werden. Die Verschlüsselung ist standardmäßig auf **True** gesetzt. Wenn Sie **False** auswählen, wird der Service ohne Verschlüsselung bereitgestellt. Dies kann verwendet werden, wenn Ihr Treiber die Verschlüsselung nicht unterstützt und Ihnen die potenziellen Risiken beim unverschlüsselten Datenverkehr bekannt sind. 

Bei der Bereitstellung Ihrer {{site.data.keyword.composeForRedis}}-Instanz können Sie den Plan *Standard* oder *Enterprise* auswählen. Mit dem Plan *Enterprise* können Sie Ihre {{site.data.keyword.composeForRedis}}-Instanz in einem {{site.data.keyword.composeEnterprise}}-Cluster bereitstellen. {{site.data.keyword.composeEnterprise}} stellt die für die Konformität mit Enterprise erforderliche Sicherheit und Isolation bereit und stellt mithilfe eines dedizierten Netzbetriebs die Leistung der bereitgestellten Datenbanken sicher. Weitere Details finden Sie in der [Dokumentation zu Compose Enterprise](../ComposeEnterprise/index.html).

## {{site.data.keyword.composeForRedis}} verwalten

Sie können Ihren Service über das Service-Dashboard verwalten. Hier finden Sie Informationen zu Ihrer {{site.data.keyword.cloud_notm}} Compose-Datenbank und dazu, wie Sie eine Verbindung zu ihr herstellen. Außerdem können Sie:
- Ihre Sicherungen verwalten
- Ihrem Service mehr Ressourcen zuordnen
- Das Servicekennwort ändern
- Whitelists verwenden, um den Zugriff auf Ihre Datenbank zu beschränken. 
Weitere Informationen finden Sie im Abschnitt [Einstellungen](./dashboard-settings.html).

## Verbindung zu {{site.data.keyword.composeForRedis}} herstellen

Sie können mit den Berechtigungsnachweisen, die zusammen mit Ihrem Service erstellt werden, oder mithilfe der Verbindungszeichenfolgen und der Befehlszeile, die auf der Registerkarte *Übersicht* Ihres Service-Dashboards bereitgestellt werden, eine Verbindung zu dem Service herstellen.

## Verbindung von einer {{site.data.keyword.cloud_notm}}-Anwendung zu {{site.data.keyword.composeForRedis}} herstellen

Um eine {{site.data.keyword.cloud_notm}}-Anwendung mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Informationen zum Herstellen einer Verbindung von einer {{site.data.keyword.cloud_notm}}-Anwendung zu einem {{site.data.keyword.composeForRedis}}-Service finden Sie im Abschnitt [{{site.data.keyword.cloud_notm}}-Anwendung verbinden](./connecting-bluemix-app.html).

## Verbindung zu {{site.data.keyword.composeForRedis}} außerhalb von {{site.data.keyword.cloud_notm}} herstellen

Wenn Sie außerhalb von {{site.data.keyword.cloud_notm}} eine Verbindung zu {{site.data.keyword.composeForRedis}} herstellen wollen, können Sie dazu die bereitgestellten Verbindungszeichenfolgen oder die Befehlszeile verwenden. Informationen dazu, wie sich eine Verbindung herstellen lässt, finden Sie im Abschnitt [Externe Anwendung verbinden](./connecting-external.html).
