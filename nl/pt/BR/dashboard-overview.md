---

Copyright:
  Years: 2017
lastupdated: "2017-09-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visão geral do serviço

A página _Visão geral_ mostra informações sobre seu banco de dados do {{site.data.keyword.cloud}} Compose. A visão geral inclui informações essenciais de identificação e o uso do recurso atual. Você também localizará uma seção para sequências de conexões que podem ser usadas com ferramentas ou fazer uso de ferramentas para se conectar a seu banco de dados.

## Detalhes da implementação

O painel _Detalhes da implementação_ mostra detalhes de seu serviço.

![Deployment Details](./images/redis-deployment-details.png "A view of the Deployment Details panel")

### Tipo

O tipo de banco de dados que é oferecido pelo serviço e a versão do banco de dados que seu serviço usa.

### Nome

Um identificador interno para o serviço.

### Uso

O tamanho de seu banco de dados e a quantia de armazenamento fornecido por seu plano de serviço.


## Conectando

Há duas maneiras de conectar um aplicativo externo a seu banco de dados. É possível se conectar usando uma **Sequência de conexões** ou com uma **Linha de comandos**. Ambas são fornecidas em sua visão geral do painel de serviço.

### HTTPS

A sequência de conexões **HTTPS** pode ser usada por algumas bibliotecas do cliente e contém todas as informações necessárias para outras bibliotecas se conectarem. É possível descobrir como usar a sequência de conexões para se conectar em [Conectando um aplicativo externo](./connecting-external.html).

**Nota:** neste momento, essa conexão **NÃO** é protegida por SSL/TLS. 

### Linha de comandos

A **Linha de comandos** é um comando pré-formatado que chamará o `redis-cli` com os parâmetros corretos. Para usá-la, você precisará ter as ferramentas do cliente Redis instaladas no sistema local. É possível descobrir mais sobre como fazer isso em [Conectando um aplicativo externo](./connecting-external.html).

**Nota:** essa conexão **NÃO** é protegida por SSL/TLS. O Redis não suporta criptografia.


