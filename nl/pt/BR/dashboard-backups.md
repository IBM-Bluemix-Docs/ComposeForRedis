---

copyright:
  years: 2017,2018
lastupdated: "2018-03-02"
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

### Usando a API para visualizar backups existentes

Uma lista de backups está disponível no terminal `GET /2016-07/deployments/:id/backups`. O Terminal Foundation com o ID da instância de serviço e o ID da implementação são ambos mostrados na _Visão geral_ do serviço. Por exemplo: 
``` 
https://composebroker-dashboard-public.mybluemix.net/api/2016-07/instances/$INSTANCE_ID/deployments/$DEPLOYMENT_ID/backups
```  

## Criando um backup sob demanda

Além de backups planejados, é possível criar um backup manualmente. Para criar um backup manual, navegue para a página *Gerenciar* de seu painel de serviço e clique em *Fazer backup agora*.

### Usando a API para criar um backup

Envie uma solicitação POST para o terminal de backups para iniciar um backup manual: `POST /2016-07/deployments/:id/backups`. Ele é imediatamente retornado com o ID do recibo e as informações sobre o backup enquanto ele está sendo executado. Será necessário verificar no terminal de backups se o backup foi concluído e localizar o backup_id antes de usá-lo. Use `GET /2016-07/deployments/:id/backups/`.

## Fazendo download de um backup

Para fazer download de um backup, navegue para a página *Gerenciar* de seu painel de serviço e clique em *Fazer download* na linha correspondente para o backup que você deseja fazer download.

### Usando a API para fazer download de um backup

Localize o backup do qual gostaria de restaurar na página _Backups_ em seu serviço e copie o backup_id ou use o `GET /2016-07/deployments/:id/backups` para localizar um backup e seu backup_id por meio da API Compose. Em seguida, use o backup_id para localizar informações e um link de download para um backup específico: `GET /2016-07/deployments/:id/backups/:backup_id`.

## Conteúdos de backup

O Redis salva uma captura instantânea binária de seus dados por padrão. O arquivo dump.rdb pode então ser usado como um backup para recuperação point-in-time. Para fazer as bifurcações do Redis de captura instantânea, para que todo o trabalho para a captura instantânea seja feito pelo processo-filho enquanto o processo pai continua a manipulação de seus dados de forma normal. O processo de backup não afeta seu aplicativo ou banco de dados. Você é capaz de fazer download de uma cópia de seus backups ou restaurá-los diretamente em uma nova implementação.

## Usando um backup com um banco de dados local

É possível usar o backup do {{site.data.keyword.composeForRedis}} para executar uma cópia local de seu banco de dados.

1. Mova o seu arquivo dump.rdb para o seu próprio diretório, digamos, 'db'.
2. Precisaremos de um arquivo de configuração do Redis para inicializar a instância do Redis, de maneira que você desejará copiar um arquivo redis.conf de sua instalação para o seu diretório db com o arquivo dump.rdb. Por exemplo, se você instalou o Redis no OS X com Homebrew, o arquivo redis.conf está em `/usr/local/etc`, então, da execução do diretório db, `cp /usr/local/etc/redis.conf`.
3. Edite o arquivo de configuração para apontar para o diretório atual quando ele é iniciado. Abra o redis.conf com um editor de texto e mude a linha `dir /usr/local/var/db/redis/` para `dir`. Salve o arquivo e saia.
4. Inicie o servidor redis no diretório db fornecendo o arquivo de configuração: `redis-server redis.conf`.

## Restaurando um backup

Para restaurar um backup para uma nova instância de serviço, siga as etapas para visualizar os backups existentes, em seguida, clique na linha correspondente para expandir as opções para o backup que você deseja fazer download. Clique no botão **Restaurar**. Uma mensagem é exibida para permitir que você saiba que uma restauração foi iniciada. A nova instância de serviço será nomeada automaticamente "redis-restore-[timestamp]" e aparecerá em seu painel quando o fornecimento iniciar.

### Restaurando por meio da CLI {{site.data.keyword.cloud_notm}}

Use as etapas a seguir para restaurar um backup de um serviço do Redis em execução para um novo serviço do Redis usando a CLI do {{site.data.keyword.cloud_notm}}. 
1. Se necessário, [faça download e instale-o](https://console.bluemix.net/docs/cli/index.html#overview). 
2. Localize o backup do qual gostaria de restaurar na página _Backups_ em seu serviço e copie o ID do backup.  
  **Ou**  
  Use o `GET /2016-07/deployments/:id/backups` para localizar um backup e seu ID por meio da API Compose. O Terminal Foundation e o ID da instância de serviço são ambos mostrados na _Visão geral_ do serviço. Por exemplo: 
  ``` 
  https://composebroker-dashboard-public.mybluemix.net/api/2016-07/instances/$INSTANCE_ID/deployments/$DEPLOYMENT_ID/backups
  ```  
  A resposta terá uma lista de todos os backups disponíveis para essa instância de serviço. Selecione o backup do qual gostaria de restaurar e copie seu ID.

3. Efetue login com a conta e as credenciais apropriadas. `bx login` (ou `bx login -help` para ver todas as opções de login).

4. Alterne para sua Organização e Espaço `bx target -o "$YOUR_ORG" -s "YOUR_SPACE"`

5. Use o comando `service create` para provisionar um novo serviço e forneça o serviço de origem e o backup específico que você está restaurando em um objeto JSON. Por exemplo:
``` 
bx service create SERVICE PLAN SERVICE_INSTANCE_NAME -c '{"source_service_instance_id": "$SERVICE_INSTANCE_ID", "backup_id": "$BACKUP_ID" }'
```
  O campo _SERVICE_ deve ser compose-for-redis e o campo _PLAN_ deve ser Padrão ou Corporativo dependendo de seu ambiente. _SERVICE\_INSTANCE\_NAME_ é onde você colocará o nome para o seu novo serviço. O _source\_service\_instance\_id_ é o ID da instância de serviço da origem do backup; ele pode ser obtido executando `bx cf service DISPLAY_NAME --guid` em que _DISPLAY\_NAME_ é o nome do serviço do redis do qual o backup é feito. 
  
  Os usuários corporativos também precisarão especificar em qual cluster implementar no objeto JSON com o parâmetro `"cluster_id": "$CLUSTER_ID"`.
  
### Migrando para uma nova versão

Alguns upgrades de versão principal não estão disponíveis na implementação em execução atual. Será necessário provisionar um novo serviço que está executando a versão com upgrade e, em seguida, migrar seus dados nele usando um backup. Esse processo é o mesmo que a restauração de um backup acima, exceto que você especificará a versão para a qual gostaria de fazer ugrade.

``` 
bx service create SERVICE PLAN SERVICE_INSTANCE_NAME -c '{"source_service_instance_id": "$SERVICE_INSTANCE_ID", "backup_id": ""$BACKUP_ID", "db_version":"$VERSION_NUMBER" }'
```

Por exemplo, restaurar uma versão mais velha de um serviço do {{site.data.keyword.composeForRedis}} para um novo serviço executando o Redis 4.0.6 será semelhante ao seguinte:
```
bx service create compose-for-redis Standard migrated_redis -c '{ "source_service_instance_id": "0269e284-dcac-4618-89a7-f79e3f1cea6a", "backup_id":"5a96d8a7e16c090018884566", "db_version":"4.0.6"  }'

