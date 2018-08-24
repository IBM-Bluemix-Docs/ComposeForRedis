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

# Connessione a un'applicazione {{site.data.keyword.cloud_notm}}

Per collegare un'applicazione {{site.data.keyword.cloud}} al tuo servizio, utilizza le credenziali create quando è stato eseguito il provisioning del servizio. 'applicazione di esempio illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForRedis_full}} utilizzando le credenziali fornite e come creare un database e come leggere e scrivere in esso.

## Collegamento utilizzando l'applicazione di esempio 'Hello World'

L'applicazione di esempio [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForRedis}} utilizzando le credenziali fornite. L'applicazione crea, legge da, e scrive su un database.

Scarica l'applicazione di esempio e segui le istruzioni nel file readme. In seguito, nella pagina dei dettagli della tua applicazione in {{site.data.keyword.cloud_notm}}, fai clic su **Visualizza applicazione** per visualizzare il contenuto della tabella *esempi*.

## Credenziali disponibili

Nome campo|Descrizione
----------|-----------
`uri`|L'URI da utilizzare quando esegui il collegamento al servizio, include lo schema (redis:), il nome utente e la password amministratore, il nome host del server e il numero di porta a cui collegarsi.
`uri_direct_1`|Un URI secondario che può essere utilizzato durante il collegamento al servizio. Il formato è lo stesso di `uri`.
`ca_certificate_base64` `(facoltativo)`|Un certificato autofirmato con codifica base64 che viene utilizzato per confermare che un'applicazione sia collegata al server corretto. Il certificato è presente solo sui servizi che hanno un certificato autofirmato invece di un certificato di Let's Encrypt. Devi decodificare la chiave prima di utilizzarla, come mostrato nell'applicazione di esempio.
`uri_cli`|Una riga di comando `redis-cli` che esegue il collegamento all'istanza del database.
`deployment_id`|Un identificativo interno per il servizio come creato in Compose.
`db_type`|Il tipo di database offerto dal servizio; in questo caso `redis`.
`name`|Il nome di distribuzione del database.
{: caption="Tabella 1. Credenziali di Compose for Redis" caption-side="top"}

**Nota:** due portali `haproxy` forniscono l'accesso al servizio Redis. Possono essere utilizzati sia `uri` che `uri_direct_1` per il collegamento. Nelle tue applicazioni, passa da `uri` a `uri_direct_1` per gestire le risposte agli errori di connessione.
