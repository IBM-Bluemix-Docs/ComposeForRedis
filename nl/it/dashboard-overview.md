---

Copyright:
  years: 2017,2018
lastupdated: "2017-11-20"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Panoramica sul servizio

La pagina _Overview_ ti mostra le informazioni sul tuo database {{site.data.keyword.cloud}} Compose. La panoramica include le informazioni di identificazione essenziali e l'utilizzo della risorsa corrente. Troverai inoltre una sezione per le stringhe di connessione che puoi utilizzare con gli strumenti o utilizzare gli strumenti per il collegamento al tuo database.

## Dettagli della distribuzione

Il pannello _Deployment Details_ mostra i dettagli del tuo servizio.

![Dettagli della distribuzione](./images/redis-deployment-details.png "Una vista del pannello dei dettagli della distribuzione")

### Tipo

Il tipo di database offerto dal servizio e la versione che il servizio utilizza. Se è disponibile una versione più recente del database, viene visualizzata una notifica, insieme a un link alla sezione [Aggiorna versione](/docs/services/ComposeForRedis/dashboard-settings.html#upgrade-version) del tuo dashboard del servizio.

### Nome

Un identificativo interno per il servizio.

### Utilizzo

La dimensione del tuo database e la quantità di memoria fornita dal tuo piano di servizio.

## Lavori correnti

L'effettuare delle modifiche amministrative al tuo servizio (come un ridimensionamento o l'esecuzione di un backup manuale) avvia un lavoro. Mentre un lavoro è in esecuzione, viene visualizzato il pannello _Current Jobs_ nella pagina _Overview_, che visualizza il nome del lavoro e una barra di avanzamento. Quando il lavoro è completo, non viene più visualizzato il pannello _Current Jobs_ nella pagina _Overview_.

## Connessione

Esistono due modi per collegare un'applicazione esterna al tuo database. Puoi eseguire il collegamento utilizzando una **Stringa di connessione** o con una **Riga di comando**. Entrambe sono fornite nella panoramica del tuo dashboard del servizio.

### HTTPS

La stringa di connessione **HTTPS** può essere utilizzata da alcune librerie client e contiene tutte le informazioni necessarie al collegamento di altre librerie. Puoi trovare come utilizzare la stringa di connessione per il collegamento in [Connessione a un'applicazione esterna](./connecting-external.html).

**Nota:** se hai annullato la spunta della casella abilitato TLS/SSL quando è stato eseguito il provisioning del servizio, questa connessione **non** è protetta con TLS/SSL. 

### Riga di comando

La **Riga di comando** è un comando pre-formattato che richiamerà `redis-cli` con i parametri corretti. Per utilizzarla, dovrai aver installato gli strumenti client Redis nel sistema locale. Puoi trovare ulteriori informazioni su come farlo in [Connessione a un'applicazione esterna](./connecting-external.html).

## API di gestione dell'istanza

Puoi gestire il tuo servizio {{site.data.keyword.composeForRedis}} tramite l'API {{site.data.keyword.cloud_notm}} Compose.

### Endpoint fondazione

L'endpoint fondazione è formato dalla regione in cui risiede il servizio e dall'ID dell'istanza del servizio. Sarà all'inizio di ogni endpoint.

### ID distribuzione

L'ID della distribuzione è necessario per la maggior parte delle chiamate e identifica l'istanza di distribuzione specifica.

### Riferimenti

Per ulteriore documentazione e i riferimenti sull'utilizzo dell'API {{site.data.keyword.cloud_notm}} Compose, in tutti i servizi {{site.data.keyword.cloud_notm}} Compose, leggi [The {{site.data.keyword.cloud_notm}} Compose API](https://www.compose.com/articles/the-ibm-cloud-compose-api/).

