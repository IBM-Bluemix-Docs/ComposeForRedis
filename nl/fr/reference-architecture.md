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

# Architecture 
{: #architecture}

## Réplication

Un service {{site.data.keyword.composeForRedis_full}} utilise [Redis Sentinel](https://redis.io/topics/sentinel) pour fournir haute disponibilité et surveillance pour vos bases de données. Chaque service se compose de trois noeuds de données ; tous exécutent le processus sentinel et deux exécutent le processus redis. Lorsque vous sélectionnez une région où le service est déployé, les trois noeuds de données sont propagés dans les zones de disponibilité de la région et vos données sont répliquées dans les trois noeuds. Lorsqu'un membre de données n'est plus accessible, votre cluster continue à fonctionner normalement.

## Chiffrement de disque

Tous les services {{site.data.keyword.composeForRedis}} disposent du chiffrement au repos. Vos données résident sur des serveurs où le chiffrement au niveau volume est activé. 

Etant donné que {{site.data.keyword.composeForRedis}} est un service géré, les opérateurs {{site.data.keyword.cloud}} Compose peuvent voir les données. Outre le chiffrement du disque, il est recommandé de chiffrer vos informations personnelles avant de les stocker dans la base de données ou d'utiliser des extensions ou des fonctions permettant d'activer le chiffrement sur la base de données elle-même. Même si ces méthodes risquent d'avoir un impact sur la facilité d'utilisation ou les performances, il est conseillé de s'assurer que les informations personnelles sont protégées par un chiffrement.

## Mise à l'échelle automatique

Les ressources sont automatiquement mises à l'échelle en fonction de l'utilisation totale de la mémoire des bases de données Redis. Le stockage est basé sur un rapport de mémoire RAM mise à disposition de 1 sur 1. Ces ressources sont intégrées en tant qu'unités.

La mise à l'échelle automatique est conçue pour répondre aux tendances à court et moyen termes de votre base de données. Votre service est contrôlé toutes les minutes et, s'il est à court de mémoire RAM, des unités supplémentaires sont attribuées au déploiement. 

Une mise à l'échelle automatique ne réduit pas la taille des déploiements où l'utilisation du disque/de la mémoire à diminué. Les ressources mises à disposition de vos bases de données sont conservées pour les besoins ultérieurs ou jusqu'à ce que vous réduisiez manuellement votre déploiement.
{: .tip}
