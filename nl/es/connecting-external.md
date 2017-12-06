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

# Conexión de una aplicación externa
{: #connecting-external-app}

Hay dos formas de conectar una aplicación externa a {{site.data.keyword.composeForRedis_full}}:

- Algunas bibliotecas de cliente pueden utilizar una **serie de conexión**, que contiene toda la información necesaria para que se conecten otras bibliotecas; en concreto el nombre de host y el puerto.

- La **línea de mandatos** es un mandato preformateado que invocará `redis-cli` con los parámetros correctos.

Encontrará ambas en la página *Visión general* del servicio {{site.data.keyword.composeForRedis}}.

## Conexión con la línea de mandatos

Generalmente utilizará el mandato `redis-cli` para conectar manualmente con el despliegue - es la forma más directa de trabajar de forma remota con la instalación de Redis. Viene como parte del paquete Redis, por lo que deberá tener Redis instalado localmente para utilizarlo. En Mac OS X, una buena manera de obtener Redis es mediante Homebrew.

1. Instale [brew](http://brew.sh).
2. Instale redis con `brew install redis` para ponerlo a trabajar.

En Linux, consulte el gestor del paquete de distribuciones de ver la última compilación. Si lo desea, puede [descargar el código fuente](http://redis.io/download) y crearlo usted mismo. 

En la línea de mandatos de TCP, copie y pegue el código en el terminal, del siguiente modo:
```shell
$ redis-cli -h portal.brilliant-redis-41.compose-3.composedb.com -p 15639 -a secretpassword
portal.brilliant-redis-41.compose-3.composedb.com:15639> set hello "world"
OK
portal.brilliant-redis-41.compose-3.composedb.com:15639> get hello
"world"
portal.brilliant-redis-41.compose-3.composedb.com:15639> 

```
Para probar la conexión, puede ejecutar algunos mandatos sencillos de Redis como los que se muestran. 

## Conexión con aplicaciones

No hay ninguna biblioteca cliente oficial de Redis. Existen varias bibliotecas cliente para muchos lenguajes que aparecen listadas en el sitio de Redis. Puede consultar la lista completa [aquí](http://redis.io/clients). Los clientes recomendados están marcados con una estrella. Si desea comenzar a trabajar rápidamente, aquí tiene una selección de clientes recomendados:       

Lenguaje|Biblioteca|Uso de serie de conexión
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Sí](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Sí](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Sí - Consulte [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

También hay una [Ruta guiada de las estrellas de Redis](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) en artículos de Compose, el [blog de Compose blog](https://www.compose.com/articles/) que examina los controladores recomendados para una amplia gama de lenguajes comúnmente utilizados.
