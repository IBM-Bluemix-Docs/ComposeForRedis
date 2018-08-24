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

# Conectando um aplicativo externo
{: #connecting-external-app}

Há duas maneiras de conectar um aplicativo externo ao {{site.data.keyword.composeForRedis_full}}:

- Uma **Sequência de conexões** pode ser usada por algumas bibliotecas do cliente e contém todas as informações necessárias para outras bibliotecas se conectarem; especificamente o nome do host e a porta.
  - As conexões ativadas por TLS/SSL terão um prefixo "rediss:". A maioria dos idiomas tem um driver que suporta conectar seu aplicativo com TLS/SSL. 
  - As conexões não criptografadas terão um prefixo "redis:". Isso poderá ser usado quando os seus drivers não lidarem com criptografia e você estiver ciente dos riscos potenciais de tráfego não criptografado. 

- **Linha de comandos** é um comando pré-formatado que chamará `redis-cli` com os parâmetros corretos.
  - Não há suporte TLS/SSL baseado no Redis de software livre, portanto, o utilitário de linha de comandos Redis, `redis-cli` só poderá usar essa conexão com configuração adicional.
  - O `redis-cli` pode usar uma conexão não criptografada nativamente, sem configuração adicional.

Você localizará a **Sequência de conexões** e a **Linha de comandos** na página *Visão geral* do serviço {{site.data.keyword.composeForRedis}}.


## Conectando com a linha de comandos

Em geral você usará o comando `redis-cli` para se conectar manualmente à implementação - é a maneira mais direta de trabalhar remotamente com a instalação do Redis. Ele é fornecido como parte do pacote Redis, portanto, a instalação terá que ter sido local para usá-lo. É possível fazer download da origem e compilá-la seguindo as instruções na [página de download do Redis](http://redis.io/download).

### Conexões não criptografadas

Se o seu Redis não estiver protegido por criptografia do TLS, que é a Sequência de conexões, mostrar `redis:`, então, pegue a sequência do campo **Linha de comandos** que é exibida e cole-a em seu terminal:
```shell
$ redis-cli -h sl-us-south-1-portal.7.dblayer.com -p 23870 -a <password>
sl-us-south-1-portal.7.dblayer.com:23870> set hello "world"
OK
sl-us-south-1-portal.7.dblayer.com:23870> get hello
"world" 
```
É possível testar sua conexão executando alguns comandos simples do Redis conforme mostrado.

### Conexões ativadas por TLS/SSL

Para usar a `redis-cli` com uma conexão criptografada, configure um utilitário como `stunnel` que pode quebrar a conexão redis-cli em criptografia do TLS. As etapas para configurar o [stunnel](https://www.stunnel.org/index.html) são:

1. Instalar o stunnel
    
    Use o gerenciador de pacote para Linux, Homebrew for Mac ou capture um [download](https://www.stunnel.org/downloads.html) apropriado para sua plataforma.

2. Analise a **Sequência de conexões**. Por exemplo, com uma sequência de conexões como:
   ```text
   rediss://admin:PASSWORD@portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370
   ```
   O texto entre os segundos dois pontos e at-symbol é a senha. O texto após a @ e até os próximos dois pontos é o host e o número que segue esses dois pontos é o número da porta. Então no exemplo, `PASSWORD` é a senha, `portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com` é o host e `24370` é a porta.

3. Inclua essas informações de configuração no arquivo stunnel.conf. A configuração é um nome para um serviço (`[redis-cli]`), uma configuração que diz que esse stunnel será um cliente TLS (`client=yes`), um endereço IP e uma porta para aceitar conexões (`accept=127.0.0.1:6830`) e se conectar, o nome do host e a porta aos quais queremos nos conectar (`connect=`portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com:24370`).
    ````text
    [redis-cli]
    client=yes  
    accept=127.0.0.1:6830  
    connect=portal972-7.bmix-lon-yp-38898e17-ff6f-4340-9da8-2ba24c41e6d8.composeci-us-ibm-com.composedb.com: 24370
    ```
    Se a sua implementação terminar com `composedb.com`, ela usará certificados Let's Encrypt e nada mais terá que ser feito. Se ela terminar com `dblayer.com` então, ela terá um certificado autoassinado; você precisará obter as informações de certificado da guia *Certificado SSL* da visão geral e copiar tudo para um arquivo de texto; digamos, `cert.crt` por exemplo. Em seguida, inclua o caminho para as informações desse certificado no arquivo stunnel.conf:
    
    ```text
    [ redis-cli ] client=yes  
    accept=127.0.0.1:6830  
    connect=sl-us-south-1-portal.7.dblayer.com: 23870 verify= 2  
    checkHost=sl-us-south-1-portal.7.dblayer.com 
    CAfile=/path/to/redis/cert.crt
    ```

3. Executar stunnel
    Digite o comando `stunnel` na linha de comandos. Ele será executado imediatamente em segundo plano.
    
4. Em uma nova janela Terminal, execute `redis-cli` apontando para o host e a porta, autentique com as credenciais da implementação.
    ```shell
    redis-cli -p 6830 -a <password>
    ```

## Conectando-se a aplicativos

Não há nenhuma biblioteca do cliente Redis oficial. Há inúmeras bibliotecas do cliente para várias linguagens que são listadas no site do Redis. É possível ver a lista integral [aqui](http://redis.io/clients). Os clientes recomendados são marcados com uma estrela. Se você deseja iniciar rapidamente, aqui está uma seleção de clientes recomendados:       

Idioma|Biblioteca|Uso da sequência de conexões
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Sim](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Sim](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Sim - veja [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

Há também um [Tour das estrelas do Redis](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) em artigos do Compose, o [Blog do Compose](https://www.compose.com/articles/) que observa os drivers recomendados para uma ampla gama de linguagens em uso comum.
