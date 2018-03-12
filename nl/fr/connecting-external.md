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

La **Chaîne de connexion** et la **Ligne de commande** sont disponibles sur la page *Overview* de votre service {{site.data.keyword.composeForRedis}}.


## Connexion avec la ligne de commande

Vous utiliserez généralement la commande `redis-cli` pour vous connecter manuellement au déploiement. C'est le moyen le plus direct pour travailler à distance avec votre installation Redis. Etant donné qu'elle est fournie dans le package Redis, vous devez l'installer en local pour l'utiliser. Vous pouvez télécharger le code source et le compiler en suivant les instructions de la [page de téléchargement de Redis](http://redis.io/download).

### Connexions activées TLS/SSL
Pour utiliser `redis-cli` avec une connexion chiffrée, configurez un utilitaire tel que `stunnel` afin de gérer le chiffrement. La configuration de [stunnel](https://www.stunnel.org/index.html) s'effectue comme suit :

1. Installez stunnel
    
    Utilisez votre gestionnaire de package pour Linux, Homebrew pour Mac ou récupérez un [téléchargement](https://www.stunnel.org/downloads.html) approprié à votre plateforme.

2. Ajoutez les informations de la zone **Ligne de commande** dans le fichier stunnel.conf
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    ```
    
    Si votre déploiement dispose d'un certificat autosigné, vous devrez ajouter les informations relatives au certificat dans le fichier stunnel.conf :
    
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
    
4. Exécutez `redis-cli` en pointant sur le port et l'hôte locaux, authentifiez-vous avec les données d'identification du déploiement.

    ```shell
    redis-cli -p 6830 -a <password>
    ```

### Connexions HTTP non chiffrées
Copiez la chaîne que contient la zone **Ligne de commande** et collez-la sur votre terminal :
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
Vous pouvez tester la connexion en exécutant quelques commandes Redis simples comme illustré. 


## Connexion avec des applications

Il n'existe pas de bibliothèque client Redis officielle. Le site de Redis répertorie un grand nombre de bibliothèque client pour de nombreux langages. Vous en trouverez la liste complète [ici](http://redis.io/clients). Les client recommandés sont repérés d'une étoile. Si vous voulez démarrer rapidement, voici une sélection de client recommandés :       

Langage|Bibliothèque|Chaîne de connexion à utiliser
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Oui](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Oui](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Oui- voir [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

Vous disposez également d'un [Tour des étoiles Redis](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) dans des articles de Compose, du [blogue de Compose](https://www.compose.com/articles/) qui commente les pilotes recommandés pour une grande palette de langages communément utilisé.
