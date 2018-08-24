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

# Configuración de conexión
{: #connection-configuration}

Las conexiones de base de datos {{site.data.keyword.composeForRedis_full}} están gestionadas por 2 portales HAProxy. Cada portal tiene 64 MB de memoria. 

Los dos portales para permitir a las aplicaciones mantener la conectividad en el caso de que uno de los portales pase a no ser accesible. La migración tras error en el lado del cliente es responsabilidad del diseñador de aplicaciones. A menos que esté trabajando con un controlador que gestione por completo los errores de migración tras error, debe:

* Utilizar un controlador que acepte varios puntos finales en su configuración de conexión.
* Asegurarse de que las llamadas de aplicaciones para leer o escribir en la base de datos reaccionen a los errores adecuadamente. Entre las opciones, se incluyen:
  + Registrar el error y reconectar.
  + Reconectar y reintentar la operación que ha provocado el error.
  + Poner en cola la operación que ha fallado y planificar la reconexión.

## Cifrado en tránsito

En la provisión, tiene la opción de habilitar TLS/SSL respaldado por un certificado de Let's Encrypt en los portales de HAProxy de {{site.data.keyword.composeForRedis}}. El cifrado TLS/SSL no es nativo de Redis. La mayoría de los controladores pueden gestionar las conexiones cifradas, pero redis-cli y algunos controladores no lo hacen sin una configuración adicional. Si habilita TLS/SSL, dependerá del caso de uso específico. Para obtener más información, consulte la página [Conexión de una aplicación externa](./connecting-external.html).

## Límites de conexión

Las conexiones de base de datos tienen un límite de conexión de 4096 conexiones por portal. El exceso del límite de conexión hará que el servicio no responda. Puede gestionar las conexiones desde la aplicación a través de la característica de agrupación de conexiones del controlador.

## Tiempos de espera del proxy

Los portales HAProxy gestionan el ciclo de vida de las conexiones entre el servidor y el cliente. Los detallamos aquí como una referencia para los escritores de controladores y otros que tienen interés en la actividad de bajo nivel de las conexiones de base de datos de {{site.data.keyword.composeForEtcd}}.

Valor | Valor | Se aplica
----------|-----------|-----------
cliente | 5m | Cuando se espera que el cliente reconozca o envíe datos.
connect | 4s | Cuando se realiza una conexión entre el proxy y el servidor.
servidor | 5m | Cuando se espera que el servidor reconozca o envíe datos.
tunnel | 1d | Cuando se establece una conexión bidireccional entre un cliente y un servidor, y la conexión permanece inactiva en ambas direcciones.
client-fin | 1h | Cuando se espera que el cliente reconozca o envíe datos mientras una dirección ya está cerrada.
check | 5s | Como una comprobación de tiempo de espera secundaria, cuando se realiza una conexión entre el proxy y el servidor.
{: caption="Tabla 1. Tiempos de espera de HAProxy de Redis" caption-side="top"}




