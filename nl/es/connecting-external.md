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

# Conexión de una aplicación externa
{: #connecting-external-app}

Hay dos formas de conectar una aplicación externa a {{site.data.keyword.composeForRedis_full}}:

- Algunas bibliotecas de cliente pueden utilizar una **serie de conexión**, que contiene toda la información necesaria para que se conecten otras bibliotecas; en concreto el nombre de host y el puerto.
  - Las conexiones habilitadas para TLS/SSL tendrán un prefijo "rediss:". La mayoría de los idiomas tienen un controlador que soporta la conexión de la aplicación con TLS/SSL. 
  - Las conexiones no cifradas tendrán un prefijo "redis:". Esto puede utilizarse cuando los controladores no manejan el cifrado y es consciente de los riesgos potenciales de tráfico cifrado. 

- La **línea de mandatos** es un mandato preformateado que invocará `redis-cli` con los parámetros correctos.
  - No hay soporte TLS/SSL integrado en Redis de código abierto, por lo que el programa de utilidad de línea de mandatos Redis, `redis-cli`, solo puede utilizar esta conexión con la configuración adicional.
  - `redis-cli` puede utilizar una conexión no cifrada de forma nativa, sin configuración adicional.

Encontrará la **Serie de conexión** y la **Línea de mandatos** en la página *Visión general* del servicio de {{site.data.keyword.composeForRedis}}.


## Conexión con la línea de mandatos

Generalmente utilizará el mandato `redis-cli` para conectarse manualmente al despliegue - es la forma más directa de trabajar de forma remota con la instalación de Redis. Viene como parte del paquete Redis, por lo que deberá tenerlo instalado de forma local para utilizarlo. Puede descargar el origen y compilarlo siguiendo las instrucciones de la [página de descarga de Redis](http://redis.io/download).

### Conexiones no cifradas

Si Redis no está protegido por cifrado TLS, es decir, se muestra `redis:` en Serie de conexión, tome la serie del campo **Línea de mandatos** que se visualiza y péguela en su terminal:
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
Para probar la conexión, puede ejecutar algunos mandatos sencillos de Redis como los que se muestran.

### Conexiones habilitadas para TLS/SSL

Para utilizar `redis-cli` con una conexión cifrada, configure un programa de utilidad como `stunnel` que pueda envolver la conexión redis-cli en cifrado TLS. Los pasos para configurar [stunnel](https://www.stunnel.org/index.html) son:

1. Instale stunnel
    
    Utilice el gestor de paquetes para Linux, Homebrew para Mac, o seleccione una [descarga](https://www.stunnel.org/downloads.html) apropiada para la plataforma.

2. Analice la **Serie de conexión**. Por ejemplo, con una serie de conexión como esta:
   ```text
   rediss://admin:PASSWORD@portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
   ```
   El texto entre los segundos dos puntos y el símbolo de arroba es la contraseña. El texto que aparece tras la @ y hasta los siguientes dos puntos es el host, y el número que aparece tras esos dos puntos es el número de puerto. Por lo tanto, en el ejemplo, `PASSWORD` es la contraseña, `portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com` es el host y `24370` es el puerto.

3. Añada esta información de configuración al archivo stunnel.conf. La configuración es un nombre para un servicio (`[redis-cli]`), un valor que indica que este stunnel será un cliente TLS (`client=yes`), una dirección IP y puerto para aceptar conexiones en (`accept=127.0.0.1:6830`) y conectarse, el nombre de host y el puerto al que desea conectarse (`connect=`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370`).
    ````text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
    ```
    Si el despliegue termina con `composedb.com`, utiliza los certificados de Let's Encrypt y no es necesario realizar ninguna otra acción. Si termina con `dblayer.com`, tiene un certificado autofirmado, y será necesario obtener la información de certificado del separador *Certificado SSL* y copiarla en un archivo de texto; por ejemplo, `cert.crt`. A continuación, añada la vía de acceso a esta información de certificado al archivo stunnel.conf:
    
    ```text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com:23870
    verify=2  
    checkHost=sl-us-south-1-portal.7.dblayer.com
    CAfile=/path/to/redis/cert.crt
    ```

3. Ejecute stunnel
    Escriba el mandato `stunnel` en la línea de mandatos. Se ejecutará de forma inmediata en segundo plano.
    
4. En una nueva ventana de terminal, ejecute `redis-cli` apuntando al host y al puerto local, autentique con las credenciales del despliegue.
    ```shell
    redis-cli -p 6830 -a <password>
    ```

## Conexión con aplicaciones

No hay ninguna biblioteca cliente oficial de Redis. Existen varias bibliotecas cliente para muchos lenguajes que aparecen listadas en el sitio de Redis. Puede consultar la lista completa [aquí](http://redis.io/clients). Los clientes recomendados están marcados con una estrella. Si desea comenzar a trabajar rápidamente, aquí tiene una selección de clientes recomendados:       

Lenguaje|Biblioteca|Uso de serie de conexión
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Sí](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Sí](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Sí - Consulte [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

También hay una [Ruta guiada de las estrellas de Redis](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) en artículos de Compose, el [blog de Compose blog](https://www.compose.com/articles/) que examina los controladores recomendados para una amplia gama de lenguajes comúnmente utilizados.
