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

# Arquitectura 
{: #architecture}

## Réplica

Un servicio de {{site.data.keyword.composeForRedis_full}} utiliza [Redis Sentinel](https://redis.io/topics/sentinel) para proporcionar alta disponibilidad y supervisión para las bases de datos. Cada servicio consta de tres nodos de datos; los tres ejecutan el proceso de sentinel y dos ejecutan el proceso de redis. Cuando selecciona una región en la que se despliega el servicio, los tres nodos se dispersan en las zonas de disponibilidad de la región, y los datos se replican en todos ellos. Si un miembro de datos se vuelve inaccesible, el clúster seguirá funcionando de forma normal.

## Cifrado de disco

Todos los servicios de {{site.data.keyword.composeForRedis}} tienen cifrado en reposo. Los datos residen en servidores que tienen el cifrado de nivel de volumen habilitado. 

Puesto que {{site.data.keyword.composeForRedis}} es un servicio gestionado, es posible que los operadores de {{site.data.keyword.cloud}} Compose vean los datos. Además del cifrado de disco, le recomendamos que, si está almacenando información personal en la base de datos, cifre información antes de almacenarla o de utilizar extensiones o características para habilitar el cifrado en la propia base de datos. Si bien estos métodos pueden afectar a la usabilidad o al rendimiento, es una buena práctica asegurarse de que la información personal esté protegida con cifrado.

## Escalado automático

Los recursos se escalan automáticamente basándose en el uso de memoria total de las bases de datos Redis. El almacenamiento se basa en una proporción de RAM suministrada de 1:1. Estos recursos se empaquetan como unidades.

El escalado automático está diseñado para responder a las tendencias a corto y medio plazo de la base de datos. Cada minuto, el servicio está marcado y si se está quedando corto en RAM, se asignan más unidades al despliegue. 

El escalado automático no reduce los despliegues en los que el uso de disco/memoria se ha reducido. Los recursos suministrados a las bases de datos permanecerán para sus necesidades futuras, o hasta que reduzca el despliegue manualmente.
{: .tip}
