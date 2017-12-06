---

copyright:
  years: 2017
lastupdated: "2017-06-07"
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

- La **Riga di comando** è un comando pre-formattato che richiamerà `redis-cli` con i parametri corretti. 

Troverai entrambe nella pagina *Overview* del tuo servizio {{site.data.keyword.composeForRedis}}.

## Connessione con la riga di comando

Normalmente starai utilizzando il comando `redis-cli` per collegarti manualmente alla distribuzione - è il modo più diretto per utilizzare in remoto la tua installazione Redis. Viene fornito come parte del pacchetto Redis, per cui dovrai avere Redis installato localmente per utilizzarlo. Su Mac OS X, un ottimo modo per ottenere Redis è utilizzando Homebrew.

1. Installa [brew](http://brew.sh)
2. Installa redis con `brew install redis` per essere velocemente operativo.

Su Linux, fai riferimento al tuo gestore del pacchetto delle distribuzioni per l'ultima build. Se non sei così propenso, puoi [download the source](http://redis.io/download) ed eseguirne la build per conto tuo. 

Dalla riga di comando TCP, taglialo e incollalo nel tuo terminale nel seguente modo:
```shell
$ redis-cli -h portal.brilliant-redis-41.compose-3.composedb.com -p 15639 -a secretpassword
portal.brilliant-redis-41.compose-3.composedb.com:15639> set hello "world"
OK
portal.brilliant-redis-41.compose-3.composedb.com:15639> get hello
"world"
portal.brilliant-redis-41.compose-3.composedb.com:15639> 

```
Puoi verificare la tua connessione eseguendo alcuni comandi Redis semplici come mostrato.

## Connessione con le applicazioni 

Non esiste una libreria client Redis ufficiale. Esistono molte librerie client per molti linguaggi elencate nel sito Redis. Puoi visualizzare l'elenco completo [qui](http://redis.io/clients). I client consigliati sono contrassegnati con una stella. Se desideri iniziare velocemente, questa è una selezione di client consigliati:       

Linguaggio|Libreria |Utilizzo stringa connessione
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Sì](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Sì](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Sì - Consulta [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

È anche presente un [Tour of the Redis stars](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) negli articoli Compose, il [Compose blog](https://www.compose.com/articles/) che cerca i driver consigliati per un'ampia gamma di linguaggi di utilizzo comune.
