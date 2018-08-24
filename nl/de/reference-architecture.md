---
copyright:
  years: 2016,2018
lastupdated: "2018-06-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Architektur 
{: #architecture}

## Replikation

Ein {{site.data.keyword.composeForRedis_full}}-Service verwendet [Redis Sentinel](https://redis.io/topics/sentinel), um Hochverfügbarkeit und Überwachung für Ihre Datenbanken bereitzustellen. Jeder Service besteht aus drei Datenknoten, wobei alle drei Knoten den Sentinel-Prozess und zwei den redis-Prozess ausführen. Wenn Sie eine Region auswählen, in der der Service bereitgestellt wird, werden die drei Knoten auf die Verfügbarkeitszonen der Region verteilt und Ihre Daten werden auf diesen Knoten repliziert. Sollte ein Datenelement (Member) nicht mehr erreichbar sein, setzt Ihr Cluster seinen Betrieb trotzdem ordnungsgemäß fort.

## Plattenverschlüsselung

Für alle {{site.data.keyword.composeForRedis}}-Services erfolgt die Verschlüsselung im Ruhezustand. Ihre Daten befinden sich auf Servern, auf denen die Verschlüsselung auf Datenträgerebene aktiviert ist. 

Da es sich bei {{site.data.keyword.composeForRedis}} um einen verwalteten Service handelt, sind Operatoren von Compose auf {{site.data.keyword.cloud}} in der Lage, Daten zu sehen. Wenn Sie persönliche Informationen in Ihrer Datenbank speichern, wird zusätzlich zur Plattenverschlüsselung empfohlen, Informationen zu verschlüsseln, bevor sie gespeichert werden, oder Erweiterungen bzw. Features zu verwenden, um die Verschlüsselung auf der Datenbank selbst zu ermöglichen. Diese Methoden können zwar den Bedienungskomfort oder die Leistung beeinträchtigen, doch es hat sich bewährt, den Schutz persönlicher Informationen mit Verschlüsselung sicherzustellen.

## Automatische Skalierung

Die Ressourcen werden basierend auf der Gesamtspeicherbelegung der Redis-Datenbanken automatisch skaliert. Der Speicher basiert auf einem Faktor des bereitgestellten Arbeitsspeichers im Verhältnis von 1:1. Diese Ressourcen werden als Einheiten gebündelt.

Die automatische Skalierung ist so konzipiert, dass sie als Reaktion auf die kurz-bis mittelfristigen Trends Ihrer Datenbank erfolgt. Ihr Service wird in Minutenintervallen überprüft. Wenn der Arbeitsspeicher für den Service knapp zu werden droht, werden der Bereitstellung weitere Einheiten zugeordnet. 

Bei der automatischen Skalierung wird kein Scale-down für Bereitstellungen durchgeführt, bei denen sich die Platten-/Speicherbelegung verringert hat. Die für Ihre Datenbanken bereitgestellten Ressourcen bleiben für zukünftige Anforderungen weiterhin bestehen, sofern Sie Ihre Bereitstellung nicht per Scale-down manuell nach unten skalieren.
{: .tip}
