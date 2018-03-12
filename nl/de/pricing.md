---

copyright:
  years: 2016,2018
lastupdated: "2018-01-03"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Preisstruktur
{: #pricing}

## Basiskonfiguration
Die Basiskonfiguration des {{site.data.keyword.composeForRedis_full}}-Service umfasst zwei redis/sentinel-Knoten mit jeweils 256 MB Hauptspeicher und 256 MB Speicher. Dies entspricht 1 Ressourceneinheit. Zum Service _gehören_ Replikation und Hochverfügbarkeit. In jedem Einzelpreis sind jeweils die Ressourcenkosten für beide Knoten _enthalten_.

Zur Basiskonfiguration gehören zudem ein dedizierter sentinel-Knoten für die Verarbeitung der Regler sowie ein HAProxy-Portal zur Verwaltung von Verbindungen. Der sentinel-Knoten und das HAProxy-Portal haben jeweils 64 MB Hauptspeicher.

### Kosten
Die Basisservicekonfiguration hat einen Festpreis. Den Grundpreis in Ihrer Landeswährung finden Sie über die entsprechenden Katalogkacheln auf {{site.data.keyword.cloud_notm}}. Der Grundpreis in US-Dollar beträgt zum Beispiel $13/Monat.

## Erweiterungsoptionen
Wenn Sie zusätzlichen Hauptspeicher für Ihren Service benötigen, können Sie die zugeordneten Ressourcen in einem Verhältnis von 1:1 von Plattenspeicher zu Speichereinheit erhöhen. Eine {{site.data.keyword.composeForRedis}}-Einheit besteht aus 256 MB Speicher und 256 MB Hauptspeicher- Im Preis pro Einheit sind die Kosten für die Erweiterung der Ressourcen auf beiden Knoten _enthalten_.

### Kosten
Jede zusätzliche Einheit (256 MB Speicher/256 MB Hauptspeicher) hat einen Einzelpreis, der auf der {{site.data.keyword.cloud_notm}}-Katalogkachel für den Service in Ihrer Landeswährung aufgelistet ist. In US-Dollar beträgt der Preis für jede zusätzliche Einheit $13. Mit zunehmender _Gesamtgröße_ Ihrer {{site.data.keyword.composeForRedis}}-Services verringert sich der Preis pro Einheit, wie aus der folgenden Tabelle zur gestaffelten Preisstruktur hervorgeht.

### Gestaffelte Preisstruktur
Anzahl der Einheiten|Einzelpreis
----------|-----------
1 - 9 Einheiten|Basiseinzelpreis -- $13,00 USD/Einheit
10 - 24 Einheiten|10% Ermäßigung --$11,70 USD/Einheit
25 - 49 Einheiten|20% Ermäßigung -- $10,40 USD/USD/Einheit
50 - 99 Einheiten|30% Ermäßigung -- $9,10 USD/Einheit
100 - 499 Einheiten|40% Ermäßigung -- $7,80 USD/Einheit
500 - 999 Einheiten|50% Ermäßigung -- $6,50 USD/Einheit
1.000 - 4.999 Einheiten|60% Ermäßigung -- $5,20 USD/Einheit
5.000+ Einheiten|70% Ermäßigung -- $3,90 USD/Einheit
{: caption="Tabelle 1. Gestaffelte Preisstruktur von {{site.data.keyword.composeForRedis}}" caption-side="top"}

