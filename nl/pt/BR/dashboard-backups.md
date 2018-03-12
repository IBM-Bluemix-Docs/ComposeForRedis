---

copyright:
  years: 2017,2018
lastupdated: "2017-07-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Backups
{: #backups}

É possível criar e fazer download de backups na guia _Backups_ da página _Gerenciar_ de seu painel de serviço. Backups diários, mensais e on demand estão disponíveis. Eles são retidos de acordo com planejamento a seguir:

Tipo de backup|Planejamento de retenção
----------|-----------
Diárias|Os backups diários são retidos por 7 dias
Semanal|Backups semanais são retidos por 4 semanas
Mensal|Backups mensais são retidos por 3 meses
On demand|Um backup on demand é retido. O backup retido é sempre o backup on demand mais recente.
{: caption="Tabela 1. Planejamento de retenção de backup" caption-side="top"}

Planejamentos de backup e políticas de retenção são fixos. Se você precisar manter mais backups do que o planejamento de retenção permite, faça download de backups e retenha os arquivos de acordo com as suas necessidades de negócios.

## Visualizando backups existentes

Os backups diários de seu banco de dados são planejados automaticamente. Para visualizar seus backups existentes, navegue para a página *Gerenciar* de seu painel de serviço. 

![Backups](./images/redis-backups-show.png "A list of backups in the service dashboard")

Clique na linha correspondente para expandir as opções para qualquer backup disponível.

![Backup Options](./images/redis-backups-options.png "Options for a backup.") 

## Criando um backup sob demanda

Além de backups planejados, é possível criar um backup manualmente. Para criar um backup manual, navegue para a página *Gerenciar* de seu painel de serviço e clique em *Fazer backup agora*.

## Fazendo download de um backup

Para fazer download de um backup, navegue para a página *Gerenciar* de seu painel de serviço e clique em *Fazer download* na linha correspondente para o backup que você deseja fazer download.

## Conteúdos de backup

O Redis salva uma captura instantânea binária de seus dados por padrão. O arquivo dump.rdb pode então ser usado como um backup para recuperação point-in-time. Para fazer as bifurcações do Redis de captura instantânea, para que todo o trabalho para a captura instantânea seja feito pelo processo-filho enquanto o processo pai continua a manipulação de seus dados de forma normal. O processo de backup não afeta seu aplicativo ou banco de dados. Você é capaz de fazer download de uma cópia de seus backups ou restaurá-los diretamente em uma nova implementação.

## Usando um backup com um banco de dados local

É possível usar o backup do {{site.data.keyword.composeForRedis}} para executar uma cópia local de seu banco de dados.

1. Mova o arquivo dump.rdb para seu próprio diretório, ou seja, 'db'.
2. Precisaremos de um arquivo de configuração do Redis para inicializar a instância do Redis, de maneira que você desejará copiar um arquivo redis.conf de sua instalação para o seu diretório db com o arquivo dump.rdb. Por exemplo, se você instalou o Redis no OS X com Homebrew, o arquivo redis.conf está em `/usr/local/etc`, então, da execução do diretório db, `cp /usr/local/etc/redis.conf`.
3. Edite o arquivo de configuração para apontar para o diretório atual quando ele é iniciado. Abra o redis.conf com um editor de texto e mude a linha `dir /usr/local/var/db/redis/` para `dir`. Salve o arquivo e saia.
4. Inicie o servidor redis no diretório db fornecendo o arquivo de configuração: `redis-server redis.conf`.

## Restaurando um backup

Para restaurar um backup para uma nova instância de serviço, siga as etapas para visualizar os backups existentes, em seguida, clique na linha correspondente para expandir as opções para o backup que você deseja fazer download. Clique no botão **Restaurar**. Uma mensagem é exibida para permitir que você saiba que uma restauração foi iniciada. A nova instância de serviço será nomeada automaticamente "redis-restore-[timestamp]" e aparecerá em seu painel quando o fornecimento iniciar.
