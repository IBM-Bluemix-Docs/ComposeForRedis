---

copyright:
  years: 2016,2018
lastupdated: "2017-10-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Acerca de {{site.data.keyword.composeForRedis}}
{: #about-compose-for-redis}

Redis es un almacén de valor de clave, en memoria, de código abierto. Los valores de Redis pueden ser cadenas sencillas, hash, listas y conjuntos o mapas de bits potentes, registros de hyperlog e índices geoespaciales. Redis es ideal como memoria caché de aplicaciones o como almacén de datos de respuesta rápida. {{site.data.keyword.composeForRedis_full}} le proporciona una configuración preajustada para alta disponibilidad y persistencia en disco, bloqueados con características de seguridad adicionales.
{:shortdesc}

**Nota:** Cualquier instancia de servicio de Compose proporcionada antes del 14 de septiembre de 2016 que siga activa se puede seguir utilizando y se puede acceder a ella directamente en [https://www.compose.com/](https://www.compose.com). Se puede acceder directamente a cualquier instancia de servicio de Compose que se proporcione desde este momento en adelante y se utilizará dentro de la cuenta de {{site.data.keyword.cloud}}.

## Creación de una instancia de servicio de {{site.data.keyword.composeForRedis}}

Puede crear un servicio de {{site.data.keyword.composeForRedis}} desde la [página de {{site.data.keyword.composeForRedis}}](https://console.{DomainName}/catalog/services/compose-for-redis/) en el catálogo de {{site.data.keyword.cloud_notm}}.

Elija un nombre de servicio, y una región, organización y espacio en los que suministrar el servicio. Puede utilizar el campo **Seleccionar una versión de base de datos** para elegir entre las versiones de bases de datos disponibles.

Hay un desplegable para seleccionar el cifrado TLS/SSL. Se establece en el cifrado **True** de forma predeterminada. Si selecciona **False**, el servicio se suministrará sin cifrado. Esto puede utilizarse cuando los controladores no manejan el cifrado y es consciente de los riesgos potenciales de tráfico cifrado. 

Cuando suministre la instancia de {{site.data.keyword.composeForRedis}}, puede elegir los planes *Estándar* o *Empresa*. Con el plan *Empresa*, puede suministrar la instancia de {{site.data.keyword.composeForRedis}} en un clúster disponible de {{site.data.keyword.composeEnterprise}}. {{site.data.keyword.composeEnterprise}} proporciona la seguridad y nivel de aislamiento necesarios para el cumplimiento de las reglas empresariales y utiliza redes dedicadas para garantizar el rendimiento de las bases de datos desplegadas. Consulte la [documentación de Compose Enterprise](../ComposeEnterprise/index.html) para ver más detalles.

## Gestión de {{site.data.keyword.composeForRedis}}

Puede gestionar el servicio desde el panel de control del servicio. Aquí encontrará información sobre su base de datos de {{site.data.keyword.cloud_notm}} Compose y cómo conectarse a la misma. También puede:
- gestionar copias de seguridad
- asignar más recursos para el servicio
- cambiar la contraseña del servicio
- utilizar listas blancas para restringir el acceso a las bases de datos. 
Para obtener más información, consulte [Valores](./dashboard-settings.html).

## Conexión a {{site.data.keyword.composeForRedis}}

Puede conectarse a su servicio utilizando las credenciales que se crean junto con el servicio, o con las series de conexión y la línea de mandatos que se proporcionan en el separador *Visión general* del panel de control del servicio.

## Conexión de una aplicación {{site.data.keyword.cloud_notm}} a {{site.data.keyword.composeForRedis}}

Para conectar una aplicación {{site.data.keyword.cloud_notm}} al servicio, utilice las credenciales que se crean junto con el servicio. Encontrará información sobre cómo conectar una aplicación {{site.data.keyword.cloud_notm}} a un servicio {{site.data.keyword.composeForRedis}} en el apartado [Conexión de una aplicación {{site.data.keyword.cloud_notm}}](./connecting-bluemix-app.html).

## Conexión a {{site.data.keyword.composeForRedis}} desde fuera de {{site.data.keyword.cloud_notm}}

Si desea conectarse a {{site.data.keyword.composeForRedis}} desde fuera de {{site.data.keyword.cloud_notm}}, puede utilizar las series de conexión proporcionadas o la línea de mandatos. Encontrará información sobre cómo conectar en el apartado [Conexión de una aplicación externa](./connecting-external.html).
