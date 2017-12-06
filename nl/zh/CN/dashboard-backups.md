---

copyright:
  years: 2017
lastupdated: "2017-07-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 备份
{: #backups}

您可以从服务仪表板的*管理*页面创建和下载备份。可以使用安排的备份和手动备份。

## 查看现有备份

数据库的每日备份会自动安排。要查看现有备份，请浏览至服务仪表板的*管理*页面。 

![备份](./images/redis-backups-show.png "服务仪表板中备份的列表")

单击相应的行以展开任何可用备份的选项。

![备份选项](./images/redis-backups-options.png "备份选项") 

## 随需应变创建备份

除了已安排的备份，您还可以手动创建备份。要创建手动备份，请浏览至服务仪表板的*管理*页面，然后单击*立即备份*。

## 下载备份

要下载备份，请浏览至服务仪表板的*管理*页面，然后单击要下载的备份相应行中的*下载*。

## 备份内容

缺省情况下，Redis 保存数据的二进制快照。然后，dump.rdb 文件可以用作备份以进行时间点恢复。要生成快照 Redis 派生，请在父进程继续正常处理数据时完成子进程的所有快照工作。备份进程不会影响应用程序或数据库。您可以下载备份副本，也可以将备份直接复原到新部署中。

## 将备份与本地数据库配合使用

您可以使用 {{site.data.keyword.composeForRedis}} 备份来运行数据库的本地副本。

1. 将 dump.rdb 文件移至它自己的目录中，例如，“db”。
2. 我们需要 Redis 配置文件来启动 Redis 实例，因此您希望使用 dump.rdb 文件将安装中的 redis.conf 文件复制到您的 db 目录中。例如，如果您已使用 homebrew 在 OSX 上安装 Redis，那么 redis.conf 文件位于 `/usr/local/etc`，因此请从 db 目录运行 `cp /usr/local/etc/redis.conf`。
3. 编辑配置文件以在启动时指向当前目录。使用文本编辑器打开 redis.conf 并将行 `dir /usr/local/var/db/redis/` 更改为 `dir .`。保存此文件并退出。
4. 在提供配置文件的 db 目录中启动 redis 服务器：`redis-server redis.conf`。

## 复原备份

要将备份复原到新服务实例，请执行以下步骤以查看现有备份，然后单击相应的行以展开要下载的备份的选项。单击**复原**按钮。此时将显示一条消息，通知您已启动复原。新服务实例将自动命名为“redis-restore-[timestamp]”，并在供应启动时显示在仪表板上。
