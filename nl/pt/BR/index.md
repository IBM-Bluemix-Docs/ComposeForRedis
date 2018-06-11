---

copyright:
  years: 2016,2018
lastupdated: "2018-03-27"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sobre o {{site.data.keyword.composeForRedis}}
{: #about-compose-for-redis}

O Redis é um armazenamento de valores de chave de software livre, na memória. Os valores no Redis podem ser sequências simples, hashes, listas e conjuntos ou bitmaps poderosos, hyperloglogs e índices geoespaciais. O Redis é ideal como um cache do aplicativo ou armazenamento de dados de resposta rápida. O {{site.data.keyword.composeForRedis_full}} dá a você uma configuração pré-ajustada para alta disponibilidade e persistência no disco, tudo bloqueado com recursos de segurança extras.
{:shortdesc}

**Nota:** todas as instâncias de serviço do Compose que foram
provisionadas antes de 14 de setembro de 2016 que ainda estiverem ativas poderão ser
usadas e acessadas diretamente em
[https://www.compose.com/](https://www.compose.com). Qualquer instância de serviço do Compose fornecida deste ponto em diante é acessada e usada diretamente dentro de sua conta do {{site.data.keyword.cloud}}.

## Criando uma instância de serviço do {{site.data.keyword.composeForRedis}}

É possível criar um serviço do {{site.data.keyword.composeForRedis}} por meio da página [{{site.data.keyword.composeForRedis}}](https://console.{DomainName}/catalog/services/compose-for-redis/) no catálogo do {{site.data.keyword.cloud_notm}}.

Escolha um nome do serviço e uma região, organização e espaço no qual provisionar o serviço. É possível usar o campo **Selecionar uma versão do banco de dados** para escolher nas versões do banco de dados disponíveis.

Há uma lista suspensa para selecionar a criptografia TLS/SSL. Ela é configurada como criptografia **True** por padrão. Se você selecionar **False**, o serviço será provisionado sem criptografia. Isso poderá ser usado quando os seus drivers não lidarem com criptografia e você estiver ciente dos riscos potenciais de tráfego não criptografado. 

Quando você provisiona sua instância do {{site.data.keyword.composeForRedis}}, é possível escolher os planos *Padrão* ou *Corporativo*. Com o plano *Corporativo*, é possível provisionar sua instância do {{site.data.keyword.composeForRedis}} em um cluster disponível do {{site.data.keyword.composeEnterprise}}. O {{site.data.keyword.composeEnterprise}} fornece a segurança e o isolamento requeridos pela conformidade corporativa e usa rede dedicada para assegurar o desempenho dos bancos de dados implementados. Veja a [Documentação do Compose Enterprise](../ComposeEnterprise/index.html) para obter mais detalhes.

## Gerenciando {{site.data.keyword.composeForRedis}}

É possível gerenciar seu serviço no painel de serviço. Aqui é possível localizar informações sobre o banco de dados do Compose do {{site.data.keyword.cloud_notm}} e como conectar-se a ele. Também é possível:
- gerenciar seus backups
- alocar mais recursos para seu serviço
- mudar a senha do serviço
- use listas de desbloqueio para restringir o acesso a seus bancos de dados. 

Para obter mais informações, veja [Configurações](./dashboard-settings.html).

O {{site.data.keyword.composeForRedis}} depende de funções do Cloud Foundry para gerenciar o acesso ao serviço. Somente usuários com a função de Desenvolvedor podem ver ou usar o painel de serviço. Para obter mais informações sobre as funções do Cloud Foundry, veja as páginas [Acesso ao Cloud Foundry](https://console.bluemix.net/docs/iam/cfaccess.html#cfaccess) e [Gerenciando ao acesso ao Cloud Foundry](https://console.bluemix.net/docs/iam/mngcf.html#mngcf).
{: .tip}

## Conectando-se ao {{site.data.keyword.composeForRedis}}

É possível se conectar a seu serviço usando as credenciais que são criadas junto com o serviço ou com as sequências de conexões e linha de comandos que são fornecidas na guia *Visão geral* de seu painel de serviço.

## Conectando um aplicativo {{site.data.keyword.cloud_notm}} ao {{site.data.keyword.composeForRedis}}

Para conectar um aplicativo {{site.data.keyword.cloud_notm}} a seu serviço, use as credenciais que são criadas com o serviço. É possível localizar informações sobre como conectar um aplicativo {{site.data.keyword.cloud_notm}} a um serviço {{site.data.keyword.composeForRedis}} em [Conectando um aplicativo {{site.data.keyword.cloud_notm}}](./connecting-bluemix-app.html).

## Conectando-se ao {{site.data.keyword.composeForRedis}} de fora do {{site.data.keyword.cloud_notm}}

Se você deseja se conectar ao {{site.data.keyword.composeForRedis}} de fora do {{site.data.keyword.cloud_notm}}, é possível usar as sequências de conexões fornecidas ou a linha de comandos. É possível localizar informações sobre como conectar-se em [Conectando um aplicativo externo](./connecting-external.html).
