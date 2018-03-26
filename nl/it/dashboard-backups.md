---

copyright:
  years: 2017,2018
lastupdated: "2017-07-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Backup
{: #backups}

Puoi creare e scaricare i backup dalla scheda _Backups_ della pagina _Manage_ del tuo dashboard del servizio. Sono disponibili backup giornalieri, settimanali, mensili e su richiesta. Vengono conservati in base alla seguente pianificazione:

Tipo di backup|Pianificazione conservazione
----------|-----------
Giornaliero|I backup giornalieri sono conservati per 7 giorni
Settimanale|I backup settimanali sono conservati per 4 settimane
Mensile|I backup mensili sono conservati per 3 mesi
Su richiesta|Il backup su richiesta viene conservato. Il backup conservato è sempre il più recente backup su richiesta.
{: caption="Tabella 1. Pianificazione conservazione backup" caption-side="top"}

Le politiche di conservazione e di pianificazione del backup sono fissate. Se hai bisogno di conservare più backup rispetto a quelli consentiti dalla pianificazione di conservazione, devi scaricare i backup e conservare gli archivi in base ai tuoi requisiti di business.

## Visualizzazione dei backup esistenti

I backup giornalieri del tuo database vengono automaticamente pianificati. Per visualizzare i tuoi backup esistenti, passa alla pagina *Manage* del tuo dashboard del servizio. 

![Backup](./images/redis-backups-show.png "Un elenco di backup nel dashboard del servizio")

Fai clic sulla riga corrispondente per espandere le opzioni per ogni backup disponibile.

![Opzioni backup](./images/redis-backups-options.png "Opzioni per il backup.") 

## Creazione di un backup su richiesta

Come per i backup pianificati puoi creare un backup manualmente. Per creare un backup manuale, passa alla pagina *Manage* del tuo dashboard del servizio e fai clic su *Backup now*.

## Scaricamento di un backup

Per scaricare un backup, passa alla pagina *Manage* del tuo dashboard del servizio e fai clic su *Download* nella riga corrispondente del backup che desideri scaricare.

## Contenuti del backup

Redis salva un'istantanea binaria dei tuoi dati per impostazione predefinita. Il file dump.rdb può quindi essere utilizzato come backup per il ripristino temporizzato. Per dividere l'istantanea Redis, in modo che tutto il lavoro sull'istantanea venga eseguito dal processo secondario mentre il processo principale continua a gestire i tuoi dati normalmente. Il processo di backup non interessa la tua applicazione o database. Potrai scaricare una copia dei tuoi backup o ripristinarli direttamente in una nuova distribuzione.

## Utilizzo di un backup con un database locale

Puoi utilizzare il tuo backup {{site.data.keyword.composeForRedis}} per eseguire una copia locale del tuo database.

1. Sposta il tuo file dump.rdb nella sua nuova directory, chiamata 'db'.
2. Abbiamo bisogno di un file di configurazione Redis per avviare l'istanza Redis, se vorrai copiare un file redis.conf dalla tua installazione nella tua directory db con il file dump.rdb. Ad esempio, se hai installato Redis su OSX con homebrew, il file redis.conf è in `/usr/local/etc`, per cui dalla directory db esegui, `cp /usr/local/etc/redis.conf .`
3. Modifica il file di configurazione in modo che punti alla nostra directory corrente all'avvio. Apri redis.conf con un editor di testo e modifica la riga `dir /usr/local/var/db/redis/` con `dir .`. Salva il file e esci.
4. Avvia il server redis nella directory db fornendo il file di configurazione: `redis-server redis.conf`.

## Ripristino di un backup

Per ripristinare un backup in una nuova istanza, segui le istruzioni per visualizzare i backup esistenti, quindi fai clic sulla riga corrispondente per espandere le opzioni del backup che desideri scaricare. Fai clic sul pulsante **Restore**. Viene visualizzato un messaggio per farti sapere che è stato avviato un ripristino. La nuova istanza del servizio sarà automaticamente denominata "redis-restore-[timestamp]" e visualizzata nel tuo dashboard dopo l'avvio del provisioning.
