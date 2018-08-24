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

# Configuration de connexion
{: #connection-configuration}

Les connexions à la base de données {{site.data.keyword.composeForRedis_full}} sont gérées par 2 portails HAProxy. Chaque portail dispose de 64 Mo de mémoire. 

Disposer de deux portails permet aux applications de conserver une connectivité lorsque l'un des portails n'est plus accessible. Le basculement côté client relève de la responsabilité du concepteur d'applications. A moins que vous n'utilisiez un pilote qui traite entièrement les erreurs de basculement, il est conseillé de procéder comme suit :

* Utilisez un pilote qui accepte plusieurs noeuds finaux dans sa configuration de connexion.
* Vérifiez que les appels de vos applications en vue d'une lecture ou d'une écriture dans la base de données réagissent aux erreurs de manière appropriée. Ces opérations incluent :
  + la journalisation de l'erreur et la reconnexion,
  + la reconnexion et une nouvelle tentative de l'opération à l'origine de l'erreur,
  + la mise en file d'attente de l'opération ayant échoué et la planification de la reconnexion.

## Chiffrement du transport

A la mise à disposition, vous avez la possibilité d'activer TLS/SSL doublé d'un certificat Let's Encrypt sur vos portails {{site.data.keyword.composeForRedis}} HAProxy. Le chiffrement TLS/SSL n'est pas natif pour Redis. La plupart des pilotes peuvent gérer les connexions chiffrées, mais redis-cli et certains pilotes ne ne le font pas sans une configuration supplémentaire. L'activation de TLS/SSL dépendra de vos scénarios spécifiques d'utilisation. Pour plus d'informations, voir la page [Connexion d'une application externe](./connecting-external.html).

## Limites de connexion

Les connexions de base de données sont limitées à 4096 connexions par portail. Lorsque la limite de connexion est dépassée, le service ne répond plus. Vous pouvez gérer les connexions à partir de votre application à l'aide de la fonction de regroupement de connexions de votre pilote.

## Délais d'attente de proxy

Les portails HAProxy gèrent le cycle de vie des connexions entre le serveur et le client. Nous en fournissons le détail à titre de référence pour les éditeurs de routeurs et les personnes intéressées par les activités de bas niveau des connexions de base de données {{site.data.keyword.composeForEtcd}}.

Paramètre | Valeur | S'applique
----------|-----------|-----------
client | 5m | Lorsque le client doit accuser réception de données ou en envoyer.
connect | 4s | Lorsqu'une connexion est établie entre le proxy et le serveur.
server | 5m | Lorsque le serveur doit accuser réception de données ou en envoyer.
tunnel | 1d | Lorsqu'une connexion bidirectionnelle est établie entre un client et un serveur et que la connexion reste inactive dans les deux sens.
client-fin | 1h | Lorsque le client doit accuser réception de données ou en envoyer alors qu'une direction est déjà fermée.
check | 5s | En tant que vérification secondaire du délai d'attente lorsqu'une connexion est établie entre le proxy et le serveur.
{: caption="Tableau 1. Délais d'attente des portails HAProxy Redis" caption-side="top"}




