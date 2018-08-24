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

# Architettura 
{: #architecture}

## Replica

Un servizio {{site.data.keyword.composeForRedis_full}} utilizza [Redis Sentinel](https://redis.io/topics/sentinel) per fornire l'alta disponibilità e il monitoraggio per i tuoi database. Ogni servizio è costituito da tre nodi di dati; tutti e tre eseguono il processo sentinel e due il redis. Quando selezioni una regione in cui viene distribuito il servizio, i tre nodi vengono distribuiti alle zone di disponibilitàdella regione e i tuoi dati vengono replicati su di essi. Se un membro dei dati diventa non raggiungibile, il cluster continuerà a funzionare normalmente.

## Crittografia del disco

Tutti i servizi {{site.data.keyword.composeForRedis}} hanno la crittografia a riposo. I tuoi dati si trovano su server che hanno la crittografia a livello di volume abilitata. 

Poiché questo {{site.data.keyword.composeForRedis}} è un servizio gestito, è possibile agli operatori {{site.data.keyword.cloud}} Compose di visualizzare i dati. In aggiunta alla crittografia del disco, ti consigliamo che se stai memorizzando le informazioni personali nel tuo database, di codificare prima le informazioni archiviandole o utilizzando le estensioni o le funzioni per abilitare la crittografia sul database stesso. Anche se questi metodi possono influire sull'usabilità o sulle prestazioni, è buona norma assicurarsi che le informazioni personali siano protette con la crittografia.

## Scalabilità automatica

Le risorse vengono ridimensionate automaticamente in base all'utilizzo della memoria totale dei database Redis. L'archiviazione è basata su un rapporto di RAM di cui viene eseguito il provisioning di 1:1. Queste risorse sono raccolte in bundle come unità.

Il ridimensionamento automatico è progettato per rispondere alle tendenze a medio e a lungo termine del tuo database. Il tuo servizio viene controllato ogni minuto e, se sta esaurendo la RAM, delle ulteriori unità vengono assegnate alla distribuzione. 

Il ridimensionamento automatico non riduce le distribuzioni in cui l'utilizzo di disco/memoria si è ridotto. Le risorse di cui è stato eseguito il provisioning ai tuoi database rimarranno per le tue future esigenze oppure finché non riduci manualmente la tua distribuzione.
{: .tip}
