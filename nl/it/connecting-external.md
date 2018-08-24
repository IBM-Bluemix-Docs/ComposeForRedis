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
  - Le connessioni non crittografate avranno un prefisso "redis:". Questo può essere utilizzato quando i tuoi driver non gestiscono la crittografia e sei consapevole dei potenziali rischi del traffico non crittografato. 

- La **Riga di comando** è un comando pre-formattato che richiamerà `redis-cli` con i parametri corretti.
  - Non esiste il supporto TLS/SSL nel open source Redis, per cui il programma di utilità della riga di comando Redis, `redis-cli` può utilizzare solo questa connessione con configurazione aggiuntiva.
  - `redis-cli` può utilizzare una connessione non crittografata in modo nativo, senza configurazione aggiuntiva.

Troverai sia la **Stringa di connessione** che la **Riga di comando** nella pagina *Overview* del tuo servizio {{site.data.keyword.composeForRedis}}.


## Connessione con la riga di comando

Normalmente utilizzi il comando `redis-cli` per collegarti manualmente alla distribuzione - è il modo più diretto per utilizzare in remoto la tua installazione Redis. Viene fornito come parte del pacchetto Redis, per cui lo dovrai avere installato localmente per utilizzarlo. Puoi scaricare l'origine e compilarla seguendo le istruzioni nella [Pagina di scaricamento Redis](http://redis.io/download).

### Connessioni non crittografate

Se il tuo Redis non è protetto dalla crittografia TLS, ossia la stringa di connessione presenta `redis:`, prendi la stringa dal campo **Command Line** visualizzato e incollala nel tuo terminale:
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
Puoi verificare la tua connessione eseguendo alcuni comandi Redis semplici come mostrato.

### Connessioni abilitate TLS/SSL

Per utilizzare `redis-cli` con una connessione crittografata, configura un programma di utilità come `stunnel` che includerà la connessione redis-cli nella crittografia TLS. La procedura per configurare [stunnel](https://www.stunnel.org/index.html) è:

1. Installa stunnel
    
    Utilizza il tuo gestore pacchetti per Linux, Homebrew per Mac o prendi uno [scaricamento](https://www.stunnel.org/downloads.html) appropriato per la tua piattaforma.

2. Analizza la **stringa di connessione**. Ad esempio, con una stringa di connessione come:
   ```text
   rediss://admin:PASSWORD@portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
   ```
   Il testo tra il secondo carattere due punti e il simbolo @ è la password. Il testo dopo il simbolo @ e fino al successivo carattere due punti è l'host e il numero dopo tale carattere due punti è il numero porta. Quindi, nell'esempio, `PASSWORD` è la password, `portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com` è l'host e `24370` p la porta.

3. Aggiungi queste informazioni di configurazione al file stunnel.conf. La configurazione è un nome per un servizio (`[redis-cli]`), un'impostazione che indica che questo stunnel sarà un client TLS (`client=yes`), un indirizzo IP e una porta su cui accettare le connessioni (`accept=127.0.0.1:6830`) e connect, il nome host e la porta a cui vogliamo stabilire la connessione (`connect=`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370`).
    ````text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
    ```
    Se la tua distribuzione termina con `composedb.com`, utilizza i certificati Let's Encrypt e non occorre fare altro. Se finisce con `dblayer.com`, ha un certificato autofirmato; dovrai ottenere le informazioni sul certificato dalla scheda *SSL Certificate* della panoramica e copiarlo integralmente in un file di testo, ad esempio `cert.crt`. Aggiungi quindi il percorso a queste informazioni sul certificato nel file stunnel.conf:
    
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
    Immetti il comando `stunnel` alla riga di comando. Sarà immediatamente eseguito in background.
    
4. In una nuova finestra del terminale, esegui `redis-cli` puntando all'host e alla porta locali ed esegui l'autenticazione con le credenziali della distribuzione.
    ```shell
    redis-cli -p 6830 -a <password>
    ```

## Connessione con le applicazioni

Non esiste una libreria client Redis ufficiale. Esistono molte librerie client per molti linguaggi elencate nel sito Redis. Puoi visualizzare l'elenco completo [qui](http://redis.io/clients). I client consigliati sono contrassegnati con una stella. Se desideri iniziare velocemente, questa è una selezione di client consigliati:       

Linguaggio|Libreria|Utilizzo stringa connessione
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Sì](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Sì](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Sì - Consulta [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

È anche presente un [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) negli articoli Compose, il [Compose blog](https://www.compose.com/articles/) che cerca i driver consigliati per un'ampia gamma di linguaggi di utilizzo comune.
