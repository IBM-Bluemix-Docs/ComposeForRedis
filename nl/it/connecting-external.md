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

# Connessione a un'applicazione esterna
{: #connecting-external-app}

Esistono due modi per collegare un'applicazione esterna a {{site.data.keyword.composeForRedis_full}}:

- Può essere utilizzata una **Stringa di connessione** in alcune librerie client che contiene tutte le informazioni necessarie per il collegamento di altre librerie; nello specifico il nome host e la porta.
  - Le connessioni abilitate TLS/SSL avranno un prefisso "rediss:". La maggior parte dei linguaggi hanno un driver che supporta la connessione alla tua applicazione con TLS/SSL. 
  - Le connessioni non codificate avranno un prefisso "redis:". Questo può essere utilizzato quando i tuoi driver non gestiscono la codifica e sei consapevole dei potenziali rischi del traffico non codificato. 

- La **Riga di comando** è un comando pre-formattato che richiamerà `redis-cli` con i parametri corretti.
  - Non esiste il supporto TLS/SSL nel open source Redis, per cui il programma di utilità della riga di comando Redis, `redis-cli` può utilizzare solo questa connessione con configurazione aggiuntiva.
  - `redis-cli` può utilizzare una connessione non codificata in modo nativo, senza configurazione aggiuntiva.

Troverai sia la **Stringa di connessione** che la **Riga di comando** nella pagina *Overview* del tuo servizio {{site.data.keyword.composeForRedis}}.


## Connessione con la riga di comando

Normalmente utilizzi il comando `redis-cli` per collegarti manualmente alla distribuzione - è il modo più diretto per utilizzare in remoto la tua installazione Redis. Viene fornito come parte del pacchetto Redis, per cui lo dovrai avere installato localmente per utilizzarlo. Puoi scaricare l'origine e compilarla seguendo le istruzioni nella [Pagina di scaricamento Redis](http://redis.io/download).

### Connessioni abilitate TLS/SSL
Per utilizzare `redis-cli` con una connessione codificata configura un programma di utilità come `stunnel` per gestire la modifica. La procedura per configurare [stunnel](https://www.stunnel.org/index.html) è:

1. Installa stunnel
    
    Utilizza il tuo gestore pacchetti per Linux, Homebrew per Mac o prendi uno [scaricamento](https://www.stunnel.org/downloads.html) appropriato per la tua piattaforma.

2. Aggiungi le informazioni dal campo **Command Line** del file stunnel.conf
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    ```
    
    Se la tua distribuzione ha un certificato autofirmato, dovrai aggiungere le informazioni del certificato al file stunnel.conf:
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    verify=2  
    checkHost=sl-us-south-1-portal.7.dblayer.com 
    CAfile=/path/to/redis/cert.crt
    ```

3. Esegui stunnel
    
    Immetti il comando `stunnel` nella riga di comando. Sarà immediatamente eseguito in background.
    
4. Esegui `redis-cli` puntando alla porta e all'host locale, autenticati con le credenziali della distribuzione.

    ```shell
    redis-cli -p 6830 -a <password>
    ```

### Connessioni HTTP non codificate
Prendi la stringa dal campo **Command Line** e incollala nel tuo terminale:
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
Puoi verificare la tua connessione eseguendo alcuni comandi Redis semplici come mostrato. 


## Connessione con le applicazioni

Non esiste una libreria client Redis ufficiale. Esistono molte librerie client per molti linguaggi elencate nel sito Redis. Puoi visualizzare l'elenco completo [qui](http://redis.io/clients). I client consigliati sono contrassegnati con una stella. Se desideri iniziare velocemente, questa è una selezione di client consigliati:       

Linguaggio|Libreria|Utilizzo stringa connessione
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Sì](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Sì](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Sì - Consulta [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

È anche presente un [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) negli articoli Compose, il [Compose blog](https://www.compose.com/articles/) che cerca i driver consigliati per un'ampia gamma di linguaggi di utilizzo comune.
