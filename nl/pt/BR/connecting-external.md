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

# Conectando um aplicativo externo
{: #connecting-external-app}

Há duas maneiras de conectar um aplicativo externo ao {{site.data.keyword.composeForRedis_full}}:

- Uma **Sequência de conexões** pode ser usada por algumas bibliotecas do cliente e contém todas as informações necessárias para outras bibliotecas se conectarem; especificamente o nome do host e a porta.

- **Linha de comandos** é um comando pré-formatado que chamará `redis-cli` com os parâmetros corretos.

Você localizará ambos na página *Visão geral* de seu serviço {{site.data.keyword.composeForRedis}}.

## Conectando com a linha de comandos

Você geralmente usará o comando `redis-cli` para se conectar manualmente à implementação, essa é a maneira mais direta para trabalhar remotamente com sua instalação do Redis. Isso vem como parte do pacote Redis; portanto, será necessário instalar o Redis localmente para usá-lo. No Mac OS X, uma boa maneira de obter o Redis é usando o Homebrew.

1. Instale o [brew](http://brew.sh)
2. Instale o redis com `brew install redis` para deixá-lo funcionando.

No Linux, consulte seu gerenciador de pacote de distribuição para a construção mais recente. Se estiver disposto, será possível [fazer download da origem](http://redis.io/download) e construir você mesmo. 

Tome a Linha de comandos do TCP e recorte e cole em seu terminal desta forma:
```shell
$ redis-cli -h portal.brilliant-redis-41.compose-3.composedb.com -p 15639 -a secretpassword
portal.brilliant-redis-41.compose-3.composedb.com:15639> set hello "world"
OK
portal.brilliant-redis-41.compose-3.composedb.com:15639> get hello
"world"
portal.brilliant-redis-41.compose-3.composedb.com:15639> 

```
É possível testar sua conexão executando alguns comandos simples do Redis conforme mostrado.

## Conectando-se a aplicativos

Não há nenhuma biblioteca do cliente Redis oficial. Há inúmeras bibliotecas do cliente para várias linguagens que são listadas no site do Redis. É possível ver a lista integral [aqui](http://redis.io/clients). Os clientes recomendados são marcados com uma estrela. Se você deseja iniciar rapidamente, aqui está uma seleção de clientes recomendados:       

Idioma|Biblioteca|Uso da sequência de conexões
----------|----------|-----------
Node|[ioredis](https://github.com/luin/ioredis)|[Sim](https://github.com/luin/ioredis#connect-to-redis)
Ruby|[redis-rb](https://github.com/redis/redis-rb)|[Sim](http://www.rubydoc.info/github/redis/redis-rb/master/Redis%3Ainitialize)
Java|[Lettuce](https://github.com/mp911de/lettuce)|Sim - veja [1](https://github.com/mp911de/lettuce/wiki/Redis-URI-and-connection-details), [2](https://lettuce.io/core/release/api/io/lettuce/core/RedisClient.html)

Há também um [Tour das estrelas do Redis](https://www.compose.com/articles/a-tour-of-the-redis-stars-2/) em artigos do Compose, o [Blog do Compose](https://www.compose.com/articles/) que observa os drivers recomendados para uma ampla gama de linguagens em uso comum.
