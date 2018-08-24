---

copyright:
  years: 2016,2018
lastupdated: "2018-03-27"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informazioni su {{site.data.keyword.composeForRedis}}
{: #about-compose-for-redis}

Redis è un archivio valore-chiave, in memoria, open source. I valori in Redis possono essere semplici stringhe, hash, elenchi e serie di bitmap potenti, hyperloglog e indici spaziali. Redis è ideale come cache dell'applicazione o per l'archiviazione veloce dei dati della risposta. {{site.data.keyword.composeForRedis_full}} ti fornisce una configurazione predisposta per l'alta disponibilità e la persistenza sul disco, entrambe bloccate con ulteriori funzioni di sicurezza.
{:shortdesc}

**Nota:** tutte le istanze del servizio Compose di cui è stato eseguito il provisioning prima del 14 settembre 2016 che sono ancora attive e che possono ancora essere utilizzate a cui si può fare direttamente accesso da [https://www.compose.com/](https://www.compose.com). È possibile accedere direttamente a tutte le istanze del servizio Compose di cui è stato eseguito il provisioning da questo punto in avanti ed è possibile utilizzarle nel tuo account {{site.data.keyword.cloud}}.

## Creazione di una istanza del servizio {{site.data.keyword.composeForRedis}}

Puoi creare un servizio {{site.data.keyword.composeForRedis}} dalla pagina [{{site.data.keyword.composeForRedis}}](https://console.{DomainName}/catalog/services/compose-for-redis/) nel catalogo {{site.data.keyword.cloud_notm}}.

Scegli un nome del servizio, una regione, un'organizzazione e uno spazio in cui eseguire il provisioning del servizio. Puoi utilizzare il campo **Select a database version** per scegliere tra le versioni del database disponibili.

È presente un menu a discesa per selezionare la crittografia TLS/SSL. La crittografia è impostata su **True** per impostazione predefinita. Se selezioni **False** il servizio eseguirà il provisioning senza la crittografia. Questo può essere utilizzato quando i tuoi driver non gestiscono la crittografia e sei consapevole dei potenziali rischi del traffico non crittografato. 

Quando esegui il provisioning della tua istanza {{site.data.keyword.composeForRedis}} puoi scegliere i piani *Standard* o *Enterprise*. Con il piano *Enterprise*, puoi eseguire il provisioning della tua istanza {{site.data.keyword.composeForRedis}} in un cluster {{site.data.keyword.composeEnterprise}} disponibile. {{site.data.keyword.composeEnterprise}} fornisce la sicurezza e l'isolamento necessari per la conformità aziendale e utilizza la rete dedicata per garantire le prestazioni dei database distribuiti. Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.composeEnterprise}}](/docs/services/ComposeEnterprise/index.html).

## Gestione di {{site.data.keyword.composeForRedis}}

Puoi gestire il tuo servizio dal dashboard del servizio. Qui puoi trovare le informazioni sul tuo database {{site.data.keyword.cloud_notm}} Compose e su come collegarti ad esso. Puoi anche:
- gestire i tuoi backup
- assegnare ulteriori risorse al tuo servizio
- modificare la password del servizio
- utilizzare le whitelist per limitare l'accesso ai tuoi database 

Per ulteriori informazioni, consulta [Impostazioni](./dashboard-settings.html).

{{site.data.keyword.composeForRedis}} si basa sui ruoli Cloud Foundry per gestire l'accesso al servizio. Solo gli utenti con il ruolo di sviluppatore possono visualizzare o utilizzare il dashboard del servizio. Per ulteriori informazioni sui ruoli Cloud Foundry, consulta le pagine [Cloud Foundry access](https://console.{DomainName}/docs/iam/cfaccess.html#cfaccess) e [Managing Cloud Foundry access](https://console.{DomainName}/docs/iam/mngcf.html#mngcf).
{: .tip}

## Connessione a {{site.data.keyword.composeForRedis}}

Puoi collegarti al tuo servizio utilizzando le credenziali create insieme al servizio o con le stringhe di connessione e la riga di comando forniti nella scheda *Overview* nel tuo dashboard del servizio.

## Connessione di un'applicazione {{site.data.keyword.cloud_notm}} a {{site.data.keyword.composeForRedis}}

Per collegare un'applicazione {{site.data.keyword.cloud_notm}} al tuo servizio, utilizza le credenziali create insieme al servizio. Puoi trovare le informazioni su come collegare un'applicazione {{site.data.keyword.cloud_notm}} a un servizio {{site.data.keyword.composeForRedis}} in [Connessione a un'applicazione {{site.data.keyword.cloud_notm}}](./connecting-bluemix-app.html).

## Connessione a {{site.data.keyword.composeForRedis}} dall'esterno di {{site.data.keyword.cloud_notm}}

Se desideri collegarti a {{site.data.keyword.composeForRedis}} dall'esterno di {{site.data.keyword.cloud_notm}}, puoi utilizzare la riga di comando o le stringhe di connessione fornite. Puoi trovare le informazioni su come collegarti in [Connessione a un'applicazione esterna](./connecting-external.html).
