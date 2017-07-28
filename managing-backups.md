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

# Backups
{: #backups}

You can create and download backups from the *Manage* page of your service dashboard. Both scheduled and manual backups are available.

## Viewing existing backups

Daily backups of your database are automatically scheduled. To view your existing backups, navigate to the *Manage* page of your service dashboard. 

![Backups](./images/pgbackups.png "A list of backups in the service dashboard")

## Creating a backup on demand

As well as scheduled backups you can create a backup manually. To create a manual backup, navigate to the *Manage* page of your service dashboard and click *Backup now*.

## Downloading a backup

To download a backup, navigate to the *Manage* page of your service dashboard and click *Download* in the corresponding row for the backup you wish to download.

## Backup contents

Redis saves a binary snapshot of your data by default. The dump.rdb file can then be used as a backup for point-in-time recovery. To make the snapshot Redis forks, so that all of the work for the snapshot is done by the child process while the parent process continues handling your data as normal. The backup process doesn't affect your application or database. You are able to both download a copy of your backups, or restore them directly into a new deployment.

## Using a backup with a local database

You can use your {{site.data.keyword.composeForRedis}} backup to run a local copy of your database.

1. Move your dump.rdb file into it's own directory, say 'db'.
2. We will need a Redis configuration file to start up the Redis instance, so you will want to copy a redis.conf file from your install into your db directory with the dump.rdb file. For example, if you installed Redis on OSX with homebrew, the redis.conf file is in `/usr/local/etc`, so from the db directory run, `cp /usr/local/etc/redis.conf .`
3. Edit the configuration file to point to our current directory when it starts. Open redis.conf with a text editor and change the line `dir /usr/local/var/db/redis/` to `dir .`. Save the file and exit.
4. Start the redis server in the db directory supplying the configuration file: `redis-server redis.conf`.
