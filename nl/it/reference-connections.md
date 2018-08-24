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

# Configurazione della connessione
{: #connection-configuration}

Le connessioni database {{site.data.keyword.composeForRedis_full}} sono gestite da 2 portali HAProxy. Ogni portale ha 64 MB di memoria. 

I due portali consentono alle applicazioni di mantenere la connettività se uno dei portali diventa irraggiungibile. Il failover al lato client è responsabilità del progettista dell'applicazione. A meno che tu non stia lavorando con un driver che gestisce completamente gli errori di failover, devi:

* Lavorare con un driver che accetta più endpoint nella sua configurazione della connessione.
* Assicurarti che le chiamate delle tue applicazioni per leggere o scrivere nel database reagiscano in modo appropriato agli errori. Le opzioni includono:
  + Registrazione dell'errore e riconnessione.
  + Riconnessione e nuovo tentativo dell'operazione che ha causato l'errore.
  + Accodamento dell'operazione non riuscita e pianificazione della riconnessione.

## Crittografia in transito

Al momento del provisioning, hai l'opzione di abilitare TLS/SSL supportata da un certificato Let's Encrypt nei tuoi portali {{site.data.keyword.composeForRedis}} HAProxy. La crittografia TLS/SSL non è nativa Redis. La maggior parte dei driver possono gestire le connessioni crittografate, ma redis-cli ed alcuni driver non possono senza un'ulteriore configurazione. Se abilitare TLS/SSL dipenderà dal tuo caso di utilizzo specifico. Per ulteriori informazioni, vedi la pagina [Connessione a un'applicazione esterna](./connecting-external.html).

## Limiti connessioni

Le connessioni database hanno un limite di connessioni di 4096 connessioni per portale. Se si supera il limite di connessioni, il tuo servizio smetterà di rispondere. Puoi gestire le connessioni dalla tua applicazione tramite la funzione di pooling di connessioni del tuo driver.

## Timeout proxy

I portali HAProxy gestiscono il ciclo di vita delle connessioni tra il server e il client. Li descriviamo qui in dettaglio come guida di riferimento per gli scrittori di driver e per gli altri che hanno un interesse nell'attività di basso livello delle connessioni al database {{site.data.keyword.composeForEtcd}}.

Impostazione | Valore | Applicazione
----------|-----------|-----------
client | 5m | Quando si prevede che il client riconosca o invii i dati.
connect | 4s | Quando si sta stabilendo una connessione tra il proxy e il server.
server | 5m | Quando si prevede che il server riconosca o invii i dati.
tunnel | 1g | Quando viene stabilita una connessione bidirezionale tra un client e un server e la connessione rimane inattiva in entrambe le direzioni.
client-fin | 1o | Quando si prevede che il client riconosca o invii dati mentre una direzione è già stata arrestata.
check | 5s | Come un controllo di timeout secondario quando si sta stabilendo una connessione tra il proxy e il server.
{: caption="Tabella 1. Timeout Redis HAProxy" caption-side="top"}




