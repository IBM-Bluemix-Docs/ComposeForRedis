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

# Connexion d'une application externe
{: #connecting-external-app}

Deux moyens permettent de connecter une application externe à {{site.data.keyword.composeForRedis_full}} :

- Une **chaîne de connexion**, qui peut être utilisée par certaines bibliothèques client et qui contient toutes les informations requises pour la connexion d'autres bibliothèques, notamment le nom d'hôte et le port.

- Une **ligne de commande**, qui est une commande préformatée qui appellera `redis-cli` avec les paramètres appropriés.

Les deux sont disponibles sur la page *Vue d'ensemble* du service {{site.data.keyword.composeForRedis}}.

## Connexion avec la ligne de commande

Vous utiliserez généralement la commande `redis-cli` pour vous connecter manuellement aux déploiement. C'est le moyen le plus direct pour travailler à distance avec votre installation Redis. Etant donné qu'elle est fournie dans le package Redis, vous devez installer Redis en local pour l'utiliser. Sur Mac OS X, le bon moyen pour obtenir Redis est d'utiliser Homebrew.

1. Installez [brew](http://brew.sh)
2. Installez Redis avec `brew install redis` pour être opérationnel.

Sous Linux, reportez-vous au gestionnaire de package de distributions pour la version la plus récente. Si ça vous tente, vous pouvez [télécharger la source](http://redis.io/download) et procéder vous-même à la génération. 

Coupez puis collez la ligne de commande TCP sur votre terminal comme suit :
```shell
$ redis-cli -h portal.brilliant-redis-41.compose-3.composedb.com -p 15639 -a secretpassword
portal.brilliant-redis-41.compose-3.composedb.com:15639> set hello "world"
OK
portal.brilliant-redis-41.compose-3.composedb.com:15639> get hello
"world"
portal.brilliant-redis-41.compose-3.composedb.com:15639> 

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
