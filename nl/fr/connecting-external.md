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

# Connexion d'une application externe
{: #connecting-external-app}

Deux moyens permettent de connecter une application externe à {{site.data.keyword.composeForRedis_full}} :

- Une **chaîne de connexion**, qui peut être utilisée par certaines bibliothèques client et qui contient toutes les informations requises pour la connexion d'autres bibliothèques, notamment le nom d'hôte et le port.
  - Les connexions activées TLS/SSL ont un préfixe "rediss:". La plupart des langages disposent d'un pilote qui prend en charge la connexion de votre application avec TLS/SSL. 
  - Les connexions chiffrées ont un préfixe "redis:". Retenez cette option lorsque vos pilotes ne gèrent pas le chiffrement et que vous pressentez des risques potentiels en cas de trafic non chiffré. 

- Une **ligne de commande**, qui est une commande préformatée qui appellera `redis-cli` avec les paramètres appropriés.
  - Etant donné qu'aucune prise en charge TLS/SSL n'est intégrée à Redis open source, une configuration supplémentaire est nécessaire pour que l'utilitaire de ligne de commande Redis, `redis-cli`, puisse utiliser ce type de connexion.
  - `redis-cli` peut utiliser une connexion chiffrée en natif, sans configuration supplémentaire.

La **Chaîne de connexion** et la **Ligne de commande** sont disponibles sur la page de vue d'ensemble de votre service {{site.data.keyword.composeForRedis}}.


## Connexion avec la ligne de commande

Vous utiliserez généralement la commande `redis-cli` pour vous connecter manuellement au déploiement. C'est le moyen le plus direct pour travailler à distance avec votre installation Redis. Etant donné qu'elle est fournie dans le package Redis, vous devez l'installer en local pour l'utiliser. Vous pouvez télécharger le code source et le compiler en suivant les instructions de la [page de téléchargement de Redis](http://redis.io/download).

### Connexions non chiffrées

Si votre Redis n'est pas protégé par le chiffrement TLS, à savoir si la chaîne de connexion indique `redis:`, copiez la chaîne de la zone **Ligne de commande** qui s'affiche et collez-la dans votre terminal :
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
Vous pouvez tester la connexion en exécutant quelques commandes Redis simples comme illustré.

### Connexions activées TLS/SSL

Pour utiliser `redis-cli` avec une connexion chiffrée, configurez un utilitaire tel que `stunnel` qui peut encapsuler la connexion redis-cli dans un chiffrement TLS. La configuration de [stunnel](https://www.stunnel.org/index.html) s'effectue comme suit :

1. Installez stunnel
    
    Utilisez votre gestionnaire de package pour Linux, Homebrew pour Mac ou récupérez un [téléchargement](https://www.stunnel.org/downloads.html) approprié à votre plateforme.

2. Analysez la syntaxe de la **Chaîne de connexion**. Par exemple, une chaîne de connexion similaire à :
   ```text
   rediss://admin:PASSWORD@portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
   ```
   Le texte qui figure entre le second symbole deux-points et le symbole @ est le mot de passe. Le texte qui suit le symbole @ et jusqu'au deux-points suivants est l'hôte, et le nombre qui suit ces deux-points est le numéro de port. Ainsi, dans cet exemple, `PASSWORD` est le mot de passe, `portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com` est l'hôte et `24370` est le port.

3. Ajoutez ces informations de configuration au fichier stunnel.conf. La configuration est le nom d'un service (`[redis-cli]`), un paramètre qui indique que ce stunnel est un client TLS (`client=yes`), une adresse IP et un port qui acceptent les connexions sur (`accept=127.0.0.1:6830`) et se connectent, ainsi que le nom d'hôte et le port vers lesquels vous voulez vous connecter (`connect=`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370`).
    ````text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
    ```
    Si votre déploiement se termine par `composedb.com`, il utilise des certificats Let's Encrypt et ne nécessite aucune autre action de votre part. S'il se termine par `dblayer.com`, il possède un certificat autosigné et vous devez alors obtenir les informations de certificat depuis l'onglet *Certificat SSL* de la vue d'ensemble et les copier intégralement dans un fichier texte, par exemple, `cert.crt`. Ajoutez ensuite le chemin menant à ces informations de certificat dans le fichier stunnel.conf :
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    verify=2  
    checkHost=sl-us-south-1-portal.7.dblayer.com 
    CAfile=/path/to/redis/cert.crt
    ```

3. Exécutez stunnel
    Saisissez la commande `stunnel` sur la ligne de commande. Elle s'exécute immédiatement en arrière-plan.
    
4. Dans une nouvelle fenêtre de terminal, exécutez `redis-cli` en pointant sur le port et le système hôte local et authentifiez-vous avec les données d'identification du déploiement.
    ```shell
    redis-cli -p 6830 -a <password>
    ```

## Connexion avec des applications

Il n'existe pas de bibliothèque client Redis officielle. Le site de Redis répertorie un grand nombre de bibliothèque client pour de nombreux langages. Vous en trouverez la liste complète [ici](http://redis.io/clients). Les client recommandés sont repérés d'une étoile. Si vous voulez démarrer rapidement, voici une sélection de client recommandés :       

Langage|Bibliothèque|Chaîne de connexion à utiliser
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Oui](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Oui](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Oui- voir [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

Vous disposez également d'un [Tour des étoiles Redis](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) dans des articles de Compose, du [blogue de Compose](https://www.compose.com/articles/) qui commente les pilotes recommandés pour une grande palette de langages communément utilisé.
